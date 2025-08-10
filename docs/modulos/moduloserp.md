# Módulos de un ERP

Las funciones de un ERP vienen definidas en los distintos módulos que podemos instalar.

> Un módulo es un software que contiene los elementos y datos necesarios para añadir alguna funcionalidad a la aplicación.

Distinguimos diferentes tipos de módulos:

- **Módulos adicionales**  
  Se instalan después (desde el mismo programa ERP o desde la web del ERP).

- **Módulo base**  
  Se carga automáticamente desde la instalación inicial del sistema.

Entre las características más importantes de los módulos funcionales de un ERP destacaremos las siguientes:

!!! info "Características de los ERPs"
    - Instalación y desinstalación mediante asistentes.
    - Poder configurar o parametrizar los módulos para que se puedan adaptar al entorno de producción.
    - Incorporar niveles de seguridad: por ello algunos módulos solo estarán accesibles para el administrador
    - Los módulos están interconectados y así la información que se introduce se comparte entre ellos, - evitando introducirla más de una vez. 
    - Posibilita la inclusión de comentarios y otros textos en las opciones de la aplicación que implementa.
    - Los menús generados por los módulos se pueden adaptar a las necesidades de los diferentes usuarios.

---

## Tipología, descripción e interconexionado

### A. Módulo Base

Hay un módulo o conjunto de módulos base que son necesarios para que funcione la aplicación. Tenemos un elemento base y alrededor del mismo podemos establecer otros tipos de módulos adicionales, pero estos no se instalan con la aplicación, solo se instalan si son necesarios para el funcionamiento o la empresa.

**Funciones del módulo base:**
- Nos permite configurar la aplicación.
- Permite la gestión de los datos maestros. Estos datos son los elementos básicos para que funcione el ERP.
- Permite establecer un idioma como predeterminado o importar traducciones.
- Permite establecer la seguridad con la gestión de usuarios y los accesos a la aplicación.
- Permite administrar otros módulos. Podemos instalar nuevos módulos o eliminarlos de la aplicación.

En nuestro caso, el módulo base de **Odoo** solo incorpora dos módulos:  
- **Empresas** (que es una Ficha de Cliente)  
- **Administración**, que permite añadir más funcionalidades a la aplicación con la instalación de nuevos módulos.

---

### B. Gestión contable y financiera

El módulo de Contabilidad automatiza todas aquellas operaciones que están relacionadas con los procesos contables de la empresa, permitiendo así tener todos estos datos centralizados.

La contabilidad financiera se relaciona con los módulos de **Compras** y **Ventas**, para evitar duplicidad en la información.  
De esta manera podemos emitir facturas a clientes o de proveedores sin necesidad de introducir los datos dos veces.

El módulo de Contabilidad debe relacionarse también con el módulo de **Tesorería** para mantener un control sobre el estado financiero global de la empresa.  
Por ejemplo, si un cliente no ha pagado una factura dentro del plazo establecido, se puede bloquear su cuenta hasta que este pago sea realizado.

**Funciones más interesantes:**
- La modularidad y flexibilidad es muy interesante, ya que los ERP disponen de módulos de contabilidad adaptados al Plan General Contable del país donde se implante.
- Permite el idioma e introducción del plan del país donde se implante.

**Contabilidad analítica / módulos:**
- Gestión de impuestos
- Presupuestos
- Facturas de clientes y proveedores
- Estados financieros (Cuentas, balances, sumas y saldos)

---

### C. Compras, ventas y almacén

El módulo de **Compras** trata todas aquellas operaciones relacionadas con el proceso de compra: presupuestos de proveedores, precios, creación de pedidos de compra, etc.

**Características del Módulo Compras:**

- Seguimiento de tarifas de proveedores
- Gestión de entregas parciales del proveedor
- Gestión de reclamaciones a proveedores
- Generación automática de borradores de pedidos de compra

Igual que se realiza una gestión de compras, también hace falta una **gestión de las ventas** de la compañía.  
La forma de trabajar es similar al módulo de Compras, con la diferencia de que nos referimos a documentos de venta.  
Entre sus funcionalidades destacan las siguientes:

---

**Características del Módulo Ventas:**

