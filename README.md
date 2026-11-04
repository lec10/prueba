# Resumen diario de noticias

Una Routine de Claude Code que corre todos los días a la mañana (hora de Argentina) y hace esto:

1. Busca en Gmail los **newsletters no leídos** de los remitentes de `config/remitentes.txt`.
2. Extrae las noticias, **junta las repetidas** y elige las **5 más relevantes**.
3. Las **traduce al español** (título y resumen de 2-3 líneas, con el link original).
4. Te manda un **mail HTML** con el resumen a la dirección configurada.
5. Recién después de confirmar el envío, **marca como leídos** los newsletters procesados.

Si algo falla (por ejemplo, el conector no puede enviar), no marca nada como leído y te avisa con una notificación.

## Estructura

| Archivo | Para qué sirve |
|---|---|
| `config/remitentes.txt` | Lista de newsletters, una dirección o `@dominio` por línea. **Completalo.** |
| `config/ajustes.md` | Destinatario, cantidad de noticias, asunto, zona horaria, etc. |
| `prompts/resumen-noticias.md` | Las instrucciones que sigue la rutina en cada corrida. |
| `templates/email.html` | La plantilla del mail (HTML con estilos inline, compatible con Gmail). |

Para cambiar cómo funciona la rutina, editá estos archivos en la rama que usa la Routine. No hace falta tocar la Routine.

## La Routine

- Nombre: **Resumen diario de noticias**
- Horario: todos los días a las 06:36 (America/Argentina/Buenos_Aires)
- Conector: Gmail (claude.ai)
- Cada corrida abre una sesión nueva con este repo y ejecuta `prompts/resumen-noticias.md`.

La podés pausar, editar o correr a mano desde claude.ai → Code → Routines.

## Limitación conocida

La rutina depende de que el conector Gmail de claude.ai permita **enviar** mails y **marcar como leído**. Si alguna de las dos no está disponible, la corrida termina sin tocar la bandeja de entrada y explica qué falta.
