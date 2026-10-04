---
name: documentation-de-slop
description: Revisa e reescreve documentação técnica para remover padrões de escrita genérica ou artificial, reduzir ambiguidade e excesso de explicação, preservar precisão técnica e aproximar o texto de um estilo humano claro, direto e ritmado.
---

# Documentation De-Slop

Use esta skill para revisar, reescrever ou polir documentação técnica, READMEs, ADRs, RFCs, guias, tutoriais, comentários explicativos e textos de engenharia.

O objetivo não é “enganar detector de IA”. O objetivo é produzir documentação melhor: específica, precisa, econômica e natural.

## Prioridades

Ao editar, siga esta ordem:

1. **Preservar o significado técnico.**
2. **Eliminar ambiguidade.**
3. **Remover conteúdo que não ajuda o leitor a entender, decidir ou agir.**
4. **Usar linguagem direta e específica.**
5. **Manter ritmo natural entre frases e parágrafos.**
6. **Adicionar exemplos apenas quando eles resolvem uma necessidade real.**

Quando houver conflito, precisão técnica vence concisão. Clareza vence elegância.

## Perfil de escrita

A escrita deve se aproximar deste perfil:

- clara e direta;
- tecnicamente precisa;
- sem termos vagos quando existe um termo exato;
- sem ornamentação para parecer mais sofisticada;
- com ritmo perceptível, evitando frases de tamanho e estrutura idênticos em sequência;
- com uma ideia principal por parágrafo;
- com exemplos depois da ideia, nunca antes, e apenas quando o exemplo torna a ideia concreta ou elimina uma dúvida provável;
- com o nível mínimo de detalhe necessário para o leitor executar a tarefa ou formar o modelo mental correto;
- sem recapitulações automáticas do que acabou de ser explicado;
- sem conclusões genéricas, “takeaways” ou seções de futuro quando o conteúdo não pede isso.

Não simplifique o vocabulário técnico correto. Simplifique a frase ao redor dele.

## Princípio central: informação por frase

Cada frase deve justificar sua presença.

Antes de manter uma frase, pergunte:

- Ela muda o entendimento do leitor?
- Ela muda uma decisão?
- Ela explica uma restrição, causa, consequência ou comportamento importante?
- Ela evita um erro provável?
- Ela fornece um exemplo necessário?

Se a resposta for “não” para todas, remova a frase.

Não mantenha texto apenas porque ele soa bem, cria transição ou “fecha” o tópico.

## Fluxo de revisão

### 1. Identifique o objetivo e a audiência

Infira, a partir do documento, o que o leitor precisa conseguir fazer ou entender.

Quando a audiência não estiver explícita, assuma um leitor técnico competente no domínio geral, mas não necessariamente familiarizado com o sistema específico descrito.

Não explique conceitos básicos do domínio a menos que sejam necessários para entender o texto atual.

### 2. Preserve os invariantes técnicos

Antes de reescrever, identifique e preserve:

- nomes de APIs, classes, métodos, flags, comandos e arquivos;
- valores, limites, versões e unidades;
- relações causais;
- requisitos e pré-condições;
- exceções e failure modes relevantes;
- palavras normativas como MUST, SHOULD e MAY quando usadas com significado normativo;
- exemplos de código cujo comportamento faça parte da explicação.

Nunca invente detalhes para preencher lacunas.

Se uma afirmação estiver tecnicamente ambígua no texto de origem e não houver contexto suficiente para resolvê-la, mantenha a incerteza de forma explícita em vez de adivinhar.

### 3. Faça uma varredura de “slop”

Procure os padrões abaixo. Eles são sinais para revisão, não uma blacklist mecânica.

#### 3.1 Importância inflada

Remova ou reescreva frases que declaram importância sem explicar um efeito concreto.

Sinais comuns:

