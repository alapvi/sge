# Creación de un modelo

Vamos a ver de manera detallada **cómo crear un modelo en Odoo 18** . 

---

## Estructura previa del módulo

Suponemos que ya tienes un módulo visible en Odoo con el manifest mínimo. La estructura debería incluir al menos:

```
task_app/
├─ __init__.py
├─ __manifest__.py
└─ models/
   └─ __init__.py
```

Si no existe `models/` o alguno de los `__init__`, créalos ahora (vacíos).

---

## Código del modelo

Ruta del archivo: `task_app/models/task_model.py`

```python
# task_app/models/task_model.py
from odoo import fields, models

class TaskModel(models.Model):
    _name = "task_app.task_model"
    _description = "Task (basic model)"

    name = fields.Char(string="Name", required=True, index=True)
    description = fields.Text(string="Description")
    is_done = fields.Boolean(string="Done", default=False)
```

---

## Explicación detallada

### Importaciones
- `from odoo import fields, models`  
  Importa el **ORM** de Odoo. `models.Model` es la clase base para todos los modelos, y `fields` contiene los tipos de campos disponibles (Char, Text, Boolean, Many2one, etc.).

### Definición de la clase
- `class TaskModel(models.Model):`  
  Declara una **clase de modelo** que hereda de `models.Model`. El nombre de la clase en Python (p. ej., `TaskModel`) puede ser cualquiera, pero por convención se usa **CamelCase** y describe la entidad.

### Metadatos del modelo
- `_name = "task_app.task_model"`  
  Es el **nombre técnico** del modelo (también llamado *model name*).  
  - Suele incluir el **prefijo del módulo** (`task_app`) para evitar colisiones con otros módulos.  
  - Este nombre se usa en vistas XML, reglas de acceso, dominios, etc.
- `_description = "Task (basic model)"`  
  Cadena legible que describe el modelo. Se utiliza en la interfaz para etiquetas y títulos.

### Campos del modelo
- `name = fields.Char(...)`  
  Campo de **texto corto**.  
  - `string="Name"` etiqueta visible en la UI.  
  - `required=True` obliga a que tenga valor antes de crear/guardar el registro.  
  - `index=True` crea un índice en BD para búsquedas más rápidas por este campo.
- `description = fields.Text(...)`  
  Campo de **texto largo** (sin límite práctico a nivel de ORM). Ideal para descripciones.
- `is_done = fields.Boolean(...)`  
  Campo **booleano**.  
  - `default=False` define el valor por defecto al crear registros.

> **Sugerencia:** Si no especificas `_rec_name`, Odoo usa por defecto el campo `name` para representar el registro (por ejemplo, en desplegables Many2one).

---

## Notas mínimas para que Odoo cargue el modelo
- Asegúrate de importar el archivo en `task_app/models/__init__.py` (por ejemplo: `from . import task_model`).  
- Incluye el módulo en tu base de datos y actualízalo desde Apps o con `-u task_app` si trabajas desde la línea de comandos.


Basado en la referencia oficial del ORM de Odoo 18:  
- Documentación ORM (fields): https://www.odoo.com/documentation/18.0/developer/reference/backend/orm.html#fields

---

## Campos básicos 

### `Char`
- **Texto corto**. Útil para nombres, códigos, títulos.
- Atributos típicos: `size` (límite de longitud), `index`, `required`.
```python
code = fields.Char(string="Código", size=32, index=True, required=True)
```

### `Text`
- **Texto largo** sin límite práctico (almacenado como `text` en PostgreSQL).
```python
description = fields.Text(string="Descripción")
```

### `Boolean`
- **Verdadero / Falso**.
```python
is_done = fields.Boolean(string="Realizada", default=False)
```

### `Integer`
- **Entero** (32 bits).
```python
priority = fields.Integer(string="Prioridad", default=0)
```

### `Float`
- **Número decimal**.
- Atributo `digits` para control de precisión.
```python
weight = fields.Float(string="Peso (kg)", digits=(16, 2))
```

### `Monetary`
- **Decimal** asociado a una **moneda** (`currency_field`).
```python
currency_id = fields.Many2one("res.currency", string="Moneda")
amount = fields.Monetary(string="Importe", currency_field="currency_id", digits=(16, 2))
```

