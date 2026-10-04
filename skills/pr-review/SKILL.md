---
name: pr-review
description: Revise pull requests somente quando solicitado explicitamente. Compare as mudanças com os padrões do projeto e a documentação oficial, mostre uma prévia dos comentários e aguarde autorização antes de enviar a revisão.
---

# Revisão de PR

## Ativação e escopo

Use esta skill somente quando o usuário invocar `$pr-review` ou pedir explicitamente o uso da skill `pr-review`. Um pedido comum para revisar um PR não ativa esta skill.

Revise o PR solicitado e prepare uma revisão no GitHub. Não altere a branch do PR, não faça merge, push ou commit como parte desta skill. Não execute testes, a menos que o usuário peça; consulte os resultados de CI existentes.

## Fluxo de revisão

1. **Verifique as convenções do repositório e do PR.** Localize o repositório correto e leia os arquivos `AGENTS.md` e `CLAUDE.md` aplicáveis, modelos de PR, `CODEOWNERS`, configurações de revisores e orientações pertinentes à revisão. Confira o estado atual do PR, os commits base e de origem, os arquivos alterados, as revisões e os comentários existentes e as verificações de CI. Revise o commit mais recente, não uma branch local desatualizada. Não altere a configuração do repositório para adaptá-la à revisão.

2. **Entenda o comportamento solicitado.** Use a descrição da tarefa, os critérios de aceitação e as observações sobre o que está fora de escopo como contrato de revisão. Identifique os chamadores do código alterado, o fluxo de dados, os contratos de persistência e de API e os testes relacionados.

3. **Confirme os achados com evidências.** Compare a implementação com padrões pertinentes na mesma base de código. Para detalhes sujeitos a mudanças de frameworks, bancos de dados, GitHub ou outras tecnologias, consulte documentação oficial e use fontes primárias. Pesquise na web quando a informação puder ter mudado, for específica ou exigir uma citação precisa. Diferencie defeitos confirmados de riscos condicionais e informe a condição que ativa cada risco.

4. **Torne os achados acionáveis.** Relate comportamentos que possam violar um critério de aceitação ou causar um problema concreto de confiabilidade, dados, segurança, desempenho ou integração. Evite sugestões apenas de estilo e preocupações especulativas. Vincule cada comentário a uma linha alterada. Trate um problema por comentário, explique brevemente a condição de falha e o impacto e inclua links para documentação oficial ou padrões locais quando forem pertinentes. Siga as convenções de severidade do repositório; caso não existam, use um título curto e um rótulo de prioridade somente quando ajudar. Inclua um esboço de código quando isso deixar a correção mais clara.

## Prévia obrigatória antes de publicar

Sempre mostre ao usuário uma prévia da revisão antes de enviar uma aprovação ou comentários. Para cada comentário proposto em linha, inclua:

- o arquivo e a linha do diff;
- por que o achado merece um comentário, com evidências e condições aplicáveis;
- o texto exato do comentário formatado, incluindo links pertinentes e código sugerido, se houver.

Informe também se não há achados acionáveis. Nesse caso, mostre que a ação será somente uma aprovação, sem comentário geral no PR. Quando houver achados, mostre o texto exato do comentário geral da revisão: `Mais detalhes nos comentários.`

Após a prévia, pare e aguarde autorização explícita do usuário para enviar exatamente aquela revisão. Um pedido anterior para revisar, aprovar ou comentar não substitui esta etapa. Se o commit de origem do PR mudar depois da prévia, confira novamente o diff afetado e mostre uma prévia atualizada antes de enviar. Nunca publique comentários que não foram apresentados ou que estejam desatualizados.

## Política de envio

Após a autorização, siga a política de revisão deste usuário:

- **Sem achados acionáveis:** envie `APPROVE`, sem texto e sem comentários.
- **Com um ou mais achados:** envie `APPROVE` com os comentários em linha apresentados na prévia e o texto geral exato `Mais detalhes nos comentários.` Não use `REQUEST_CHANGES`, a menos que o usuário altere explicitamente essa política.

Verifique novamente o estado do PR imediatamente antes do envio. Se o PR já tiver sido mesclado ou fechado, não envie uma aprovação retroativa. Explique que a aprovação já não pode afetar o PR e publique os comentários apresentados na prévia somente se ainda forem úteis e o usuário tiver autorizado. Para comentários em linha, use o commit atual e os campos de caminho, linha e lado do diff aceitos pela API do GitHub; não use os campos obsoletos de posição no diff. Prefira enviar uma única revisão com os comentários autorizados e o evento de revisão.

Após o envio, verifique o estado da revisão, o commit, o texto geral e o caminho, a linha e o texto de cada comentário. Se o resultado for incerto, consulte o GitHub antes de tentar novamente, para evitar duplicatas.

## Resposta final

Mantenha o relatório final curto. Inclua um link para a revisão ou os comentários enviados. Informe se o PR foi aprovado, se comentários foram publicados e se alguma mudança de estado impediu a aprovação. Quando não houver comentários, diga apenas que a revisão foi aprovada, sem acrescentar um comentário geral ao PR.
