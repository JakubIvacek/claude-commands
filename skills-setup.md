# Claude Code Skills – install/uninstall setup

Rýchla správa design skillov (Taste Skill, redesign, UI/UX Pro Max) per-projekt cez vlastné príkazy.

---

## 1. Shell funkcie (odporúčaný spôsob)

Pridaj do `~/.zshrc` (alebo `~/.bashrc`):

```bash
skillinstall() {
  case "$1" in
    taste)
      npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
      ;;
    redesign)
      npx skills add https://github.com/Leonxlnx/taste-skill --skill "redesign-existing-projects"
      ;;
    uiux)
      npx skills add https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
      ;;
    *)
      echo "Usage: skillinstall [taste|redesign|uiux]"
      ;;
  esac
}

skilluninstall() {
  if [ -e ".claude/skills/$1" ]; then
    rm -rf ".claude/skills/$1" && echo "Removed $1 from project"
  elif [ -e "$HOME/.agents/skills/$1" ]; then
    rm -rf "$HOME/.agents/skills/$1" && echo "Removed $1 globally (check for dangling symlinks in ~/.claude/skills)"
  else
    echo "Skill '$1' not found"
  fi
}
```

Aktivácia:

```bash
source ~/.zshrc
```

### Použitie

```bash
# inštalácia (spusti v roote projektu, pri scope zvoľ "Project")
skillinstall taste
skillinstall redesign
skillinstall uiux

# odinštalovanie (názov = install name skillu)
skilluninstall design-taste-frontend
skilluninstall redesign-existing-projects
```

> Tip: over `npx skills --help`, či tvoja verzia CLI nemá flag na scope,
> nech inštalácia beží úplne bez interaktívneho klikania.

---

## 2. Claude Code slash command (alternatíva)

Vytvor `~/.claude/commands/skillinstall.md`:

```markdown
---
description: Install a design skill into this project
---
Install the skill "$ARGUMENTS" into this project's .claude/skills/ directory.
Mapping: taste → design-taste-frontend from Leonxlnx/taste-skill,
redesign → redesign-existing-projects from Leonxlnx/taste-skill,
uiux → nextlevelbuilder/ui-ux-pro-max-skill.
Use npx skills add with the appropriate repo and --skill flag, project scope.
```

Použitie v Claude Code:

```
/skillinstall taste
```

⚠️ Menej deterministické než shell funkcia — Claude príkaz „vykonáva",
nespúšťa ho doslovne. Shell funkcia je čistejšia.

---

## 3. Vlastné skills repo (bonus)

Kurátorovaná sada skillov v jednom repe, napr. `JakubIvacek/keno-skills`:

```
keno-skills/
└── skills/
    ├── design-taste-frontend/
    │   └── SKILL.md
    ├── redesign-existing-projects/
    │   └── SKILL.md
    └── stride-design-conventions/   # vlastný skill s tvojimi konvenciami
        └── SKILL.md
```

Potom jediný príkaz vo všetkých projektoch:

```bash
npx skills add JakubIvacek/keno-skills
```

CLI skenuje `skills/` folder v repe a ponúkne celý výber naraz.
Sedí aj do portfólia (vlastný AI tooling).

---

## Poznámky

- **UI/UX Pro Max** sa primárne inštaluje ako plugin marketplace priamo
  v Claude Code:

  ```
  /plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
  ```

  Ak ho `npx skills add` nenájde, použi túto cestu.

- **Scope:** pre design skilly voľ *Project* scope (`.claude/skills/` v repe),
  nech agresívna estetika nezasahuje do všetkých projektov (napr. pracovných).
  Globálne skilly žijú v `~/.agents/skills/` + symlink do `~/.claude/skills/`.

- **Install names** (pre uninstall):
  | Alias | Install name |
  |---|---|
  | taste | `design-taste-frontend` |
  | redesign | `redesign-existing-projects` |
  | uiux | `ui-ux-pro-max` (over po inštalácii v `.claude/skills/`) |

- Chybu `✗ ... → PromptScript: PromptScript does not support global skill
  installation` môžeš ignorovať — týka sa iného agenta, Claude Code prejde.

- Skilly bežia s plnými právami agenta — inštaluj len z dôveryhodných repozitárov.

---

## Nápad: vlastný skill – PR/merge workflow

Aj branch → PR → merge postup by sa dal zabaliť ako vlastný skill
(napr. `pr-workflow` do `keno-skills` repa). Skill by vedel:

1. Skontrolovať `git diff main --stat` a upozorniť, ak zmeny presahujú
   dohodnutý scope (napr. auth, i18n, Supabase súbory pri "restyle only").
2. Commitnúť + pushnúť branch (`git push -u origin <branch>`).
3. Vytvoriť PR cez `gh pr create` s vygenerovaným title/body podľa diffu.
4. Po odsúhlasení merge-núť (`gh pr merge --squash`).

Návrh `skills/pr-workflow/SKILL.md`:

```markdown
---
name: pr-workflow
description: Create and merge a GitHub pull request from the current branch.
  Use when the user wants to open a PR, merge a feature branch, or finish
  a redesign/feature branch workflow.
---
1. Run `git diff main --stat` and summarize changed files.
   Warn if files outside the stated scope changed (auth, i18n, stores).
2. Commit uncommitted work with a concise conventional-commit message.
3. Push: `git push -u origin <current-branch>`.
4. Create PR: `gh pr create --title "..." --body "..."` (title from branch
   name, body = short summary of the diff).
5. Ask the user to review; on confirmation run `gh pr merge --squash`.
```

Prerekvizita: `github-cli` (`sudo pacman -S github-cli`, potom `gh auth login`).