### `Date`
- **Fecha** sin hora.
```python
deadline = fields.Date(string="Fecha límite")
```

### `Datetime`
- **Fecha y hora** (timezone-aware a nivel de UI).
```python
scheduled_at = fields.Datetime(string="Programada")
```

### `Selection`
- Valor **enumerado** entre opciones cerradas.
- Puedes usar `selection=[(...), ...]` o `selection=_method`.
```python
state = fields.Selection(
    [
        ("draft", "Borrador"),
        ("progress", "En progreso"),
        ("done", "Hecho"),
        ("cancel", "Cancelado"),
    ],
    string="Estado",
    default="draft",
    index=True,
)
```

### `Binary`
- **Binario** (archivos). Suele usarse con `attachment=True` para almacenar en adjuntos.
```python
file_data = fields.Binary(string="Adjunto", attachment=True)
```

### `Html`
- **HTML enriquecido** (editor WYSIWYG).
```python
notes_html = fields.Html(string="Notas")
```

### `Image`
- Imagen almacenada en binario con utilidades de **redimensionado**.
```python
image = fields.Image(string="Imagen", max_width=512, max_height=512)
```

---

## 2) Campos relacionales

### `Many2one`
- Relación **muchas a una** hacia otro modelo (crea columna `<campo>_id`).
- Atributos clave: `comodel_name`, `ondelete`, `domain`, `context`, `index`.
```python
partner_id = fields.Many2one(
    "res.partner",
    string="Contacto",
    ondelete="set null",
    index=True,
    domain=[("active", "=", True)],
)
```

### `One2many`
- Relación **una a muchas** (virtual), inversa a un `Many2one` en el modelo destino.
- Requiere `comodel_name` y `inverse_name` (el `Many2one` que apunta a este modelo).
```python
line_ids = fields.One2many(
    "task.line",
    "task_id",          # inverse_name en el modelo task.line
    string="Líneas"
)
```

### `Many2many`
- Relación **muchas a muchas** usando una tabla relacional.
- Se puede especificar tabla/columnas o dejar que Odoo las genere.
```python
tag_ids = fields.Many2many(
    "task.tag",
    "task_tag_rel",     # nombre de la tabla relacional (opcional)
    "task_id",          # columna que referencia a este modelo (opcional)
    "tag_id",           # columna que referencia al comodel (opcional)
    string="Etiquetas",
)
```

---

## 3) Campos computados y relacionados

### Campo **computado** (`compute`)
- El valor se calcula por código. Con `store=True` se guarda en BD (y define dependencias con `@api.depends`).
```python
from odoo import api, fields, models

class Task(models.Model):
    _name = "x.task"

    name = fields.Char(required=True)
    hours = fields.Float()
    rate = fields.Float()
    amount = fields.Float(compute="_compute_amount", store=True)

    @api.depends("hours", "rate")
    def _compute_amount(self):
        for rec in self:
            rec.amount = rec.hours * rec.rate
```

### Campo **relacionado** (`related`)
- Apunta a un campo de otra relación. Opcionalmente `store=True` para almacenar una copia sincronizada.
```python
partner_country = fields.Many2one(
    related="partner_id.country_id",
    comodel_name="res.country",
    string="País (cliente)",
    store=True,
    readonly=True,
)
```

---

## 4) Atributos comunes (cheatsheet)

> No todos aplican a todos los tipos; consulta la doc oficial para detalles y compatibilidades.

