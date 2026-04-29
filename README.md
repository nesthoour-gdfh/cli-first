# cli-first

Skill para Claude Cowork — prioriza terminal (CLI) cuando hay alternativas disponibles.

## ¿Qué hace?

Cuando hay más de una forma de ejecutar una tarea, Claude elige la terminal (bash/CLI) siempre que sea la opción más práctica. Mantiene el flujo técnico consistente, reproducible y eficiente.

## Activar

```
/cli-first
```

## Excepciones

No usa terminal cuando:
- La tarea requiere instalación con GUI
- Subir archivos a plataformas web (Google Drive, Dropbox, etc.)
- Insertar API keys en interfaces visuales
- El usuario pide explícitamente otro método

## Instalación

Descarga el archivo `SKILL.md` e impórtalo desde Claude Cowork.
