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

### Proyecto existente (ya tiene `.claude/`)

Si el proyecto ya tiene carpeta `.claude/` con su propia config, haz merge manual:

```bash
# Clona el repo afuera del proyecto
cd /tmp
git clone git@github.com:Manuekle/.claude.git

# Vuelve a tu proyecto
cd /ruta/de/tu/proyecto

# Merge agents (cada .md es un sub-agent)
cp -n /tmp/.claude/agents/*.md .claude/agents/

# Merge skills
cp -rn /tmp/.claude/skills/* .claude/skills/

# Merge commands
cp -n /tmp/.claude/commands/*.md .claude/commands/

# Merge hooks
cp -n /tmp/.claude/hooks/*.py .claude/hooks/

# Merge settings.json (UNION de permisos, no overwrite)
# Mezcla manual: combina arrays "allow" de ambos archivos
```

**Recomendado**: Usa `diff` para revisar diferencias antes de mezclar:
```bash
diff .claude/settings.json /tmp/.claude/settings.json
```

Los archivos existentes NO se sobrescriben (flag `-n` en cp). Si quieres reemplazar los tuyos por estos, omite `-n`.

### Post-instalación

Verifica que funcione:
```bash
# Claude debería cargar agents, commands y hooks
# Prueba un comando:
/commit --help

# O ejecuta un agente:
Usa el Agent tool para lanzar "test-runner"
```

## Cómo empezar a usar Claude Code

### 1. Abrir Claude Code

```bash
# En la raíz de tu proyecto
claude

# O apuntando a un directorio específico
claude /ruta/del/proyecto
```

### 2. Usar comandos slash

Los comandos slash se escriben directo en el chat:

```
/commit         → Crea commit convencional de cambios recientes
/arch-review    → Revisa arquitectura del código
/bugs           → Busca errores lógicos
/ui-review      → Revisa UI/UX y accesibilidad
/arewedone      → Verifica que los cambios estén completos
```

### 3. Invocar agents

Los agents se lanzan desde el chat con el Agent tool:

```
"Ejecuta el test-runner para verificar que todo pase"
"Usa el architecture-reviewer para revisar src/components/"
"Lanza el bug-finder en esta función que acabo de escribir"
```

Claude Code detecta automáticamente cuándo usar un agente según la descripción del mismo.

### 4. Usar skills

Las skills cargan conocimiento especializado. Claude las usa automáticamente cuando el contexto lo requiere:

- Tocas un archivo Prisma → carga skill `prisma-expert`
- Hablas de rendimiento → carga skill `performance`
- Mencionas SEO → carga skill `seo-geo`
- Trabajas con Supabase → carga skill `supabase`

También puedes forzar una skill:
```
"Usa la skill de accessibility para revisar este componente"
"Carga la skill de frontend-design para mejorar esta landing page"
```

### 5. Flujo de trabajo típico

```bash
# 1. Abres Claude en tu proyecto
claude

# 2. Pides un cambio
"Agrega una página de login con email y contraseña"

# 3. Claude implementa, luego usas /arch-review para revisar
/arch-review

# 4. Corriges si hay observaciones, luego /arewedone
/arewedone

# 5. Finalmente /commit para hacer commit
/commit

# 6. Y /bugs para asegurarte que no hay errores
/bugs
```

### 6. Atajos útiles

| Acción | Comando |
|--------|---------|
| Limpiar conversación | `/clear` |
| Mostrar costo de sesión | `/cost` |
| Compactar contexto | `/compact` |
| Cambiar modelo | `/model sonnet` |
| Ver settings activos | `/settings` |
| Ayuda rápida | `/help` |

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
