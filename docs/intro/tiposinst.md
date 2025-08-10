## Tipos de licencias

Actualmente hay un gran número de aplicaciones que pueden ser utilizadas por las empresas. Todas ellas llevan un determinado tipo de licencia. Por otra parte, han proliferado un gran número de tipos de licencias de software. En consecuencia, tenemos que poder reconocer la licencia que acompaña a cada software y cuáles son sus implicaciones.

**IMPORTANTE**

Según indica la Real Academia Española, una licencia es una "autorización que se concede para explotar con fines industriales o comerciales una patente, marca o derecho". En el caso del software, una licencia permite el uso con el consentimiento del autor e implica una serie de derechos y deberes.

A causa de que los derechos y deberes que los autores pueden asignar a sus obras son de varios tipos, han aparecido gran número de tipos de licencias que, básicamente, podemos clasificar en dos grandes grupos:

- **Software privativo**
- **Software libre**

El **software libre** (*free software*) es aquel que permite al usuario el uso total del producto adquirido. El **software privativo** es aquel que no lo es.

## A. El software libre en el mercado de los ERP

El software privativo ha sido generado y gestionado por grandes empresas (proveedores). Se paga por las licencias de uso, los costes de implantación, la adaptación del ERP a la empresa y las actualizaciones/correcciones/errores. Esto se garantiza mediante un contrato de mantenimiento (económicamente elevado), que garantiza al cliente la reparación de errores en el software y las actualizaciones periódicas.

El software libre, por el contrario, implica la implementación anual por el usuario; o bien contratando o colaborando por las horas trabajadas. No se paga licencia y para las actualizaciones no hay una garantía como tal; sino que la comunidad desarrolladora repara el error o actualiza la versión en un plazo no determinado. El usuario es el encargado de estar atento si quiere tener el sistema actualizado.

**Ventajas del software libre:**

- Software y actualizaciones gratis.
- Gran cantidad de información de fácil acceso en foros y comunidades de usuarios.
- Gran cantidad de aplicaciones ERP.

### Algunos ejemplos

**Openbravo**

Es una iniciativa de origen español. Aunque Openbravo se considere como software libre, su modelo de negocio incluye:

- Parte abierta
- Parte de módulos de pago
- Otros licenciados con licencia **OBPL** (*Openbravo Public License*)
- El resto de módulos tienen licencia **OBCL** (*Openbravo Commercial License*), y para ser instalados se debe realizar el pago de una suscripción.

**Odoo**

De origen Belga, se caracteriza por tener una amplia variedad de módulos. Presenta dos versiones: *Odoo Community* [código abierto] y *Odoo Enterprise* [con licencia]. 

## Pasos previos a la instalación

Aunque depende del sistema operativo y del tipo de instalación elegida, las tareas para instalar y configurar el ERP son, en resumen, las siguientes:

- **Diseñar la instalación**: antes de instalar, debemos realizar un estudio de las necesidades de la empresa y plantear cómo las va a resolver la aplicación ERP: tablas que necesitamos adaptar, datos, formularios e informes necesarios, etc.
- **Instalación de equipos**: es imprescindible la instalación, revisión y/o actualización del hardware de la empresa donde se va a instalar, de manera que se cumplan los requisitos mínimos necesarios. Algunas veces, la empresa puede decidir contratar los servicios externos y acceder así a los recursos remotos.
- **Instalación del software**: además del ERP, deberemos instalar todo aquel software necesario para el correcto funcionamiento del sistema.
- **Adaptar y configurar el programa**: una vez instalada la aplicación, debemos configurar y adaptar el software a la empresa cliente.
- **Migrar los datos**: este es uno de los pasos más importantes ya que los datos de la empresa son necesarios para su correcto funcionamiento; debemos migrar datos de clientes y proveedores; la contabilidad; facturación; etc.
- **Realizar pruebas**: habrá que realizar pruebas para comprobar que el ERP funciona correctamente y que los resultados son satisfactorios.
- **Documentar el sistema**: se deben crear manuales y documentar todos los procesos realizados.
- **Formar a los usuarios**: se debe formar a los usuarios para que utilicen el ERP; normalmente se realiza una formación inicial para responsables del proyecto y otra para usuarios finales.

