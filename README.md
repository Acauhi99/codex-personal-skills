# Codex Personal Skills

Personal skills configured for Codex, published together for reuse and version control.

## Skills

| Skill | Purpose |
| --- | --- |
| [`clear-output`](skills/clear-output/SKILL.md) | Write concise, direct user-facing prose. |
| [`dual-process-harness`](skills/dual-process-harness/SKILL.md) | Route work between fast execution and deliberate review. |
| [`completion-gate`](skills/completion-gate/SKILL.md) | Verify changes against their acceptance criteria before calling them done. |
| [`pr-review`](skills/pr-review/SKILL.md) | Review pull requests, preview findings, and wait for authorization before submitting. |

Each skill has its own directory and `SKILL.md`, which contains its name, description, and instructions.

## Install in Codex

Codex discovers personal skills under `~/.codex/skills`. Clone this repository to a stable location, then create links from the skill directories into that directory:

```sh
git clone https://github.com/Acauhi99/codex-personal-skills.git "$HOME/dev/codex-personal-skills"
cd "$HOME/dev/codex-personal-skills"
mkdir -p "$HOME/.codex/skills"

for skill in clear-output dual-process-harness completion-gate pr-review; do
  target="$HOME/.codex/skills/$skill"
  if [ -e "$target" ] || [ -L "$target" ]; then
    printf 'Already exists; inspect before replacing: %s\n' "$target"
  else
    ln -s "$PWD/skills/$skill" "$target"
  fi
done
```

The links use the checkout as their source. Update the skills with `git -C "$HOME/dev/codex-personal-skills" pull --ff-only`.

## License

These skills are released under the [MIT License](LICENSE).
