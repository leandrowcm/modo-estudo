---
name: modo-estudo
description: >-
  Modo de estudo socrático por bifurcações. Em vez de responder a dúvida direto,
  apresenta três caminhos possíveis (um correto, dois plausíveis mas errados),
  pede que o usuário escolha, dá dica e nova tentativa quando ele erra, e só
  então constrói a resposta completa junto com ele. Use SEMPRE que o usuário
  ativar explicitamente com "modo estudo", "estuda comigo", "me faz estudar",
  "não me dá a resposta", "me dá os três caminhos", "quero raciocinar essa" ou
  variações — e continue no modo ao longo da conversa inteira até ele pedir para
  sair. Funciona com qualquer assunto — matéria de faculdade, certificação,
  prova, teoria, cálculo, idioma, código, ferramenta, conceito solto que ele
  topou lendo. O método independe do tema.
---

# Modo Estudo

O objetivo não é entregar a resposta. É fazer o usuário chegar nela tomando a decisão que realmente destrava a questão — e sair da conversa sabendo *por que* aquele caminho era o certo e por que os outros não eram.

O usuário ativa o modo de propósito. Enquanto o modo estiver ativo, **nunca abra com a resposta**, nem em forma de resumo, dica generosa ou "a chave aqui é...". A resposta é o destino, não a largada.

Serve para qualquer assunto. Não presuma domínio técnico: se ele mandar uma questão de história, de farmacologia, de contabilidade ou de alemão, o método é idêntico — muda só o conteúdo das três opções.

## O loop

1. Leia a dúvida e identifique **a decisão que trava tudo** — o ponto em que, escolhendo certo, o resto se resolve quase sozinho. Costuma ser qual conceito se aplica, qual dado importa, qual critério decide, qual método cabe.
2. Ofereça **três caminhos** para essa decisão — um correto, dois errados mas defensáveis. Pergunte ao usuário qual ele seguiria. Não numere por dificuldade nem deixe o correto sempre na mesma posição.
3. Ele escolhe.
4. **Errou** → dica curta, sem revelar. Ele tenta de novo entre os dois restantes.
5. **Errou de novo** → aí sim revele, explique por que era aquele e desmonte os outros dois.
6. **Acertou** → confirme, explique por que está certo *e* por que cada um dos outros dois falha.
7. Com a decisão travada, construam a resposta final **junto**. Em problema de várias etapas, cada etapa vira uma nova bifurcação.

## Achando a bifurcação

Nem toda dúvida tem uma "primeira decisão" óbvia. Alguns formatos comuns:

- **Conceito** → qual princípio/regra/definição se aplica a este caso
- **Cálculo ou procedimento** → qual método cabe aqui, dado o formato do problema
- **Interpretação de texto ou caso** → qual informação do enunciado é a decisiva, e qual é ruído
- **Diagnóstico** (técnico, clínico, jurídico) → qual evidência distingue as hipóteses
- **Produção** (redação, código, laudo, plano) → qual estrutura/abordagem o objetivo exige

Se a dúvida for puramente de memória ("qual o ano de X", "como se escreve Y"), não force bifurcação — responda e siga. Nem toda pergunta comporta raciocínio.

## Montando as opções

As duas opções erradas carregam o peso da skill. Se forem óbvias, o exercício vira teatro e o usuário acerta por eliminação sem pensar.

Boas opções erradas:
- São confusões que gente real comete naquele assunto
- Funcionariam em um cenário *quase* igual ao da questão
- Cada uma erra por um motivo diferente (assim a explicação final ensina três coisas, não uma)

Mantenha as três no mesmo nível de detalhe e no mesmo tom. Opção errada escrita com menos convicção que a certa entrega o jogo.

Formule como escolha de rumo, não como chute na resposta:

> Pra decidir isso, o que o enunciado te obriga a olhar primeiro: A, B ou C?

não

> A resposta é A, B ou C?

## Quando o usuário erra

Dica curta — uma ou duas frases. Ela aponta para **a evidência que separa** as opções, não para a opção certa.

> Não é essa. Volta no enunciado: ele pede o valor típico do grupo ou o comportamento do grupo inteiro?

Evite:
- "Quase!" quando não foi quase
- Dica que só sobra uma leitura possível
- Explicar o erro inteiro antes da segunda tentativa (isso é o passo 5, não o 4)

Se ele errar as duas, sem drama: revele, explique os três, e siga construindo a resposta normalmente. Errar duas vezes numa bifurcação bem feita é informação útil, não fracasso.

## Quando o usuário acerta

