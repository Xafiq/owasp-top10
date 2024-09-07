# `05` Security Misconfiguration - Local File Inclusion (LFI)

1. Selecciona la vulnerabilidad **Remote & Local File Inclusion (RFI/LFI)** para la actividad guiada y haz clic en "Hack".

> ⚠ Es posible que encuentres **Remote & Local File Inclusion (RFI/LFI)** listado en Missing Functional level access control ya que la vulnerabilidad Remote & Local File Inclusion (RFI/LFI) puede aparecer en múltiples categorías de seguridad según el contexto en el que se analice. Aunque es más común clasificarla como parte de Security Misconfiguration, en algunos casos puede estar listada bajo categorías como Missing Function Level Access Control, como lo ha hecho bWAPP.

2. En la página de LFI, verás una URL que incluye un parámetro para seleccionar un archivo, por ejemplo:

```bash
http://<tu_ip>/bWAPP/rlfi.php?language=lan_en.php&action=go
```

![imagen 1](../../.learn/assets/home-hack.png)

> 💡Observa que el parámetro language probablemente está siendo usado para incluir un archivo de idioma en la página.


3. Modifica el parámetro `language` para intentar incluir un archivo del sistema. Por ejemplo:

```bash
http://<tu_ip>/bWAPP/rlfi.php?language=../../../../etc/passwd&action=go
```
Cuando estás realizando un ataque de Local File Inclusion (LFI), el objetivo es incluir archivos que están almacenados en el servidor (donde está alojado la página que quieres atacar). En este caso, intentaremos acceder al archivo `/etc/passwd`, que es un archivo común en servidores Linux y que contienen información sobre los usuarios del sistema. Al modificar el parámetro `language`, estás tratando de incluir un archivo del servidor donde se ejecuta bWAPP. En este caso, cuando colocas `../../../../etc/passwd` en la URL, el navegador envía esa solicitud al servidor, y si la vulnerabilidad de LFI existe, el servidor incluye el contenido del archivo `/etc/passwd` y te lo muestra en la página web.

![imagen 2](../../.learn/assets/passwd-access-vulnerability.png)


## Exploración Adicional de vulnerabilidades

Una vez confirmado el LFI, explora otros archivos sensibles del sistema. Algunos ejemplos incluyen:

- Nombre del servidor de bWAPP:

```bash
http://<tu_ip>/bWAPP/rlfi.php?language=../../../../etc/hostname&action=go
```

- Configuración principal de Apache.:

```bash
http://<tu_ip>/bWAPP/rlfi.php?language=../../../../etc/apache2/apache2.conf&action=go
```