## Tipos de instalación

El tipo de instalación del ERP/CRM dependerá de la plataforma en la que lo instalemos y del ERP que vayamos a utilizar. Los más habituales son los siguientes:

### Tipos de instalación ERP/CRM

**Instalación mediante máquina virtual**

Tanto la aplicación como todos los programas necesarios para el funcionamiento del ERP se proporcionan en una máquina virtual que está lista para ser ejecutada. Esta opción no es apta para un entorno en producción y normalmente se utiliza para hacer una primera evaluación del producto.

**Instalación de paquetes en entorno gráfico**

En este caso utilizamos el entorno gráfico del sistema operativo para instalar la aplicación y hacemos uso de los asistentes que instalan y resuelven las dependencias entre los paquetes. Normalmente este tipo de instalación se suele utilizar en entornos de producción.

**Instalación personalizada**

Para instalar una versión más reciente de la aplicación, podemos descargarnos los paquetes fuente desde la página web que los contenga, e instalar el ERP mediante comandos. Esta opción permite controlar los programas que instalaremos y sus dependencias, aunque suele ser un proceso más complejo que la instalación en entorno gráfico.

**No instalar o acceder a la aplicación en línea**

Algunos ERP permiten acceder a demostraciones online de sus productos; de esta forma no instalamos nada, nos conectamos a un servidor de Internet que ya tiene todos los datos de la aplicación. Normalmente esta opción la utilizan los proveedores de ERP que ofrecen el servicio SaaS.

### Tipos de instalación Odoo

**Instalación mediante máquina virtual**  
Simplemente pondremos en funcionamiento una imagen de Odoo sobre *una máquina virtual* o sobre *Docker*.

**Instalación de paquetes en entorno gráfico**  
Utilizamos el entorno gráfico del sistema operativo para instalar la aplicación y hacemos uso de los asistentes que instalan y resuelven las dependencias entre los paquetes.  
Podemos utilizar cualquier sistema operativo, libre o con licencia. Para los usuarios no expertos, podríamos utilizar un sistema Windows actual y seguir los pasos de la instalación. Este tipo de instalación no requiere muchos conocimientos previos.  
Podemos descargar Odoo desde su página web. Encontrarás el link en la sección *Enlaces de descarga* de esta unidad.

**Instalación personalizada**  
Este es el tipo de instalación que utilizaremos. Nos centraremos en la preparación y posterior instalación paso a paso.

**No instalar o acceder a la aplicación en línea**  
Para tener una idea rápida de Odoo, hay instancias de demostración disponibles. Son instancias compartidas que solo viven unas pocas horas y que se pueden usar para navegar y probar cosas sin compromiso.  
Las instancias de demostración no requieren instalación local, solo un navegador web.  
El SaaS debe ir acompañado con una instancia privada e ilimitada pero gratis.  
Se puede usar para descubrir y probar las aplicaciones personalizadas sin código (es decir, incompatible con módulos personalizados o con la Tienda de aplicaciones de Odoo) y sin tener que instalarlo localmente.  
Puede usarse tanto para prueba como para uso profesional a largo plazo.  
Tal y como pasa en las instancias demo de demostración, las instancias SaaS tampoco requieren instalación local.  
Tenemos acceso a ella en la sección *trial*, en la web de Odoo.

---

## Formas de trabajar

Los ERP pueden trabajar de dos maneras:

- Desde uno o varios ordenadores en red mediante una aplicación web con un navegador para conectar el ERP (como Odoo).
- Desde un servidor de la empresa al que se puede acceder a través de Internet o desde una intranet (solo desde cualquier terminal interno).

Debemos indicar en cada caso al servidor al que nos vamos a conectar. Hay dos opciones:

**Monousuario**  
La base de datos y la aplicación están alojadas en el mismo equipo, adyacente a sí mismo directamente.  
En este caso nos conectamos directamente indicando `localhost`, refiriéndonos al equipo donde tenemos instalado nuestro ERP.