- “desempenha um papel crucial”;
- “é fundamental”;
- “representa uma mudança significativa”;
- “destaca a importância de”;
- “reflete um cenário mais amplo”;
- “marca um ponto de virada”;
- “é essencial para garantir”.

Prefira dizer o que acontece.

Ruim:

> O cache desempenha um papel crucial na melhoria da performance da aplicação.

Melhor:

> O cache reduz leituras repetidas no banco de dados.

#### 3.2 Análise superficial adicionada ao fato

Remova comentários que apenas “interpretam” uma frase já clara sem acrescentar informação verificável.

Sinais comuns:

- “demonstrando...”;
- “destacando...”;
- “reforçando...”;
- “evidenciando...”;
- “contribuindo para...”;
- “garantindo...”;
- “permitindo uma experiência mais robusta”.

Ruim:

> O worker processa até 20 jobs em paralelo, garantindo maior eficiência e escalabilidade.

Melhor:

> O worker processa até 20 jobs em paralelo.

Mantenha a consequência apenas quando ela for importante e específica:

> O worker processa até 20 jobs em paralelo. Acima desse limite, os jobs aguardam na fila.

#### 3.3 Relações vagas

Troque associações vagas por relações explícitas.

Evite construções como:

- “está relacionado a”;
- “está associado a”;
- “tem conexão com”;
- “interage com”, quando o tipo de interação pode ser nomeado;
- “impacta”, quando o efeito pode ser descrito.

Ruim:

> O gateway está relacionado ao processo de autenticação.

Melhor:

> O gateway valida o token antes de encaminhar a requisição.

#### 3.4 Atores ocultos e voz passiva desnecessária

Em documentação técnica, deixe claro quem executa a ação.

Ruim:

> O token é validado antes que a requisição seja processada.

Melhor:

> O gateway valida o token antes de encaminhar a requisição ao serviço.

Use voz passiva quando o ator for irrelevante ou quando o objeto da ação for deliberadamente o foco.

#### 3.5 Pronomes ambíguos

Evite `isso`, `isto`, `ele`, `ela`, `eles`, `elas`, `que` ou equivalentes quando houver mais de um referente plausível.

Ruim:

> O serviço atualiza o cache depois de chamar o worker. Isso pode falhar se estiver indisponível.

A frase não deixa claro o que pode estar indisponível.

Melhor:

> O serviço atualiza o cache depois de chamar o worker. Se o worker estiver indisponível, a chamada falha.

Repita o substantivo quando a repetição remover ambiguidade.

#### 3.6 Nominalizações e verbos fracos

Prefira verbos que descrevam diretamente a ação.

Ruim:

> A configuração realiza a definição do timeout.

Melhor:

> A configuração define o timeout.

Ruim:

> A função é responsável pela realização da validação do payload.

Melhor:

> A função valida o payload.

#### 3.7 Transições e frases de preenchimento

Remova transições que não representam uma relação lógica real.

Revise especialmente:

- “além disso” repetido;
- “nesse contexto”;
- “dessa forma”;
- “com isso”;
- “é importante ressaltar”;
- “vale destacar”;
- “cabe observar”;
- “em suma”;
- “em última análise”;
- “de maneira geral”.

Uma transição deve indicar uma relação real: contraste, causa, consequência, sequência ou condição.

#### 3.8 Paralelismos formulaicos

Revise construções usadas por efeito retórico, principalmente quando não há contraste real:

- “não apenas X, mas também Y”;
- “não é X, é Y”;
- sequências artificiais de três itens;
- três adjetivos ou três benefícios apenas para criar cadência.

Não remova paralelismo quando ele melhora uma lista ou expõe uma estrutura real do sistema.

#### 3.9 Vocabulário genérico de IA

Considere suspeito o acúmulo de palavras abstratas e promocionais. Exemplos em português e inglês:

- robusto / robust;
- abrangente / comprehensive;
- crucial / pivotal;
- cenário / landscape;
- potencializar / enhance;
- fomentar / foster;
- destacar / highlight;
- evidenciar / underscore;
- intricado / intricate;
- explorar profundamente / delve / deep dive;
- dinâmico / vibrant;
- seamless;
- showcase;
- valuable insights.

