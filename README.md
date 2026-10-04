# Skills pessoais do Codex

Skills pessoais configuradas para o Codex e reunidas para reutilização e controle de versão.

## Skills disponíveis

| Skill | Descrição |
| --- | --- |
| [`clear-output`](skills/clear-output/SKILL.md) | Escreva respostas claras e diretas. |
| [`dual-process-harness`](skills/dual-process-harness/SKILL.md) | Coordene a execução rápida com a análise deliberada. |
| [`completion-gate`](skills/completion-gate/SKILL.md) | Verifique os critérios antes de declarar uma alteração concluída. |
| [`pr-review`](skills/pr-review/SKILL.md) | Revise PRs, mostre os comentários propostos e aguarde autorização para enviá-los. |
| [`documentation-de-slop`](skills/documentation-de-slop/SKILL.md) | Revise documentação técnica para ganhar clareza, precisão e concisão. |

Cada skill tem seu próprio diretório e um arquivo `SKILL.md` com o nome, a descrição e as instruções.

## Instalação no Codex

O Codex descobre skills pessoais em `~/.codex/skills`. Clone este repositório para um local estável e crie links dos diretórios das skills para esse diretório:

```sh
git clone https://github.com/Acauhi99/codex-personal-skills.git "$HOME/dev/codex-personal-skills"
cd "$HOME/dev/codex-personal-skills"
mkdir -p "$HOME/.codex/skills"

for skill in clear-output dual-process-harness completion-gate pr-review documentation-de-slop; do
  target="$HOME/.codex/skills/$skill"
  if [ -e "$target" ] || [ -L "$target" ]; then
    printf 'Já existe; confira antes de substituir: %s\n' "$target"
  else
    ln -s "$PWD/skills/$skill" "$target"
  fi
done
```

Os links usam este clone como origem. Atualize as skills com `git -C "$HOME/dev/codex-personal-skills" pull --ff-only`.

## Licença

Estas skills são distribuídas sob a [licença MIT](LICENSE).
