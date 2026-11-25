# Mini CRM

Laboratorio para ver, en vivo, cómo un asistente de IA construye el mismo producto de dos maneras: **vibe coding** y **spec-driven development**.

En esta rama no hay aplicación. El público parte de las especificaciones y del prompt, y el código se escribe durante la sesión con Cursor o GitHub Copilot.

El producto es un CRM mínimo: un tablero Kanban para seguir conversaciones de venta, editar cada lead y pedir una sugerencia corta del siguiente paso. La interfaz queda en inglés, como la escriben las especificaciones.

## Las dos prácticas

Hazlas en carpetas distintas. Así se puede comparar el resultado sin mezclar decisiones.

### 1. Vibe coding

Abre un directorio vacío en Cursor o GitHub Copilot. No abras este repositorio y no adjuntes `spec-driven-development/`. Pega el contenido de `vibe-coding/prompt.md`, o usa este prompt:

```text
Constrúyeme una aplicación sencilla de mini CRM.

Quiero hacer seguimiento de leads de ventas en un tablero Kanban con columnas como New, Contacted, Proposal, Won y Lost.

Debe haber un botón para agregar un lead nuevo. Cada lead debe tener nombre, empresa, email, estado y notas.

Debe tener una función de IA que sugiera la siguiente acción de seguimiento de un lead a partir de las notas.
```

Deja que el asistente elija stack, estructura y comportamiento. Si el resultado se queda corto, sigue con frases sueltas, por ejemplo: "ahora guárdalo en una base de datos" o "haz que la sugerencia no falle si no hay API key".

### 2. Spec-driven development

Abre este repositorio. Las especificaciones son la fuente de verdad. Pide una feature por vez, en este orden:

1. `spec-driven-development/features/feature_01_lead_crud.md`
2. `spec-driven-development/features/feature_02_kanban_pipeline.md`
3. `spec-driven-development/features/feature_03_lead_detail_modal.md`
4. `spec-driven-development/features/feature_04_ai_followup_suggestion.md`

Antes de cada feature, el asistente debe leer `product.md` y `tech.md`. En Cursor, `AGENTS.md` ya lo indica. En GitHub Copilot, `.github/copilot-instructions.md` hace lo mismo.

Prompts de ejemplo:

```text
Lee spec-driven-development/product.md, spec-driven-development/tech.md y spec-driven-development/features/feature_01_lead_crud.md. Implementa solo esa feature. Respeta el stack, el esquema de Prisma y las rutas de tech.md. No agregues nada de la sección Non-Goals.
```

```text
Implementa spec-driven-development/features/feature_02_kanban_pipeline.md. Cinco columnas fijas, sin drag and drop. Al guardar un cambio de estado, la tarjeta debe moverse de columna de inmediato. Rechaza estados que no estén en la spec.
```

```text
Implementa spec-driven-development/features/feature_03_lead_detail_modal.md. Al hacer clic en una tarjeta se abre el modal con nombre, empresa, email, estado, notas, sugerencia, createdAt y updatedAt. Guardar llama a PATCH /api/leads/:id. Cancelar cierra sin guardar. Muestra los errores de validación.
```

```text
Implementa spec-driven-development/features/feature_04_ai_followup_suggestion.md. El botón debe decir "Suggest follow-up". Envía nombre, empresa, estado y notas. Guarda el resultado en aiSuggestedNextAction. Si falta OPENAI_API_KEY, si la llamada falla o si hay timeout, usa exactamente el texto de respaldo de tech.md y no dejes que la app falle.
```

## Cómo comparar

Al terminar las dos carpetas, mira lo mismo en ambas:

- ¿El stack se mantiene o cambia de idea entre iteraciones?
- ¿Los leads siguen ahí después de refrescar la página?
- ¿Nombre y empresa son obligatorios y el email solo exige `@`?
- ¿Un estado inválido se rechaza con un mensaje claro?
- ¿La sugerencia se guarda y se ve en la tarjeta y en el detalle?
- ¿La app arranca y sugiere un seguimiento sin `OPENAI_API_KEY`?

## Solución de referencia

La rama `solucion-sdd` tiene una implementación completa que sigue estas especificaciones. No la abras durante el ejercicio. Sirve después, para contrastar lo que construyó el asistente en vivo.

```bash
git fetch origin
git checkout solucion-sdd
```

## Estructura de esta rama

```text
/
├── README.md
├── AGENTS.md
├── .github/copilot-instructions.md
├── .gitignore
├── spec-driven-development/
│   ├── product.md
│   ├── tech.md
│   └── features/
│       ├── feature_01_lead_crud.md
│       ├── feature_02_kanban_pipeline.md
│       ├── feature_03_lead_detail_modal.md
│       └── feature_04_ai_followup_suggestion.md
└── vibe-coding/
    └── prompt.md
```
