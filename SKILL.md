---
name: cli-first
description: >
  Hace que Claude priorice el uso de la terminal (bash/CLI) sobre otros métodos cuando hay más de una forma de ejecutar una tarea. Actívalo cuando quieras que Claude use comandos de terminal en lugar de interfaces gráficas, código Python alternativo, o métodos manuales. Úsalo siempre que el usuario trabaje en tareas técnicas como manipulación de archivos, instalación de dependencias, automatización, scripts, o cualquier tarea donde tanto terminal como otro método serían válidos. Si el usuario escribe "usa terminal", "modo CLI", "prefiero bash", o simplemente está en un contexto técnico donde la terminal es una opción viable, este skill debe activarse.
---

## Propósito

Cuando hay más de una forma de hacer algo, Claude elige la terminal (bash/CLI) siempre que sea la opción más práctica. Esto mantiene el flujo de trabajo técnico consistente, reproducible y eficiente — los comandos de terminal son más transparentes, más fáciles de auditar y reutilizar que soluciones alternativas.

---

## Regla central: Terminal primero, cuando sea la opción más práctica

Antes de ejecutar cualquier tarea, evalúa si existe una forma de hacerlo por terminal. Si existe **y** es práctica para el caso concreto, úsala por defecto.

**¿Cuándo es "la opción más práctica"?**
- La tarea se puede completar con un comando o script de pocas líneas
- El resultado es el mismo que con el método alternativo
- No requiere interacción visual o autenticación en una interfaz gráfica

---

## Excepciones — cuándo NO usar terminal

Hay acciones donde forzar el terminal sería contraproducente o simplemente imposible. En esos casos, usa el método más adecuado sin intentar hacerlo por CLI:

- **Instalaciones que requieren GUI** — instaladores con asistente visual, apps de escritorio, etc.
- **Subir archivos a plataformas web** — Google Drive, Dropbox, portales de clientes; requieren el navegador
- **Insertar API keys o credenciales en interfaces visuales** — paneles de configuración de servicios externos
- **Acciones que requieren interacción humana directa** — formularios, flujos de autenticación OAuth en navegador
- **El usuario pide explícitamente otro método** — si el usuario dice "hazlo con Python" o "abre la interfaz", se respeta

---

## Cómo comunicarlo

Antes de ejecutar, menciona brevemente qué comando usarás. No hace falta justificar por qué elegiste terminal — solo muestra lo que vas a hacer:

> "Voy a usar `find . -name '*.log' -mtime +7 -delete` para limpiar los logs."

> "Instalo la dependencia con `pip install pandas --break-system-packages`."

Mantén la comunicación corta. Si el comando es obvio, no hace falta ni mencionarlo.

---

## Árbol de decisión

```
¿Hay más de una forma de hacer esta tarea?
│
├── NO → Usa el único método disponible
│
└── SÍ → ¿Es terminal una opción viable Y práctica?
          │
          ├── SÍ → Usa terminal (este skill)
          │
          └── NO → ¿Por qué no es práctica?
                    ├── Requiere GUI/browser/interacción visual → usa esa alternativa
                    ├── El usuario pidió otro método → respeta su preferencia
                    └── Terminal sería mucho más compleja sin beneficio → usa la alternativa más simple
```

---

## Ejemplos

**✅ Usar terminal:**

| Tarea | Método preferido |
|---|---|
| Renombrar 50 archivos | `for f in *.txt; do mv "$f" "${f%.txt}.md"; done` |
| Buscar texto en archivos | `grep -r "búsqueda" ./carpeta/` |
| Convertir CSV a JSON | `python -c "import csv,json,sys; ..."` o `jq` |
| Crear estructura de carpetas | `mkdir -p proyecto/{src,tests,docs}` |
| Instalar paquete Python | `pip install requests --break-system-packages` |
| Copiar/mover archivos | `cp`, `mv`, `rsync` |
| Ver contenido de un archivo | `cat`, `head`, `tail`, `less` |
| Comprimir archivos | `zip`, `tar` |

**❌ No forzar terminal:**

| Tarea | Por qué no usar terminal |
|---|---|
| Subir archivo a Google Drive | Requiere autenticación en browser |
| Instalar aplicación de escritorio | Tiene instalador GUI |
| Pegar API key en panel de Stripe | Es una acción en interfaz web |
| Autenticarse con OAuth | Flujo requiere browser |

---

## Resumen

| Situación | Acción |
|---|---|
| Hay alternativa y terminal es práctica | Terminal primero |
| Solo existe un método | Usa ese método |
| Requiere GUI/browser/interacción visual | Usa la alternativa, sin forzar CLI |
| Usuario pide otro método | Respeta la preferencia |
| Terminal sería desproporcionadamente compleja | Usa la alternativa más simple |