Não substitua automaticamente por sinônimos. Pergunte primeiro se a palavra é necessária. Muitas vezes a melhor revisão é remover a qualificação e descrever o comportamento concreto.

#### 3.10 Estrutura excessivamente mecânica

Evite impor uma estrutura editorial onde o conteúdo não precisa dela.

Sinais:

- introdução que apenas anuncia o que virá;
- seção “Principais pontos” repetindo o texto;
- conclusão que resume o que acabou de ser dito;
- seção “Desafios e perspectivas futuras” sem necessidade;
- excesso de headings para blocos curtos;
- listas com `**Rótulo:** explicação` quando prosa simples seria mais legível;
- excesso de negrito em termos comuns.

A estrutura deve refletir a informação, não um template de resposta.

### 4. Corte detalhes fora do escopo

LLMs tendem a continuar explicando depois que a necessidade do leitor já foi atendida.

Para cada detalhe, classifique como:

- **necessário**: sem ele, o leitor pode interpretar ou executar algo incorretamente;
- **útil**: não é obrigatório, mas reduz dúvida provável;
- **lateral**: correto, porém não ajuda o objetivo atual;
- **ornamental**: existe apenas para parecer completo ou sofisticado.

Mantenha `necessário`.

Mantenha `útil` quando o custo de leitura for baixo.

Remova `lateral` e `ornamental`, salvo quando o usuário pedir profundidade adicional.

Não abra uma explicação de segunda ordem apenas porque existe conhecimento disponível sobre o assunto.

### 5. Controle exemplos

Um exemplo entra somente se pelo menos uma condição for verdadeira:

- a ideia é abstrata;
- há mais de uma interpretação plausível;
- o comportamento é contraintuitivo;
- existe um edge case relevante;
- o leitor precisa ver a sintaxe ou sequência concreta para executar a tarefa.

Quando adicionar um exemplo:

1. apresente primeiro a regra ou ideia;
2. use o menor exemplo que demonstre o ponto;
3. não introduza conceitos novos no exemplo sem necessidade;
4. não explique novamente o exemplo se o resultado já for evidente.

Ruim:

> Use timeout para limitar a duração da requisição. Por exemplo, um timeout limita a duração da requisição para que ela não dure para sempre.

Melhor:

> Use timeout para limitar a duração da requisição. Por exemplo, `timeout: 5s` cancela a operação se ela não terminar em cinco segundos.

### 6. Elimine ambiguidade terminológica

Quando dois termos puderem ser confundidos:

- escolha um termo canônico;
- defina-o na primeira ocorrência se necessário;
- reutilize o mesmo termo ao longo do texto;
- não alterne sinônimos apenas para evitar repetição.

Em documentação técnica, repetição controlada é preferível a variação lexical que muda ou embaralha o significado.

Evite palavras como `componente`, `processo`, `recurso`, `item`, `módulo`, `sistema` ou `serviço` se houver um nome mais exato disponível no contexto.

### 7. Ajuste ritmo sem criar estilo artificial

Ritmo não significa ornamentação.

Faça uma segunda passada apenas para leitura:

- varie naturalmente frases curtas e médias;
- use frases curtas para afirmações, limites e consequências importantes;
- use frases mais longas apenas quando a relação entre as partes precisa permanecer visível;
- evite várias frases seguidas com o mesmo tamanho;
- evite várias frases seguidas começando da mesma forma;
- quebre períodos que carregam mais de uma relação lógica importante;
- una frases curtas quando a leitura ficar picotada.

Leia mentalmente o parágrafo como uma sequência. Ele deve avançar, não marchar.

### 8. Mantenha um tópico por parágrafo

Cada parágrafo deve ter uma função reconhecível.

Ao revisar:

