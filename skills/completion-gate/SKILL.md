---
name: completion-gate
description: Faça uma auditoria delimitada de cada implementação ou alteração antes de declará-la concluída. Verifique o comportamento no contexto real, corrija bloqueios e informe a validação e o estado.
---

# Critérios de conclusão

Considere uma tarefa concluída quando houver evidências suficientes de que a alteração solicitada funciona com segurança no contexto real. Não busque perfeição teórica.

## 1. Delimite a tarefa

Antes de declarar a conclusão, identifique:

- o comportamento solicitado e os critérios de aceitação;
- o tipo de entrega e o nível de evidência exigido;
- o código, os documentos e os contratos diretamente afetados;
- os chamadores, as dependências, os testes, a configuração e os fluxos de dados relevantes.

Se os critérios de aceitação estiverem implícitos, deduza-os a partir do pedido e do comportamento existente do sistema.

Não amplie a tarefa para incluir limpeza ou reformulação sem relação direta com o pedido.

### Ajuste a verificação à entrega

Use evidências adequadas à etapa solicitada. Passar em uma etapa não comprova as seguintes:

- **Documento ou especificação:** verifique a autoridade das fontes, a rastreabilidade, a consistência entre documentos, a completude, os links e os critérios de aceitação. Não é necessário comprovar a execução, a menos que isso tenha sido solicitado.
- **Esquema ou contrato:** diferencie a validade da sintaxe JSON do comportamento das instâncias, da semântica entre registros e do comportamento de adaptadores ou da execução. Verifique somente as camadas dentro do escopo.
- **Implementação ou integração:** verifique o comportamento no fluxo relevante do código e no contexto do sistema.
- **Execução ou produção:** obtenha as evidências observadas solicitadas, como resultados de POC, telemetria, custos, restauração ou comportamento de alertas.

A falta de evidências de etapas posteriores não bloqueia uma entrega anterior, a menos que os critérios de aceitação as exijam.

Em tarefas que atravessam várias interações, diferencie o que foi proposto, aprovado, implementado e observado. Registre o que cada aprovação autoriza; aprovar um documento ou uma estimativa não autoriza mudanças externas. Preserve as autorizações explícitas e cumpra qualquer etapa de revisão do repositório exigida para a alteração específica.

## 2. Implemente

Faça a menor alteração coerente que satisfaça a tarefa e as convenções existentes no projeto.

Prefira os contratos e padrões específicos do repositório a recomendações genéricas.

## 3. Faça uma auditoria de conclusão

Depois da implementação, faça uma revisão delimitada do resultado.

Verifique apenas os pontos relevantes:

- correção e casos-limite relevantes;
- chamadores, dependências, interfaces, estado, configuração e regressões;
- limites de segurança afetados, autorização, validação, segredos e entradas não confiáveis;
- impacto em desempenho ou recursos quando a escala, a latência, I/O, concorrência ou memória puderem ser afetados materialmente;
- migrações, novas tentativas, timeouts, tratamento de falhas e operação, quando aplicáveis;
- testes, build, verificação de tipos, lint ou outras validações disponíveis no projeto.

Ao escolher as verificações, siga a hierarquia de instruções vigente e a autorização do usuário. Execute somente as verificações permitidas para a tarefa e informe como não verificadas as que forem relevantes, mas não executadas.

Um achado precisa descrever uma condição concreta de falha ou um caminho plausível afetado. Não crie trabalho com base apenas em melhorias hipotéticas.

## 4. Classifique os achados

Um achado é um **bloqueio** quando pode causar materialmente:

- falha de um critério de aceitação;
- comportamento incorreto ou regressão;
- integração ou contrato quebrado;
- vulnerabilidade de segurança;
- perda ou corrupção de dados;
- regressão relevante de confiabilidade ou desempenho;
- falha de uma validação pertinente.

Corrija os bloqueios antes de declarar a conclusão.

Uma **melhoria não bloqueante** pode tornar a implementação mais limpa, genérica, rápida ou fácil de manter, mas não é necessária para atender ao pedido nem para reduzir materialmente o risco atual.

Não continue a implementação por melhorias não bloqueantes, a menos que a tarefa as exija explicitamente.

## 5. Valide novamente sem reabrir a revisão

Depois de corrigir um bloqueio, repita as verificações afetadas pela correção.

Não reinicie uma crítica ampla da implementação a cada correção.

Faça outra auditoria ampla somente se a correção tiver alterado materialmente a arquitetura, os contratos ou o escopo. Nunca faça mais de duas auditorias amplas para a mesma tarefa.

## 6. Condições para encerrar

Declare `DONE` quando:

- o comportamento solicitado estiver implementado;
- os critérios de aceitação relevantes forem atendidos;
- as validações permitidas e pertinentes passarem;
- não houver bloqueios conhecidos.

Declare `PARTIAL` ou `BLOCKED` quando restar um problema material devido à falta de informações, indisponibilidade do ambiente, dependência externa ou bloqueio não resolvido.

Registre como não verificada qualquer validação indisponível ou não permitida; não a trate silenciosamente como aprovada.

Melhorias não bloqueantes não justificam adiar `DONE`.

## Relatório final

Comece com uma frase que responda diretamente ao pedido original e diga o que foi estabelecido ou está pronto. Não faça o usuário deduzir o resultado a partir do estado ou dos detalhes da validação.

Mantenha o relatório conciso. Inclua:

- conclusão: resposta direta ou resultado;
- estado: `DONE`, `PARTIAL` ou `BLOCKED`;
- mudanças materiais;
- validações executadas e seus resultados;
- bloqueios não resolvidos ou riscos materiais conhecidos, se houver.

Opcionalmente, mencione até três melhorias não bloqueantes diretamente relevantes. Não as investigue nem detalhe, a menos que o usuário peça.
