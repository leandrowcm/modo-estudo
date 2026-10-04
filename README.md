# modo-estudo

Uma skill para o Claude que troca a resposta pronta por três caminhos para eu escolher.

## Por que criei

Uso o Claude para estudar, tanto para a faculdade quanto para a minha transição para Blue Team/SOC. Com o tempo percebi que eu sempre recebia a resposta de mão beijada. Eu perguntava, vinha a explicação completa, eu lia, fazia sentido e eu seguia para a próxima dúvida.

Ou seja, quem fazia o raciocínio era o Claude. Eu só lia.

Pensando nisso, escrevi esta skill. Quando ativo o modo estudo, o Claude deixa de responder direto e passa a me obrigar a tomar a decisão que destrava a questão.

## Como funciona

1. Ele lê a dúvida e identifica a decisão que trava tudo, aquela que, escolhida certo, faz o resto se resolver quase sozinho.
2. Apresenta três caminhos para essa decisão: um correto e dois errados, mas defensáveis.
3. Eu escolho.
4. Se erro, recebo uma dica curta que aponta para a evidência que separa as opções, sem entregar a resposta, e tento de novo.
5. Se erro de novo, ele revela e explica.
6. Quando acerto, ele explica por que aquele caminho está certo e por que cada um dos outros dois falha.
7. Com a decisão tomada, a resposta final é construída junto. Em problema de várias etapas, cada etapa vira uma nova bifurcação.

Funciona com qualquer assunto. O método é o mesmo, muda só o conteúdo das três opções.

## Exemplo

Este é um dos exemplos que deixei dentro da skill:

> **Eu:** Modo estudo. Preciso achar no Splunk as máquinas que tentaram acessar um domínio malicioso conhecido.
>
> **Claude:** Pra provar que uma máquina *tentou* alcançar esse domínio, qual log responde melhor: proxy/HTTP, DNS ou firewall?
>
> **Eu:** Proxy.
>
> **Claude:** Não. Pensa no domínio que nunca chegou a virar conexão. O proxy registra o quê nesse caso?
>
> **Eu:** DNS.
>
> **Claude:** Isso. DNS pega a intenção: a máquina resolve o nome antes de qualquer conexão, então a consulta aparece mesmo que o tráfego seja bloqueado depois e mesmo fora do proxy. Proxy só vê o que passou por ele. Firewall trabalha com IP, e com CDN o IP muda e você perde o vínculo com o domínio.
>
> Próxima decisão: casar o domínio por igualdade exata, por curinga, ou com uma lookup da lista de IOCs?

E assim segue, uma decisão por mensagem, até a query completa. A sessão inteira está em [`exemplos/splunk-dns.md`](exemplos/splunk-dns.md).

## Como instalar

A skill é um arquivo só: [`modo-estudo/SKILL.md`](modo-estudo/SKILL.md).

**No Claude (app ou navegador):** baixe a pasta `modo-estudo`, compacte em `.zip` e envie na área de skills das configurações. O recurso de skills precisa estar habilitado na sua conta.

**No Claude Code:** copie a pasta `modo-estudo` para `~/.claude/skills/`.

## Como usar

Para ativar, basta escrever "modo estudo" antes da dúvida. Também funciona com "estuda comigo", "não me dá a resposta" ou "quero raciocinar essa".

O modo continua ativo durante a conversa inteira. Para sair, "sai do modo estudo" ou "pode responder normal".

Se eu estiver sem tempo, posso pedir a resposta direta no meio da sessão e ele entrega, sem sermão.

## O que ela ainda não resolve

- A skill depende de as duas opções erradas serem boas. Se elas saem óbvias, dá para acertar por eliminação sem pensar, e o exercício perde o sentido.
- Pergunta de pura memória (uma data, uma grafia) não vira bifurcação. Nesses casos ela responde direto.
- Ainda estou usando e ajustando. O que eu mudar vai aparecendo no histórico de commits.

## Adaptar

O texto da skill foi escrito para o meu jeito de estudar. Se quiser mudar o número de opções, o tom das dicas ou os exemplos, é só editar o `SKILL.md`. Sugestões são bem-vindas nas issues.

## Licença

MIT