- Creación de pedidos de venta.
- Revisión de los pedidos en sus diferentes estados.
- Confirmación del envío.
- Definir formas de pago: contado, transferencia, etc., diferenciando estas por pedido y por fecha de facturación.
- Gestionar y calcular todos los gastos generados por el envío de los pedidos.
- Albaranes automáticos desde pedidos.
- Un pedido equivale a un albarán. El pedido puede dividirse en partes, cada una con su albarán parcial (se desglosa y se unifica en la factura).

---

**Características del Módulo Almacén:**

**Características del módulo:**

- Definición de múltiples almacenes.
- Control del stock y la rotación de inventario.
- Traspasos entre almacenes.
- Codificación y numeración de productos de forma personalizada.
- Definición de compras de un producto a diferentes proveedores.

---

### D. Módulo de Facturación

**Funcionalidades del módulo:**

- Configuración de formas de pago: contado, transferencia, etc., diferenciadas por pedido y fecha de facturación.
- Facturas automáticas desde pedidos o albaranes.
- Generación automática desde el cobro o pago.
- Gestión de recibos, órdenes de pago y transferencias.
- Integración con extractos bancarios.
- Envío telemático de datos de remesas al banco.

---

### E. Módulo de Gestión Personal

Este módulo se encarga de todas las gestiones relacionadas con los trabajadores:

- Realización de nóminas.
- Altas y bajas de contratos.
- Control de horarios y días festivos.
- Gestión del sistema de remuneraciones.
- Pago a empleados, incluyendo comisiones por ventas realizadas en un periodo de tiempo.

**Funcionalidades del módulo de Gestión de Personal**

- Gestión de empleados y calendario de vacaciones.
- Gestión de contratos de empleados.
- Gestión de beneficios.
- Gestión de ausencias.
- Gestión de producción y rendimiento.
- Gestión de perfiles y responsabilidades.

Cada uno de estos módulos puede ser ampliado con la instalación de módulos adicionales.  
En ocasiones, la aplicación no dispone de un módulo de RRHH como tal, de forma que la gestión del personal se lleva a cabo introduciendo conceptos contables relacionados, y la gestión de las comisiones se realiza a través del módulo Comercial.

---

### F. Relaciones con clientes

**CRM** (*Customer Relationship Management*, o *Gestión de las relaciones con los clientes*) es una aplicación que permite centralizar en una única base todas las interacciones entre la empresa y sus clientes.

El CRM recopila toda la información de las gestiones comerciales con los clientes, manteniendo un histórico detallado.  
De esta forma, el CRM dispone de gran conocimiento sobre cada cliente y posibilita entender sus necesidades y anticiparse a ellas.

Por otra parte, el CRM permite dirigir y gestionar de forma sencilla las campañas de captación y fidelización de clientes, controlando el conjunto de acciones realizadas sobre los actuales y potenciales, para poder realizar acciones concretas dirigidas al cliente adecuado en el momento adecuado.

Las empresas que utilizan CRM disponen de la información necesaria para ofrecer un servicio de atención al cliente diferenciado, acorde a las necesidades y expectativas actuales del mercado.

**Ejemplo:**  
Openbravo incluye funcionalidad CRM dentro de los módulos de Ventas y Facturación, pero puede integrarse en otro ERP de modo independiente, como **SugarCRM**.

Los sistemas ERP pueden incluir funcionalidades con todas las características del CRM, pero para poder desarrollar nuevos módulos es necesario adaptarse a nuevas tendencias y acceder a la instalación del CRM.

---

**Funcionalidades del módulo CRM**

- Datos identificativos del contacto.
- Segmentación de contactos en función de múltiples criterios.
- Determinación del ciclo de clientes reales y potenciales.
- Seguimiento de oportunidades de negocio.
- Registro de actividades comerciales realizadas en la interacción cliente-empresa:
  - Planificación y ejecución de campañas de marketing.
  - Seguimiento de resultados comerciales.
  - Sincronización con la fuerza de ventas.

Incluye herramientas de análisis para determinar qué documentos enviar en cada momento (ofertas, presupuestos), mensajes SMS, estadísticas diversas, etc.


## 📝 Actividad
!!! Question "Instalación de Odoo"
    1. Investiga los diferentes módulos de Odoo que hemos visto y dónde encontramos.
    2. ¿Hay algún otro módulo?