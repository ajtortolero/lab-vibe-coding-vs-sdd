# Instrucciones para el asistente

Este repositorio es el punto de partida de un laboratorio. Todavía no hay aplicación. Constrúyela a partir de las especificaciones, una feature por vez.

Las especificaciones son la fuente de verdad:

- `spec-driven-development/product.md`
- `spec-driven-development/tech.md`
- `spec-driven-development/features/feature_01_lead_crud.md`
- `spec-driven-development/features/feature_02_kanban_pipeline.md`
- `spec-driven-development/features/feature_03_lead_detail_modal.md`
- `spec-driven-development/features/feature_04_ai_followup_suggestion.md`

Orden de trabajo:

1. Lee `product.md` y `tech.md`.
2. Implementa solo la feature que te pidan. Empieza por la 01 si todavía no hay código.
3. No adelantes la feature siguiente.
4. No copies la rama `solucion-sdd`. Esa rama es la solución de referencia y no forma parte del ejercicio.

Reglas:

- Implementa solo lo que piden las specs. Si una feature no menciona un cambio, no lo hagas de paso.
- No agregues los non-goals de `product.md`: autenticación, varios usuarios, pagos, integraciones, envío de email, calendario, drag and drop, permisos avanzados, línea de tiempo ni carga de archivos.
- Usa el stack y la estructura de carpetas de `tech.md`: Next.js, TypeScript, React, Tailwind, SQLite, Prisma y la API de OpenAI.
- La base de datos local es `database/dev.db`. En el esquema, la URL de SQLite tiene que resolver a ese archivo. Prisma resuelve las rutas desde `prisma/`, así que `file:../database/dev.db` apunta a `database/dev.db`.
- Valida en el servidor. Nombre y empresa son obligatorios. Si hay email, debe contener `@`. El estado solo puede ser New, Contacted, Proposal, Won o Lost. Un lead nuevo queda en New.
- Si falta `OPENAI_API_KEY`, si la llamada falla o si hay timeout, guarda exactamente: `Follow up with this lead, reference the latest notes, and ask for a clear next step.` La app no debe fallar por la IA.
- La sugerencia tiene menos de 40 palabras y usa nombre, empresa, estado y notas.
- Los textos de la interfaz se quedan en inglés, como están escritos en las specs.
- Los errores de la API y de la UI deben entenderse sin leer el código.
- Prefiere cambios pequeños y legibles. No introduzcas Redux ni capas extra.
