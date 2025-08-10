# Visual Studio Code
Visual Studio Code es un editor de código gratuito que funciona en los sistemas operativos macOS, Linux y Windows. Su instalación es rápida y sencilla, permitiéndote comenzar a trabajar en minutos.

VS Code es ligero y debería funcionar en la mayoría de los equipos y versiones de plataformas disponibles. Puedes revisar los [Requisitos del sistema](https://code.visualstudio.com/docs/supporting/requirements) para verificar si tu configuración de computadora es compatible.

## Configuración de VS Code para tu plataforma

**Descargar e instalar Visual Studio Code para tu plataforma**

   - [macOS](https://code.visualstudio.com/docs/setup/mac)
   - [Linux](https://code.visualstudio.com/docs/setup/linux)
   - [Windows](https://code.visualstudio.com/docs/setup/windows)
  

> Nota: VS Code publica nuevas versiones mensualmente y admite actualizaciones automáticas cuando una nueva versión está disponible.

**Instalar extensiones de VS Code desde el Marketplace de Visual Studio**

   Personaliza VS Code con temas, formateadores, extensiones de lenguaje y depuradores para tus lenguajes favoritos, entre otros.


## Visual Studio en Debian

Completa los siguientes pasos para instalar Visual Studio Code en tu sistema Debian.

1. Empieza por actualizar el índice de paquetes e instalar las dependencias escribiendo:

```bash
apt update
apt install software-properties-common apt-transport-https curl
```
2. Importa la clave GPG de Microsoft usando el siguiente comando `curl`:

```bash
curl -sSL https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
```
3. Añade el repositorio de Visual Studio Code a tu sistema:

```bash
add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
```
4. Después de agregar el repositorio, instala la última versión de Visual Studio Code:

```bash
apt update
apt install code
```

¡Eso es todo!

Visual Studio Code ha sido instalado en tu escritorio Debian y ya puedes comenzar a usarlo.

## Próximos pasos

Una vez que hayas instalado VS Code, estos temas te ayudarán a aprender más sobre él:

- [Tutorial de VS Code](https://code.visualstudio.com/docs/getstarted/keybindings): Un recorrido práctico por las características clave de VS Code.
- [Consejos y trucos](https://code.visualstudio.com/docs/getstarted/keybindings): Una colección de consejos de productividad para trabajar con VS Code.
- [Codificación asistida por IA](https://code.visualstudio.com/docs/getstarted/keybindings): Aprende a usar GitHub Copilot en VS Code para ayudarte a escribir código más rápido.


## 📝 Actividad
!!! Question "Instala vscode"
    1. Haz una instalación de vscode.  



