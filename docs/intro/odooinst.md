# Instalación de Odoo

Odoo proporciona [paquetes de instalación](https://www.odoo.com/documentation/18.0/es/administration/on_premise/packages.html) para:

- **Distribuciones Linux basadas en Debian** (Debian, Ubuntu, etc.),
- **Distribuciones Linux basadas en RPM** (Fedora, CentOS, RHEL, etc.),
- Y **Windows**, tanto para las ediciones **Community** como **Enterprise**.

Los paquetes de compilación nocturna de Odoo Community están disponibles en el servidor nocturno con todos los requisitos de dependencias necesarios.

> Es posible que sea complicado mantener los paquetes nocturnos al día.

Los paquetes oficiales de Community y Enterprise se pueden descargar desde [la página de descargas de Odoo](https://www.odoo.com/page/download).

> Para descargar los paquetes de Enterprise es necesario que haya iniciado sesión como un cliente que paga Odoo de forma local o un partner.

## Linux
---

### Preparar

Odoo necesita un servidor **PostgreSQL** para ejecutarse correctamente.

### Debian / Ubuntu

La configuración predeterminada para el paquete `.deb` de Odoo está diseñada para usar el servidor PostgreSQL en el **mismo huésped** que la instancia de Odoo.

Para instalar PostgreSQL, ejecuta:

```bash
sudo apt install postgresql -y
```

### Fedora

(Sigue pasos similares usando `dnf`, si estás en una distribución basada en RPM).

---

> ⚠️ **Advertencia**  
> `wkhtmltopdf` no está instalado mediante `pip` y debe instalarse **manualmente** en la versión **0.12.6** para ser compatible con encabezados y pies de página.  
> Consulta esta [wiki de Odoo sobre wkhtmltopdf](https://github.com/odoo/odoo/wiki/wkhtmltopdf) para más detalles sobre las versiones compatibles.


### Repositorio

Odoo S.A. ofrece un repositorio que te permite instalar la edición Community ejecutando:

```bash
# Para Debian/Ubuntu:
wget -q -O - https://nightly.odoo.com/odoo.key | sudo gpg --dearmor -o /usr/share/keyrings/odoo-archive-keyring.gpg
echo 'deb [signed-by=/usr/share/keyrings/odoo-archive-keyring.gpg] https://nightly.odoo.com/18.0/nightly/deb/ ./' | sudo tee /etc/apt/sources.list.d/odoo.list
sudo apt-get update && sudo apt-get install odoo

# Para Fedora/CentOS/RHEL:
sudo dnf config-manager --add-repo=https://nightly.odoo.com/18.0/nightly/rpm/odoo.repo
sudo dnf install -y odoo
sudo systemctl enable odoo
sudo systemctl start odoo
```

Usa `apt-get upgrade` o su equivalente para mantener el sistema actualizado.

### Paquete de distribución

También puedes descargar paquetes `.deb` o `.rpm` desde la página oficial de Odoo (tanto para Community como para Enterprise).

**Notas sobre `.deb`:**

- Soporta **Debian Bookworm (12)** y **Ubuntu Jammy (22.04 LTS)** o versiones posteriores.
- Para instalar desde la terminal como root:

```bash
dpkg -i <ruta_al_paquete.deb>  # Esto puede fallar por dependencias
apt-get install -f             # Corrige las dependencias faltantes
dpkg -i <ruta_al_paquete.deb>  # Repite la instalación
```

- Si necesitas exportar a formato XLS y estás en Debian anterior (como Buster) u otra versión antigua de Ubuntu:
  - Instala manualmente `xlwt`:

    ```bash
    sudo pip3 install xlwt
    ```

  - Para Odoo con módulos `l10n_mx_edi`, si falta `num2words`, instálalo manualmente:

    ```bash
    sudo pip3 install num2words
    ```

**Notas sobre `.rpm`:**

- Compatible con **Fedora 38**.
- Instalación típica:

```bash
sudo dnf localinstall odoo_18.0.latest.noarch.rpm
sudo systemctl enable odoo
sudo systemctl start odoo
```

## Windows
---

> ⚠️ **Advertencia**: el instalador de Windows es práctico para pruebas o uso local por un solo usuario, pero **no se recomienda para producción** debido a varias limitaciones.

### Pasos básicos:

1. Descarga el instalador desde el servidor *nightly* (solo Community) o desde la página oficial (Community o Enterprise).
2. Ejecuta el archivo descargado.
3. En Windows 8 o superior, podrías ver una alerta de seguridad ("Windows protegió tu PC"). Haz clic en **Más información** y luego en **Ejecutar de todas formas**.
4. Acepta el aviso de control de cuentas de usuario (UAC).
5. Sigue las instrucciones del instalador.
6. Al finalizar, **Odoo se inicia automáticamente**.

## Docker

### Descripción

[Esta imagen oficial de Docker](https://github.com/docker-library/docs/tree/master/odoo) ejecuta [Odoo](https://www.odoo.com/), un sistema ERP modular y extensible. Está preparada para ejecutarse en contenedores Docker, con soporte para despliegues simples o en clúster. 

---
### Uso básico con Docker
Ejemplo de comando para lanzar un contenedor Odoo conectado a un contenedor PostgreSQL:

```bash
docker network create odoo-net

docker run -d --name db --network odoo-net \
  -e POSTGRES_USER=odoo \
  -e POSTGRES_PASSWORD=odoo \
  -e POSTGRES_DB=postgres \
  postgres:15

docker run -d --name odoo --network odoo-net -p 8069:8069 \
  -e HOST=db -e USER=odoo -e PASSWORD=odoo \
  odoo:18.0
```

---

### Uso con Docker Compose

La forma recomendada para producción y desarrollo es usar `docker-compose`.
Ejemplo de archivo `docker-compose.yml` para Odoo 18 con PostgreSQL:

```yaml
services:
  web:
    image: odoo:18.0
    depends_on:
      - db
    ports:
      - "8069:8069"
    volumes:
      - odoo-web-data:/var/lib/odoo
      - ./config:/etc/odoo
      - ./addons:/mnt/extra-addons
    environment:
      - PASSWORD_FILE=/run/secrets/postgresql_password
    secrets:
      - postgresql_password
  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD_FILE=/run/secrets/postgresql_password
      - POSTGRES_USER=odoo
      - PGDATA=/var/lib/postgresql/data/pgdata
    volumes:
      - odoo-db-data:/var/lib/postgresql/data/pgdata
    secrets:
      - postgresql_password
volumes:
  odoo-web-data:
  odoo-db-data:

secrets:
  postgresql_password:
    file: odoo_pg_pass
```

### Explicación rápida:

- `db`: servicio que ejecuta PostgreSQL con datos persistentes en volumen.
- `odoo`: servicio que ejecuta Odoo, que se conecta a PostgreSQL.
- Los puertos 8069 del contenedor Odoo se exponen en el host para acceso web.
- Montar addons personalizados ubicados en `./addons`.
- Usar un archivo de configuración personalizado ubicado en `.config/odoo.conf`.
- Usar volúmenes con nombre para los directorios de datos de Odoo y PostgreSQL.
- Usar un archivo de secrets llamado `odoo_pg_pass` que contiene la contraseña de PostgreSQL compartida por ambos servicios.

### Persistencia de datos y volúmenes

- Los datos de PostgreSQL se guardan en el volumen `odoo-db-data`.
- Los datos y configuraciones de Odoo se guardan en el volumen `odoo-web-data`.

Esto garantiza que la información persista aunque los contenedores se reinicien o eliminen.

## 📝 Actividad
!!! Question "Instalación de Odoo"
    1. Haz una instalación de Odoo utilizando `docker-compose`  
    