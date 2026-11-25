# Instrucciones para GitHub Copilot

Este repositorio todavía no tiene la aplicación. Es el punto de partida de un laboratorio. Las especificaciones son la fuente de verdad. Léelas antes de proponer código:

- `spec-driven-development/product.md`
- `spec-driven-development/tech.md`
- `spec-driven-development/features/feature_01_lead_crud.md`
- `spec-driven-development/features/feature_02_kanban_pipeline.md`
- `spec-driven-development/features/feature_03_lead_detail_modal.md`
- `spec-driven-development/features/feature_04_ai_followup_suggestion.md`

Construye de a una feature. Si el proyecto está vacío, empieza por `feature_01_lead_crud.md`. No implementes la feature siguiente hasta que te la pidan.

No leas ni copies la rama `solucion-sdd`. Es una solución de referencia para después del ejercicio.

Al escribir Mini CRM:

- Sigue el stack de `tech.md`: Next.js, TypeScript, React, Tailwind CSS, SQLite, Prisma y OpenAI.
- Crea las rutas `GET/POST /api/leads`, `PATCH /api/leads/:id` y `POST /api/leads/:id/suggest-follow-up` cuando la feature correspondiente lo pida.
- No agregues autenticación, drag and drop, envío de email, permisos, pagos ni integraciones. Están fuera de alcance en `product.md`.
- Nombre y empresa son obligatorios. El email, si viene, solo debe contener `@`. El estado inicial es `New`.
- Si no hay `OPENAI_API_KEY`, si OpenAI falla o si la llamada expira, usa este texto y guárdalo en `aiSuggestedNextAction`: `Follow up with this lead, reference the latest notes, and ask for a clear next step.`
- No dejes que un fallo de IA tumbe la request ni la interfaz. Muestra un error legible solo cuando también falle el respaldo, por ejemplo si la base de datos no puede guardar.
- Mantén los textos de la UI en inglés.
- SQLite vive en `database/dev.db`. Prisma resuelve la ruta desde `prisma/`, así que usa `file:../database/dev.db`.
