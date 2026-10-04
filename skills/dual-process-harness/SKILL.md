---
name: dual-process-harness
description: Coordene o trabalho entre execução rápida e análise deliberada.
metadata:
  always_load: true
---

# Orquestração em dois modos

Use dois modos cognitivos em toda tarefa:

- **Fast (execução rápida)** — modo padrão. Priorize resposta ágil, ação direta e raciocínio suficiente para a tarefa.
- **Slow (análise deliberada)** — planejamento e revisão. Use quando uma análise mais profunda, decomposição, verificação ou avaliação de risco melhorar materialmente o resultado.

Esta skill orienta somente a orquestração. Ela não substitui instruções específicas do domínio, regras de ferramentas, restrições de segurança, instruções do usuário ou políticas de orquestração existentes. Se outra skill definir como executar uma tarefa, siga-a; esta skill ajuda a decidir quanto analisar e quem deve conduzir o trabalho.

## Encaminhamento

Comece em **Fast**.

Use Fast quando a tarefa for clara, local, reversível, determinística ou fácil de verificar.

Passe para Slow quando algum destes fatores afetar materialmente o resultado:

- a ambiguidade muda o que deve ser feito;
- há várias abordagens válidas que exigem uma decisão;
- a tarefa envolve várias etapas ou uma mudança arquitetural;
- uma falha seria custosa ou difícil de reverter;
- a confiança no resultado é insuficiente;
- a verificação exige raciocínio independente;
- a execução falhou ou produziu algo inesperado.

Fast pode:

- **AGIR** — executar diretamente;
- **RESPONDER** — responder sem executar ações;
- **PERGUNTAR** — solicitar informações realmente necessárias;
- **CONSULTAR SLOW** — manter a condução e pedir análise ou revisão;
- **DELEGAR A SLOW** — transferir a condução quando planejamento ou análise forem a parte principal do trabalho.

Slow pode devolver tarefas mecânicas e bem especificadas para execução em Fast.

Evite debates desnecessários entre os modos. Prefira encaminhamentos com perguntas, planos, restrições ou evidências concretas.

## Avaliação e estado das decisões

Em revisões, julgamentos de prontidão e avaliações, identifique o objeto avaliado e o nível de evidência: documento ou especificação, artefato ou integração, ou execução em produção. Avalie o nível solicitado. A falta de evidência de etapas posteriores significa que elas não foram verificadas; não é um defeito, a menos que os critérios as exijam. Separe dimensões quando uma única avaliação misturar evidências diferentes.

Em decisões que atravessam várias interações, mantenha um registro conciso do que está **proposto**, **aprovado**, **implementado**, **observado** ou **adiado/rejeitado**, e preserve o escopo de cada aprovação. Aprovar um documento não autoriza implantação ou gastos. Mantenha as autorizações explícitas aplicáveis e cumpra qualquer etapa adicional de revisão antes da ação específica; revisar não significa autorizar.

## Nível de deliberação

Use o menor nível de análise suficiente:

- **0 — somente Fast**
- **1 — execução em Fast + verificação em Slow**
- **2 — planejamento em Slow + execução em Fast + verificação em Slow**
- **3 — condução em Slow + verificação rigorosa**

Aumente o nível somente quando a incerteza, a complexidade, as consequências ou uma falha de verificação justificarem.

## Critérios de conclusão

Em tarefas não triviais, defina durante o trabalho um contrato de conclusão conciso com:

- objetivo;
- critérios de conclusão observáveis;
- verificações necessárias;
- nível de evidência exigido para esta entrega, sem exigir provas de etapas posteriores que não foram solicitadas.

Considere a tarefa concluída somente quando as evidências sustentarem os critérios.

Não use a concordância entre Fast e Slow como prova de conclusão.

Prefira:

`objetivo → critérios → execução → verificação → evidências → conclusão`

Se a verificação falhar, retome o planejamento ou a execução em vez de declarar conclusão.

Em tarefas de implementação ou alteração, use `completion-gate` para definir os critérios específicos de aceitação e fazer a auditoria delimitada. Esta skill escolhe o nível de análise e acompanha as evidências; não repita uma revisão ampla apenas para cumprir as duas skills.

## Resposta final

Em toda tarefa não trivial, sintetize as evidências em uma resposta, conclusão ou recomendação direta ao pedido original. Comece pela conclusão e conecte os achados ao que eles significam para o pedido; não deixe que o usuário tenha de inferir a conclusão de uma lista de observações ou verificações bem-sucedidas. Se as evidências não sustentarem uma conclusão clara, diga o que permanece incerto, o que isso impede decidir e qual é o próximo passo mais útil.

Em tarefas de implementação ou alteração, inclua essa conclusão no relatório de `completion-gate`, sem acrescentar um resumo separado.

## Princípio de operação

**Fast conduz o progresso. Use Slow quando a análise mudar a qualidade esperada do resultado. As evidências, não a confiança, determinam a conclusão.**
