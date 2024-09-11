# `08` Cryptographic Failures - Weak Password Hashing. 
Hashing Débil de Contraseñas


Una implementación débil de hashing de contraseñas representa una vulnerabilidad critica de **fallos criptográficos**, ya que en lugar de almacenar las contraseñas en texto plano, estas deben ser hasheadas (convertidas a un valor no reversible mediante un algoritmo criptográfico) antes de ser almacenadas en una base de datos. Sin embargo, si se utilizan algoritmos de hash débiles o inadecuados, como MD5 o SHA-1 (que ya no son seguros), los atacantes pueden crackearlos fácilmente usando técnicas como ataques de diccionario o fuerza bruta.

A través de este ejercicio identificaremos la vulnerabilidad con SQL Injection para obtener hashes de contraseñas desde la base de datos y explotaremos la vulnerabilidad de fallas criptográficas crackeando los hashes a través de la utilización de herramientas como **John the Ripper**. Posteriormente iniciaremos sesión con las contraseñas obtenidas para demostrar la vulnerabilidad.


### Obtención de hashes de contraseñas

1. Selecciona la vulnerabilidad **SQL Injection (GET/Search)** y "Hack".
2. Tal como lo hicimos en el ejercicio de [sql injection](../03-injection-sqlinjection/README.es.md) explora el formulario vulnerable. Verás un formulario con un campo para ingresar una búsqueda (generalmente llamado `title` o `id`).

3. Apoyandonos en lo aprendido en el ejercicio [sql injection](../03-injection-sqlinjection/README.es.md) introduce un payload para obtener el nombre del usuario actual:

```bash
http://<tu_ip>/bWAPP/sqli_1.php?title=test' UNION SELECT 1, 2, user(), 4, 5, 6, 7-- &action=search
```
Si obtienes como resultado el nombre de usuario, la aplicación es vulnerable.

4. Extraer hashes de contraseñas. Usa una inyección SQL avanzada para extraer los datos sensibles (nombres de usuario, contraseñas) como lo hicimos en [sql injection](../03-injection-sqlinjection/README.es.md)

> 💡 Pista: Los nombres de los usuarios estan guardados en la columna `login` toma esto en cuenta para cuando quieras obtener el nombre de usuario.


### Crackear los hashes

1. Crea un archivo llamado `hash.txt` con el siguiente formato (ajusta el formato según el hash que hayas obtenido):

```bash 
bee:202cb962ac59075b964b07152d234b70
```
- bee es el nombre de usuario.
- 202cb962ac59075b964b07152d234b70 es el hash de una contraseña.

2. Utiliza **John the Ripper** para crackear el hash. Ejecuta el siguiente comando en tu terminal, posicionado en la carpeta donde creaste el archivo:

```bash
john --format=raw-sha1 hash.txt
```
> 💡 Puedes instalar **John the Ripper** en la maquina de beebox pero puede llegar a tener algunas complicaciones y vas  perder mucho tiempo en su instalación, por el contrario podrias usar kali linux para hacer el crakeo ya que tiene la herramienta **John the Ripper** instalada por defecto, elige tu camino sabiamente.


3. Revisa los resultados. Si John el Ripper crackea el hash correctamente, verás algo como:

![imagen 1](../../.learn/assets/hash-craked.png)


### Inicia sesión a bWAPP con la contraseña crackeada

1. Ve al formulario de inicio de sesión en bWAPP.
2. Ingresa el nombre de usuario y la contraseña crackeada (por ejemplo, bee y 123).
3. Verifica si puedes acceder a la cuenta del usuario con las credenciales obtenidas.



> ⚠ Mitigar los problemas relacionados con Weak Password Hashing es crucial porque un atacante que logre acceder a la base de datos de contraseñas podría obtener el control total de las cuentas de los usuarios.

Si lograste los resultados esperados, ¡felicitaciones! ve a la siguiente leccion `-->`





<!-- En bWAPP, la categoría de Security Logging and Monitoring Failures no tiene una lección específica directamente etiquetada con ese nombre. Sin embargo, hay algunas prácticas comunes que se pueden adaptar para simular y explorar fallos en el registro y monitoreo de seguridad. Aquí tienes una forma de abordar esto con los recursos disponibles en bWAPP:

Ejercicio Intermedio: Simulación de Fallos en Logging y Monitoreo
Objetivo:
Explorar cómo la falta de logging y monitoreo puede afectar la seguridad de una aplicación y cómo un atacante podría aprovechar estas fallas para realizar ataques sin ser detectado.

Pasos del Ejercicio:
Inicia sesión en bWAPP:

Accede a bWAPP desde tu navegador utilizando la dirección IP de la máquina virtual BeeBox.
Inicia sesión con las credenciales:
Usuario: bee
Contraseña: bug
Selecciona un Ejercicio Relacionado con Input Malicioso:

En bWAPP, elige una lección que permita introducir datos maliciosos, como SQL Injection, XSS, o incluso un ejercicio de Remote File Inclusion (RFI). Por ejemplo, selecciona "SQL Injection (GET/Select)" si está disponible.
Realiza un Ataque y Observa la Respuesta:

Introduce una carga maliciosa para probar la vulnerabilidad. Por ejemplo:
SQL Injection: Prueba inyecciones SQL que podrían ser utilizadas para acceder o modificar datos sensibles.
XSS: Inyecta scripts para observar si hay algún tipo de registro de actividad maliciosa.
Verifica la Falta de Monitoreo:

Intenta realizar el ataque y luego revisa si hay alguna manera de verificar si la actividad maliciosa ha sido registrada. En entornos reales, deberías buscar archivos de registro o paneles de monitoreo para detectar la actividad.
En bWAPP, verifica si hay una sección de logs en la aplicación o en el servidor para determinar si el ataque ha sido registrado. En muchos casos, bWAPP no tiene funcionalidades de logging visibles, por lo que debes considerar esto como una limitación.
Simula un Ataque Persistente:

Realiza múltiples intentos de ataque para simular un ataque persistente o un intento de explotación. Esto ayudará a evidenciar la falta de monitoreo en una aplicación que no tiene registros adecuados.
Documenta tus Hallazgos:

Anota cualquier evidencia de falta de logging y monitoreo que hayas encontrado.
Describe cómo la ausencia de estos mecanismos puede facilitar ataques continuos sin detección y cómo mejorar la seguridad mediante la implementación de prácticas adecuadas de logging y monitoreo.
Implementa Medidas de Mitigación:

Discute y documenta cómo las prácticas adecuadas de logging y monitoreo pueden ayudar a identificar y mitigar ataques. Esto puede incluir la configuración de sistemas de logging adecuados, la revisión periódica de los registros y el establecimiento de alertas para actividades sospechosas.
Explicación del Ataque:
Este ejercicio ilustra cómo la falta de un sistema adecuado de logging y monitoreo puede permitir a un atacante explotar vulnerabilidades en una aplicación sin ser detectado. Al simular ataques y observar la ausencia de registros, se puede entender la importancia de mantener registros detallados y monitorear continuamente las actividades en una aplicación para mejorar la seguridad.

Este enfoque adaptado te permitirá explorar el impacto de los fallos en logging y monitoreo en un entorno controlado como bWAPP. Si tienes alguna otra pregunta o necesitas más detalles, ¡no dudes en pedirlo! -->
