# `04` Injection - Cross-site scripting (XSS) Reflected GET and POST

### **Cross-Site Scripting (XSS) Reflected (GET)**

1. Selecciona la vulnerabilidad **Cross-Site Scripting (XSS) Reflected (GET)**.
2. En la página que se abre, verás un formulario que solicita First name y Last name. Introduce cualquier valor en ambos campos, por ejemplo:

```bash
First name: Test
Last name: User
```

![imagen 6](../../.learn/assets/testget.png)

3. Al enviar el formulario, verás que los valores ingresados se muestran como un mensaje en la página y también se incluyen en la URL como parámetros GET. Algo similar a esto:

```bash
http://localhost/bWAPP/xss_get.php?firstname=Test&lastname=User
```
![imagen 7](../../.learn/assets/urltest.png)

### **Inyectar el Script XSS en el Formulario** 

1. En lugar de valores regulares, ingresa el siguiente script en cualquiera de los campos del formulario para inyectar un ataque XSS:

```bash
First name: <script>alert('XSS con GET')</script>
Last name: User (o cualquier otro valor) form alert get  
```


![imagen 8](../../.learn/assets/alertget.png) 

Al enviar el formulario, el script se ejecutará, mostrando una alerta con el mensaje "XSS con GET".

![imagen 9](../../.learn/assets/alertUrlGET.png) 

### **Verificación de la Explotación**
- Confirma los Resultados de la Explotación: Asegúrate de que la página muestra la alerta correctamente, confirmando que la inyección de XSS ha sido exitosa.

> Observa que en GET los datos ingresados son visibles en la URL, lo que hace que este método sea más fácil de explotar y compartir, pero también más evidente.


## **Cross-Site Scripting (XSS) Reflected (POST)**

1. Selecciona la vulnerabilidad **Cross-Site Scripting (XSS) Reflected (POST)**.
2. En la página que se abre, verás un formulario que solicita First name y Last name. Introduce el siguiente script en cualquiera de los campos del formulario para inyectar un ataque XSS

```bash
First name: <script>alert('XSS con POST')</script>
Last name: User (o cualquier otro valor)
```

![imagen 11](../../.learn/assets/formXssPost.png)

Al enviar el formulario, el script se ejecutará, mostrando una alerta con el mensaje "XSS con POST".

![imagen 12](../../.learn/assets/xssPostAlert.png)


### **Verificación de la Explotación**
- A diferencia del método GET, aquí no verás los parámetros en la URL, ya que se envían en el cuerpo de la solicitud POST.
- Verifica que la alerta se muestre en la página, confirmando que la inyección de XSS ha sido exitosa.

#### 💡 Sobre GET y POST en XSS:
- **GET**: Los datos se muestran en la URL, lo que lo hace más fácil de explotar y compartir, pero más visible.
- **POST**: Los datos se envían en el cuerpo de la solicitud, lo que hace que el ataque sea menos visible, pero más complicado de ejecutar y compartir sin interacción del usuario.

**Ambos métodos permiten ejecutar scripts maliciosos en el navegador de la víctima si la página no sanitiza adecuadamente las entradas, pero cada uno tiene sus particularidades en cuanto a la explotación y visibilidad.**