- `string="Etiqueta"` → Texto mostrado en la UI.
- `help="Texto de ayuda"` → Tooltip de ayuda.
- `required=True` → Hace obligatorio el campo.
- `default=<valor|función>` → Valor por defecto (literal o función/`lambda`).
- `index=True` → Índice en BD (búsqueda más rápida).
- `copy=True/False` → Se copia al duplicar el registro.
- `readonly=True` → Solo lectura en la UI (no evita cambios por código).
- `states={...}` → Modifica atributos según estado (vistas form).
- `groups="module.group_xmlid"` → Visibilidad/edición restringida a grupos.
- `tracking=True/number` → Rastreo en chatter (si el modelo hereda de `mail.thread`).
- `translate=True` → Traducción (en `Char`, `Text`, `Html`, etc.).
- `size=NN` → Longitud máxima (principalmente `Char`).
- `digits=(precision, escala)` → Precisión en `Float/Monetary`.
- `currency_field="currency_id"` → Campo moneda asociado (`Monetary`).
- `domain=[(...)]` → Filtrado dinámico en relacionales (UI/ORM).
- `context={...}` → Valores por defecto, comportamiento contexto.
- `ondelete="restrict|cascade|set null|set default"` → Política al eliminar (`Many2one`).
- `compute="_method"` → Campo computado; combínalo con `@api.depends`.
- `inverse="_method"` → Acción inversa del compute (cuando procede).
- `search="_method"` → Método de búsqueda personalizada.
- `store=True` → Persistir valor de campo computado/relacionado.
- `compute_sudo=True` → Computar con superusuario (evita problemas de permisos).
- `selection_add=[(...)]` → Extender selecciones existentes.
- `related="x.y.z"` → Campo relacionado.
- `deprecated="18.0"` → Marcar campo como obsoleto (nota para devs).

---

## 5) Campos especiales / reservados más comunes

> Odoo crea o usa estos campos con semántica especial. Conviene conocerlos.

- `name` (`Char`) → **“display name”** por defecto; se muestra como identificador del registro.
- `active` (`Boolean`) → **Archivado**: si `False`, el registro se oculta de listas por defecto.
- `sequence` (`Integer`) → Ordenación preferente en vistas/listas.
- `create_uid` (`Many2one(res.users)`) → Usuario que **creó** el registro.
- `create_date` (`Datetime`) → Fecha/hora de **creación**.
- `write_uid` (`Many2one(res.users)`) → Último usuario que **modificó**.
- `write_date` (`Datetime`) → Fecha/hora de la **última modificación**.
- `company_id` (`Many2one(res.company)`) → Compañía del registro (multiempresa).
- `display_name` (`Char`, compute) → Nombre mostrado (puede combinar varios campos).

**Notas**:
- Los cuatro campos de auditoría (`create_uid`, `create_date`, `write_uid`, `write_date`) se manejan **automáticamente** por el ORM.
- `active` agrega el filtro “Incluir archivados” en la UI cuando existe en el modelo.
- `name_get` / `name_search` permiten personalizar el **display name** y la búsqueda rápida.

---

## 6) Ejemplo compacto de modelo con varios tipos

```python
from odoo import api, fields, models

class Task(models.Model):
    _name = "demo.task"
    _description = "Demo Task"

    # Básicos
    name = fields.Char(required=True, index=True)
    description = fields.Text()
    is_done = fields.Boolean(default=False)
    deadline = fields.Date()
    planned_at = fields.Datetime()

    # Números
    hours = fields.Float(digits=(16, 2))
    currency_id = fields.Many2one("res.currency")
    amount = fields.Monetary(currency_field="currency_id", digits=(16, 2))

    # Media y HTML
    image = fields.Image(max_width=256, max_height=256)
    notes_html = fields.Html()

    # Relacionales
    partner_id = fields.Many2one("res.partner", ondelete="set null", index=True)
    tag_ids = fields.Many2many("demo.tag", string="Etiquetas")

    # Computados y relacionados
    partner_country = fields.Many2one(
        related="partner_id.country_id", store=True, readonly=True
    )

    # Archivado
    active = fields.Boolean(default=True)

    # Computado con depends
    effective = fields.Float(compute="_compute_effective", store=True)

    @api.depends("hours", "is_done")
    def _compute_effective(self):
        for rec in self:
            rec.effective = rec.hours if rec.is_done else 0.0
```

---

## 7) Consejos rápidos
- Define `index=True` en campos usados en dominios/filtros frecuentes.
- Usa `ondelete="set null"` en `Many2one` salvo que necesites bloquear (`restrict`) o arrastrar (`cascade`).
- En `Monetary`, **SIEMPRE** define el `currency_field`.
- En campos computados con `store=True`, no olvides las dependencias con `@api.depends`.
- Para grandes textos, `Text` o `Html`; para pequeñas etiquetas, `Char` con `size`.
- `selection_add` es la forma limpia de extender `Selection` de otro módulo.