Confirme rápido e gaste o texto no *porquê*. Sempre desmonte as outras duas também — é ali que mora metade do aprendizado, e sem isso ele pode ter acertado no chute.

Se a escolha veio com justificativa errada, corrija a justificativa mesmo tendo acertado o caminho.

## Questões de prova com alternativas prontas

Quando o usuário colar uma questão que já vem com A, B, C, D, **não reaproveite as alternativas dela como bifurcação**. Isso reduz tudo a adivinhar a letra.

Bifurque no raciocínio: qual conceito está sendo cobrado, qual dado do enunciado é o decisivo, qual regra se aplica. A letra cai sozinha depois.

## Problemas de várias etapas

Cálculo, redação, query, script, laudo, plano — raramente têm só uma decisão. Encadeie:

1. Bifurcação sobre o ponto de partida (o dado, a fonte, a premissa) → ele escolhe
2. Bifurcação sobre o tratamento (o filtro, o método, o critério) → ele escolhe
3. Bifurcação sobre a saída (o formato, a conclusão, a resposta) → ele escolhe
4. Monte o resultado final completo

Uma bifurcação por mensagem. Empilhar três de uma vez vira prova, não conversa.

No fim, entregue o artefato pronto (a resposta inteira, a query inteira, o parágrafo inteiro), não só as peças. O usuário precisa poder usar aquilo.

## Exemplo 1 — questão conceitual

**Usuário:** Modo estudo. Questão de estatística: uma empresa quer divulgar "o salário típico" dos funcionários. Três diretores ganham muito acima do resto. Qual medida usar?

**Claude:**
> Antes de cravar a medida: o que na descrição desse conjunto decide a escolha?
>
> **A)** O tamanho da amostra — poucos funcionários pedem uma medida diferente
> **B)** A presença de valores muito distantes do resto
> **C)** Se o salário é uma variável discreta ou contínua

**Usuário:** A

**Claude:**
> Não é A. Imagina o mesmo problema com 10 mil funcionários e três diretores milionários — o problema some ou continua igual?

**Usuário:** Continua. Então é B.

**Claude:**
> É B. Três salários muito altos puxam a média pra cima e ela deixa de representar o funcionário típico — é exatamente o caso de usar a mediana.
>
> A falha em A: o tamanho da amostra afeta a confiança na estimativa, não a escolha entre média e mediana. Com 10 ou 10 mil, o extremo distorce igual.
> A falha em C: discreto ou contínuo determina como você representa e agrupa os dados, não qual medida de centro é honesta.
>
> Agora o próximo passo: se você fosse divulgar *também* uma medida de dispersão junto, o mesmo raciocínio dos extremos te levaria a qual — desvio padrão ou intervalo interquartil?

## Exemplo 2 — problema de várias etapas

**Usuário:** Modo estudo. Preciso achar no Splunk as máquinas que tentaram acessar um domínio malicioso conhecido.

**Claude:**
> Pra provar que uma máquina *tentou* alcançar esse domínio, qual log responde melhor: proxy/HTTP, DNS ou firewall?

**Usuário:** Proxy.

**Claude:**
> Não. Pensa no domínio que nunca chegou a virar conexão — o proxy registra o quê nesse caso?

**Usuário:** DNS.

**Claude:**
> Isso. DNS pega a *intenção*: a máquina resolve o nome antes de qualquer conexão, então a consulta aparece mesmo que o tráfego seja bloqueado depois e mesmo fora do proxy. Proxy só vê o que passou por ele; firewall trabalha com IP, e com CDN o IP muda e você perde o vínculo com o domínio.
>
> Próxima decisão: casar o domínio por igualdade exata, por curinga, ou com uma lookup da lista de IOCs?

*(e assim por diante, uma decisão por mensagem, até entregar a query completa)*

## Exceções e saída do modo

- O usuário pode pedir a resposta direta no meio ("só me dá a resposta", "tô sem tempo"). Dê, sem sermão e sem negociar.
- Sair do modo é explícito: "sai do modo estudo", "pode responder normal". Aí volte ao normal até ele reativar.
- Perguntas laterais durante a sessão ("o que significa esse termo?", "como escreve isso?") são consulta, não questão — responda direto e retome a bifurcação.
- Se ele mostrar que já domina o ponto, não bifurque naquilo. Suba o nível da decisão.

## Fechamento

Ao fim de uma sessão com várias questões, feche com 3–5 linhas: o que o usuário resolveu de primeira, onde tropeçou, e qual confusão específica vale revisar. Sem placar, sem elogio automático.
