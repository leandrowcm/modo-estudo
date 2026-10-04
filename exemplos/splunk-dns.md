# Exemplo completo: domínio malicioso no Splunk

Sessão ilustrativa do modo estudo em um problema de várias etapas. Cada etapa é uma bifurcação, e no fim a query sai inteira.

Os nomes de índice e de campos (`index=dns`, `query`, `src`) são genéricos. Eles mudam conforme o ambiente e a fonte dos logs.

---

**Usuário:** Modo estudo. Preciso achar no Splunk as máquinas que tentaram acessar um domínio malicioso conhecido.

**Claude:**
> Pra provar que uma máquina *tentou* alcançar esse domínio, qual log responde melhor?
>
> **A)** Proxy/HTTP
> **B)** DNS
> **C)** Firewall

**Usuário:** Proxy.

**Claude:**
> Não. Pensa no domínio que nunca chegou a virar conexão. O proxy registra o quê nesse caso?

**Usuário:** DNS.

**Claude:**
> Isso. DNS pega a intenção: a máquina resolve o nome antes de qualquer conexão, então a consulta aparece mesmo que o tráfego seja bloqueado depois e mesmo fora do proxy.
>
> A falha no proxy: ele só vê o que passou por ele.
> A falha no firewall: ele trabalha com IP, e com CDN o IP muda e você perde o vínculo com o domínio.
>
> Próxima decisão. Como casar o domínio na busca?
>
> **A)** Igualdade exata com o domínio
> **B)** Curinga cobrindo o domínio e os subdomínios
> **C)** Lookup com a lista de IOCs

**Usuário:** Igualdade exata, pra não trazer falso positivo.

**Claude:**
> Não é essa. Se a máquina infectada consultar `c2.dominio-malicioso.com`, a igualdade exata faz o quê com esse evento?

**Usuário:** Perde. Então curinga.

**Claude:**
> Curinga. Infraestrutura maliciosa costuma usar subdomínios, e a igualdade exata deixa todos eles de fora.
>
> O cuidado é escrever o curinga com o ponto: `*.dominio-malicioso.com`. Sem o ponto, `*dominio-malicioso.com` também casa com `outrodominio-malicioso.com`, que é outro domínio. Por isso a busca combina os dois: o domínio exato e `*.` para os subdomínios.
>
> A falha na lookup: ela resolve o problema de ter muitos indicadores, e aqui há um só. Além disso, por padrão a lookup casa por igualdade exata, então o problema dos subdomínios continuaria lá.
>
> Última decisão. A pergunta é *quais máquinas*. Que saída responde isso?
>
> **A)** Uma tabela com todos os eventos encontrados
> **B)** Uma agregação por máquina de origem, com contagem e primeira e última consulta
> **C)** Um gráfico das consultas ao longo do tempo

**Usuário:** B.

**Claude:**
> B. A pergunta é sobre máquinas, então a saída precisa ter uma linha por máquina. A contagem e os horários ajudam a priorizar: uma consulta isolada e centenas de consultas ao longo de dias são situações diferentes.
>
> A falha em A: a mesma máquina aparece em dezenas de linhas e você ainda precisa contar na mão.
> A falha em C: o gráfico mostra *quando* houve consulta, e a pergunta é *quem* consultou.
>
> A query completa:
>
> ```spl
> index=dns (query="dominio-malicioso.com" OR query="*.dominio-malicioso.com")
> | stats count AS consultas, min(_time) AS primeira, max(_time) AS ultima BY src
> | convert ctime(primeira) ctime(ultima)
> | sort - consultas
> ```
>
> Um ponto de atenção: dependendo de onde o log de DNS é coletado, o `src` pode ser o servidor DNS interno que repassou a consulta, e não a máquina que perguntou. Se todas as linhas apontarem para o mesmo IP, é esse o caso, e o log certo é o do próprio servidor DNS interno.
