# `01` Broken Access Control - Insecure DOR (Change Secret)

**Broken Access Control** son vulnerabilidades en las aplicaciones web que ocurre cuando los controles que restringen el acceso a recursos o funcionalidades no están implementados correctamente. Esto permite a los atacantes eludir las restricciones de acceso, lo que les da la capacidad de ver, modificar o interactuar con datos o funcionalidades a los que no deberían tener acceso. Para este ejercicio intentaremos explotar el hack **Insecure DOR**, para intentar modificar el valor del parámetro de usuario en la solicitud para cambiar el secreto de otra cuenta.


### **Crear un nuevo usuario**

1. Inicia la máquina virtual beebox.
2. Accede a la interfaz web de bWAPP desde tu navegador usando la dirección IP de la máquina beebox.
3. **Crea un nuevo usuario**:
    - Crea un usuario llamado geeks con el secret: secret test.
    ![imagen 1](../../.learn/assets/usergeeks.png)
4. Inicia sesión en bWAPP:

```bash
    - Usuario: bee
    - Contraseña: bug
```

### **Verificación en MySQL**

1. Abre la terminal en la VM Beebox.
2. Accede a MySQL usando el siguiente comando:

```bash
mysql -u root -p
```
> 💡 La contraseña predeterminada: `bug`

3. Selecciona la base de datos de bWAPP:

```sql
USE bWAPP;
```
4. Verifica que el usuario `geeks` y su "secret" hayan sido creados:

```sql
SELECT * FROM users;
```
   
![imagen 2](../../.learn/assets/mysqlsecrettest.png)


### **Modificación del secreto de otro usuario**


1. Vuelve a iniciar sesión como el usuario predeterminado `bee`.
2. Selecciona la vulnerabilidad **Insecure DOR (Change Secret)** y "Hack".

![imagen 3](../../.learn/assets/hack.png)


3. Inspeccionar el Formulario HTML.

- Una vez en la página de cambio de "secret", haz clic derecho en el campo donde se ingresa el nuevo "secret" y selecciona "Inspeccionar" (o usa las herramientas de desarrollo del navegador).

![imagen 4](../../.learn/assets/htmlbeeuser.png)

4. Modificar el Valor del Formulario.

- En el código HTML inspeccionado, localiza el valor del campo oculto (input) que contiene el valor "bee".
- Cambia este valor por "geeks" para que, al enviar el formulario, se modifique el "secret" del usuario geeks en lugar del usuario bee.

![imagen 5](../../.learn/assets/htmlvalue.png)

5. Enviar el Formulario:

- Cambia el "secret" a hello geeks en el formulario, y envíalo.

### Comprobación en la Base de Datos:

1. Vuelve a la terminal de MySQL.
2. Verifica que el "secret" del usuario geeks haya sido modificado:

```bash
SELECT * FROM users;
```

> Deberías ver que el "secret" ha cambiado a hello geeks.

![imagen 6](../../.learn/assets/secretgeeks.png)



