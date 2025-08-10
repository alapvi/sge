# 📦 Implantación de un ERP con Odoo

Este documento describe en detalle las fases de un proyecto de implantación de un ERP (Enterprise Resource Planning), tomando como referencia la plataforma **Odoo**. Se incluyen ejemplos prácticos, recomendaciones y buenas prácticas.

---

## 🔍 Estudio del Mercado

### Objetivo
Analizar las soluciones ERP existentes y evaluar cuál se adapta mejor a las necesidades de la empresa.

### Factores a evaluar
- Coste total de propiedad (licencia, mantenimiento, personalización)
- Código abierto vs. propietario
- Escalabilidad
- Comunidad y soporte técnico

### Comparativa básica
| ERP         | Licencia    | Comunidad | Personalización | Coste inicial |
|-------------|-------------|-----------|------------------|----------------|
| Odoo        | Libre (Community) / Comercial (Enterprise) | Alta      | Muy Alta         | Bajo             |
| SAP Business One | Comercial | Alta      | Media            | Alto            |
| Microsoft Dynamics | Comercial | Media     | Alta             | Medio           |

**Ejemplo práctico:** Una PYME con necesidades básicas de contabilidad, CRM y ventas opta por **Odoo Community**, por ser económico y flexible.

---

## ✅ Selección del ERP

### Reunión con stakeholders
Identificar los procesos clave y puntos de dolor actuales.

### Requisitos funcionales y técnicos
- Multiempresa / multiusuario
- Gestión de inventario
- Facturación electrónica
- Integraciones con plataformas externas (por ejemplo, e-commerce)

---

## ⚙️ Fase de Implantación

### Planificación del proyecto
- Asignación de roles: consultor, administrador, usuarios clave
- Calendario de implantación (metodología ágil recomendada)

### Instalación técnica
- Entorno de pruebas y producción (Docker, servidores, nube)
- Base de datos PostgreSQL + Odoo

### Formación inicial
- Sesiones por departamentos (Ventas, Almacén, Administración)
- Manuales básicos de uso de Odoo

**Ejemplo:** Se crea un entorno de pruebas con Odoo y se carga una muestra de clientes y productos.

---

## 🚀 Fase de Puesta en Marcha

### Migración de datos
- Importación de clientes, productos, proveedores, facturas
- Odoo permite importar desde Excel o CSV

### Validación de procesos
- Validación de ventas: cotización > pedido > albarán > factura
- Validación de almacén: entrada > ubicación > salida

### Soporte post-lanzamiento
- Resolución de errores y ajustes de configuración
- Monitorización de logs y rendimiento

**Ejemplo:** Se detecta que los albaranes no se generan correctamente y se ajusta el flujo de entrega en Odoo.

---

## 🔚 Cierre del Proyecto

### Documentación
- Manual de uso por departamentos
- Documentación técnica: configuración, módulos instalados

### Evaluación
- Encuesta de satisfacción a usuarios
- Informe de lecciones aprendidas

**Ejemplo:** El cliente solicita incluir KPIs de ventas semanales y se incorpora un dashboard con Odoo Studio.

---

## 🧩 Selección de Módulos según Necesidades

| Departamento | Módulo Odoo         | Funcionalidad principal                    |
|--------------|---------------------|--------------------------------------------|
| Ventas       | `sale_management`   | Presupuestos, pedidos, clientes             |
| Compras      | `purchase`          | Órdenes de compra, proveedores              |
| Almacén      | `stock`             | Control de inventario y ubicaciones         |
| Contabilidad | `account`           | Facturación, asientos, impuestos            |
| CRM          | `crm`               | Gestión de oportunidades y clientes         |
| Recursos Humanos | `hr`            | Empleados, ausencias, nóminas               |
| Fabricación  | `mrp`               | Órdenes de fabricación, rutas, listas materiales |

**Ejemplo:** Una empresa sin fabricación activa puede prescindir del módulo `mrp` inicialmente.

---

## 🛠️ Configuración y Personalización del ERP

### Creación de empresa y usuarios
- Configurar multicompañía si es necesario
- Asignación de roles: gerente, usuario, contable

### Personalización visual
- Logos, plantillas de facturas y presupuestos
- Traducción de interfaz al español

### Personalización funcional
- Crear campos personalizados con Odoo Studio
- Automatización de flujos con reglas y acciones programadas

### Desarrollo personalizado (avanzado)
- Crear nuevos módulos con `odoo scaffold`
- Modificar vistas, modelos y controladores

```bash
docker exec -it odoo odoo scaffold gestion_eventos /mnt/extra-addons
```

**Ejemplo:** Se desarrolla un módulo a medida para gestionar eventos internos de la empresa con inscripción de empleados.

---

## 📘  Actividad
!!! Question "Implantación de Odoo"
    📘 Actividad 1: Análisis y planificación de implantación de Odoo en una empresa ficticia.

    **Objetivo**: Simular un proyecto real de implantación de Odoo, desde el análisis de necesidades hasta la propuesta de módulos y personalizaciones.

    **Instrucciones**:

    1. En grupos de 3-4 personas, diseñad una empresa ficticia con al menos:
        - Nombre
        - Sector de actividad (ej. comercio electrónico, logística, fabricación, servicios, etc.)
        - Número de empleados
        - Procesos clave a digitalizar
        - Elaborad un documento que contenga:
        - Análisis de necesidades
        - Selección justificada de módulos de Odoo (mínimo 4)
        - Propuesta de calendario de implantación (fases)
    1. Presentad la propuesta en clase con apoyo visual (diapositivas, mural o infografía).