#  Añadir **acción de ventana** y **menús** para `task_model` (sin vistas aún)

En este paso vamos a **abrir el modelo desde la UI** creando:
- una **acción de ventana** (`ir.actions.act_window`) que apunte a `task_model`, y
- dos **menús** (uno raíz y otro hijo) que disparen esa acción.

> **Nota:** No definiremos todavía vistas `<list>` ni `<form>`. Odoo es capaz de **generar vistas básicas por defecto** cuando no existen vistas específicas para un modelo. En el siguiente paso crearemos nuestras vistas personalizadas.

---

## Prerrequisitos
- Módulo `task_app` instalado o visible en *Apps*.
- Modelo del paso anterior creado e importado:
  - Modelo: **`task_model`** con campos `name`, `description`, `is_done`.

Estructura mínima:
```
task_app/
├─ __init__.py
├─ __manifest__.py
├─ models/
│  ├─ __init__.py
│  └─ task_model.py
└─ views/
```

Crea la carpeta `views/` si no existe.

---

## Crear menús

Archivo: **`task_app/views/task_menus_action.xml`**

```xml
<odoo>
  <!-- Acción de ventana: abre el modelo task_app.task_model -->
  <record id="action_task_model" model="ir.actions.act_window">
    <field name="name">Tasks</field>
    <field name="res_model">task_app.task_model</field>
    <!-- Importante en Odoo 18: usar list/form (no tree) -->
    <field name="view_mode">list,form</field>
    <!-- Opcional: ayuda cuando no hay registros aún -->
    <field name="help" type="html">
      <p class="o_view_nocontent_smiling_face">
        Crea tu primera tarea
      </p>
    </field>
  </record>

  <!-- Menú raíz de la app (puedes renombrar a tu gusto) -->
  <menuitem id="menu_task_root" name="Task App" sequence="10"/>

  <!-- Menú que dispara la acción -->
  <menuitem id="menu_task_model"
            name="Tasks"
            parent="menu_task_root"
            action="action_task_model"
            sequence="10"/>
</odoo>
```

> *Consejo:* usa IDs claros y estables (`action_task_model`, `menu_task_root`, `menu_task_model`) para facilitar futuras herencias/extensiones.

---

## Añadir el XML al `__manifest__.py`

Edita **`task_app/__manifest__.py`** y añade el archivo en la clave `data` (mantén primero seguridad cuando la tengas):

```python
"data": [
    # "security/ir.model.access.csv",   # (lo añadiremos en un paso posterior)
    "views/task_menus_actions.xml",
],
```

> Si ya tenías `data: []`, simplemente inserta la ruta tal cual. Evita listar ficheros que **no existan**.

---

## Actualizar el módulo

### Opción A — Interfaz
1. **Ajustes → Activar Modo desarrollador**.
2. **Apps → Actualizar lista de aplicaciones**.
3. **Actualizar** (o **Instalar**) el módulo `task_app`.

### Opción B — Docker (CLI)
Con contenedores `web` (Odoo) y `db` (PostgreSQL), ejecuta:

```bash
docker exec -it odoo18_web_1 sh -lc '
  odoo \
    --db_host=db \
    --db_port=5432 \
    --db_user=odoo \
    --db_password="$(cat /run/secrets/postgresql_password)" \
    --addons-path=/usr/lib/python3/dist-packages/odoo/addons,/mnt/extra-addons \
    -d odoodb -u task_app --stop-after-init
'
```

> Usa `--stop-after-init` para evitar el error “Port 8069 in use” si el servidor ya está activo en el contenedor.

---

## Verificar desde la UI

1. Abre **Task App → Tasks** (el menú que acabamos de crear).
2. Deberías poder entrar y ver una **lista generada por defecto** (Odoo 18) y, al abrir un registro, un **formulario básico**.
3. Si no ves el menú:
   - Comprueba que el módulo está **actualizado** sin errores.
   - Activa Modo desarrollador y revisa en **Ajustes → Técnico → Acciones de Ventana** que existe **`action_task_model`** (res_model = `task_model`).
   - Revisa en **Ajustes → Técnico → Menús** que existen **`menu_task_root`** y **`menu_task_model`**.

> **Permisos:** si no eres *Administrador*, podrías necesitar accesos en `security/ir.model.access.csv` para que los usuarios internos creen/lean tareas. Lo añadiremos más adelante.

---

## 📝 Actividad
!!! Question "Crear menús"
    1. Crea un menú para acceder al modelo task_model