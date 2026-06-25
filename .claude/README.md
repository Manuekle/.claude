# .claude — Config portable para Claude Code

Configuración personal de Claude Code con agents, skills, commands y hooks listos para usar en cualquier proyecto.

## Instalación

### Opción 1: Clonar directo en `~/.claude/` (global)

```bash
git clone git@github.com:Manuekle/.claude.git ~/.claude
```

### Opción 2: Por proyecto

```bash
# En la raíz del proyecto
git clone git@github.com:Manuekle/.claude.git .claude
# O como submódulo
git submodule add git@github.com:Manuekle/.claude.git .claude
```

### Opción 3: Copiar manual

```bash
git clone git@github.com:Manuekle/.claude.git
cp -r .claude/ ~/.claude/
```

> **Nota**: Los hooks en `settings.json` usan paths relativos (`.claude/hooks/`). Si copias a `~/.claude/`, cambia los paths en `settings.json` de `.claude/hooks/` a `~/.claude/hooks/`.

## Qué incluye

| Ruta | Descripción |
|------|-------------|
| `settings.json` | Permisos, hooks, plugins, modelo |
| `CLAUDE.md` | Instrucciones base para Claude |
| `agents/` | 13 sub-agents (arquitectura, bugs, rendimiento, UI/UX, etc.) |
| `skills/` | 39 skills reutilizables (Prisma, Sentry, SEO, Supabase, Vercel, etc.) |
| `commands/` | 8 comandos slash (`/commit`, `/arch-review`, `/bugs`, etc.) |
| `hooks/` | 3 hooks pre/post tool use (emoji guard, github guard, CLAUDE.md protect) |

## Comandos disponibles

| Comando | Descripción |
|---------|-------------|
| `/commit [desc]` | Commit convencional inteligente |
| `/arch-review [path]` | Revisión de arquitectura |
| `/arewedone` | Verificación de integridad estructural |
| `/bugs [path]` | Caza de bugs lógicos y edge cases |
| `/docs [path]` | Workflow completo de documentación |
| `/perf-check [path]` | Análisis de rendimiento |
| `/ui-review [path]` | Revisión UI/UX y accesibilidad |
| `/review-gauntlet` | Ejecuta todos los revisores en paralelo |

## Agents destacados

- **architecture-reviewer** — Revisa integridad estructural, escalabilidad y mantenibilidad
- **bug-finder** — Busca errores lógicos, race conditions y edge cases
- **structural-completeness-reviewer** — Verifica que cambios estén bien integrados
- **ui-ux-perf-a11y-auditor** — Auditoría completa de UI, rendimiento y accesibilidad
- **test-runner** — Ejecuta suite de tests y reporta resultados
- **compatibility-reviewer** — Detecta rupturas silenciosas en interfaces públicas

## Skills disponibles

Prisma, Sentry, Supabase, Vercel React, Vercel React Native, SEO, UI/UX Pro, SVG Logo Designer, Canvas Design, Framer Motion, Core Web Vitals, Performance, Accessibility, Brainstorming, Algorithmic Art, Frontend Design, Web Quality Audit, y más.

## Hooks

| Hook | Disparador | Función |
|------|-----------|---------|
| `emoji_remover.py` | Post-Edit/Write | Bloquea emojis en archivos |
| `github_issue_guard.py` | Pre-Bash/MCP GitHub | Evita menciones a Claude/Anthropic en issues |
| `protect_claude_md.py` | Pre-Edit/Write | Protege CLAUDE.md de modificaciones automáticas |

## Personalización

1. **Modelo**: Cambia `"model"` en `settings.json`
2. **Permisos**: Agrega/quita entradas en `permissions.allow`
3. **Effort**: Ajusta `"effortLevel"` (low/medium/high)
4. **StatusLine**: Compila `statusline.go` o usa `build_statusline.sh`

## Links

- [Docs Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview)
- [Settings](https://docs.anthropic.com/en/docs/claude-code/settings)
- [Skills](https://code.claude.com/docs/en/skills)
- [Slash Commands](https://docs.anthropic.com/en/docs/claude-code/slash-commands)
- [Sub-agents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- [Hooks](https://docs.anthropic.com/en/docs/claude-code/hooks-guide)