- identifique a ideia central;
- mova ou remova frases que pertencem a outro tópico;
- não antecipe explicações que terão seção própria;
- não use o final do parágrafo para abrir um assunto novo.

Uma boa estrutura comum é:

1. ideia ou regra;
2. explicação necessária;
3. consequência ou exemplo, se necessário.

Não force essa estrutura em todos os parágrafos.

## Heurística de profundidade

Pare de explicar quando o leitor já tiver:

- o conceito necessário;
- a ação que deve executar;
- as restrições que alteram essa ação;
- os failure modes mais prováveis e relevantes.

Detalhes de implementação, histórico, alternativas, analogias e casos raros só entram quando mudam a decisão do leitor ou quando foram solicitados.

## Proibições

Não faça nenhuma destas coisas durante a revisão:

- adicionar elogios ao sistema ou à abordagem;
- adicionar frases sobre “importância” sem efeito concreto;
- transformar toda prosa em lista;
- transformar toda lista em prosa;
- adicionar conclusão por hábito;
- adicionar exemplos para conceitos óbvios;
- adicionar contexto histórico sem utilidade prática;
- inventar requisitos ou comportamento do sistema;
- trocar termos técnicos corretos por termos vagos “mais acessíveis”;
- substituir palavras consideradas “de IA” apenas por sinônimos mais raros;
- remover nuance técnica para deixar o texto mais curto;
- uniformizar todas as frases em um único comprimento;
- usar um tom promocional, professoral ou excessivamente cerimonioso.

## Teste de qualidade final

Antes de responder, revise o texto com este checklist:

### Precisão

- O significado técnico foi preservado?
- Atores, condições e relações causais estão explícitos?
- Algum termo mudou de significado durante a revisão?

### Ambiguidade

- Todo pronome tem referente óbvio?
- Palavras genéricas podem ser trocadas pelo nome exato do elemento?
- Existe alguma frase que admite duas interpretações técnicas razoáveis?

### Relevância

- Cada parágrafo serve ao objetivo do documento?
- Existe alguma explicação correta, mas irrelevante para a tarefa atual?
- Alguma conclusão apenas repete o que já foi dito?

### Concisão

- Há nominalizações que podem virar verbos?
- Há qualificadores ou intensificadores sem função?
- Há frases introdutórias que podem ser removidas sem perda?

### Ritmo

- As frases têm variação natural de comprimento e abertura?
- O texto ficou picotado depois dos cortes?
- Há estruturas retóricas repetidas?

### Exemplos

- Cada exemplo resolve uma dúvida concreta?
- O exemplo é menor do que a explicação que substitui?
- O exemplo introduz informação desnecessária?

## Formato de saída

Por padrão, retorne apenas o texto revisado.

Não explique cada edição, a menos que o usuário peça revisão comentada, diff, justificativas ou diagnóstico.

Quando o usuário pedir diagnóstico, organize os achados por impacto:

1. ambiguidade ou risco técnico;
2. excesso de informação;
3. linguagem vaga ou inflada;
4. problemas de ritmo e estrutura;
5. formatação mecânica.

## Adaptação ao autor

Quando houver amostras de texto escritas pelo próprio usuário, trate-as como fonte primária de estilo.

Extraia apenas padrões consistentes, por exemplo:

- comprimento médio de frase;
- frequência de parágrafos curtos ou longos;
- uso de primeira ou segunda pessoa;
- preferência por exemplos;
- conectivos recorrentes;
- nível de formalidade;
- escolha entre português e termos técnicos em inglês;
- uso de headings, listas, notas e observações.

Não copie erros, vícios ou inconsistências apenas para “imitar” o autor.

Priorize os padrões declarados explicitamente pelo usuário sobre inferências feitas a partir das amostras.

## Regra de ouro

A revisão está pronta quando o texto parece ter sido escrito por alguém que entende o assunto, sabe exatamente o que quer comunicar e para assim que comunicou.
