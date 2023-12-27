# SustiDesarrollo
Parte 1

Previamente ejecutando todos los comandos para inizializar el proyecto se verifica cucumber es así que nuestro proyecto queda así

![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/ddd97dc4-e0bf-4af3-997b-fdfbec3a7162)

Con los escenarios fallidos

![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/491150b3-6675-413d-bbfa-1864efe93bf3)

Cobertura de codigo 
El index.html nos muestra un informde nuestras pruebas en general
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/3b5697d2-3964-4860-a5fa-cc4229fc9663)

Pregunta 1
-migracion 
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/19f8d808-1e7f-41e7-bdf9-90e492271d79)

Se modifican las vistas
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/e8b08fed-bc87-4624-8afc-e501a6660a9b)

![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/76a96b46-daa4-4422-932b-a30a3a0a16f4)

![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/d39230fd-3b1a-4160-b94b-735d46013d4b)

Para encontrar las definiciones nos vamos al feature que nos muestra los escenarios 
Algunos pasos se cumplen al crear la columna de director, sin embargo, muchos más no lo hacen
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/127adf9f-50cc-443d-8df9-724155f7e7fd)

Además si necesitamos que se comprende humano computador, configuramos /support/paths.rb así 
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/0ebdb867-d65c-4eb3-8c28-70ee166d38be)

Finamelmente tenemos que modificar 
def movie_params
    params.require(:movie).permit(:title, :rating, :description, :release_date, :director)
  end
Sino al crear o editar alguna pelicula no lo permitiría


Parte 2: Ruby on Rails
Pregunta 1 (1 punto)
¿Por qué la abstracción de un objeto de formulario pertenece a la capa de presentación y no a la capa
de servicios (o inferior)?
La abstracción de un objeto de formulario pertenece a la capa de presentación porque está directamente relacionada con la interfaz de usuario y la entrada de datos. La capa de presentación maneja la interacción del usuario y la representación visual de la aplicación. 
En contraste, la capa de servicios o capas inferiores se centran en la lógica de negocio y en la manipulación de datos, pero no están directamente involucradas en la presentación de la interfaz de usuario.
Pregunta 2 (1 punto)
¿Cuál es la diferencia entre autenticación y autorización?
La autenticación se refiere al proceso de verificar la identidad de un usuario, asegurando que la persona o entidad que está intentando acceder a un sistema o recurso es quien dice ser. En cambio, la autorización se centra en determinar qué acciones o recursos específicos tiene permitido realizar un usuario autenticado. En resumen, la autenticación se ocupa de la identidad, mientras que la autorización se ocupa de los permisos y los accesos

Pregunta 3
Se aprecian los diferentes middlewares
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/faa2abed-950b-4278-a5e5-54d695b38cf1)

Con la ayuda de la gema trace_location podemos realizar el track de procesos en nuestra aplicación es así que podemos:
Realizar seguimiento al ciclo de vida de la aplicación 
1.
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/b38a511e-a7d8-46b3-aee5-6054a38ba906)

y usamos 

TraceLocation.trace do
  status, headers, body = Rails.application.call(env)
end

nos genera un archivo .md donde vemos como trackea cada variables de entorno cada path cada script, valida archivos, etc

![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/d1ee9eae-4fda-4ce9-9628-8f69612cd26b)

2. Podemos trackear la creación de una instancia de objeto
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/26bf9e7f-037e-44d7-b1dd-5b050f29cd27)

![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/aaa32bde-41c6-4714-b79b-7c480da93e5e)

Podemos ver como realiza las validaciones y la persistencia

Pregunta4 
1. Uso de git log --format=oneline -- app/models/user.rb | wc -l
-Nos permite buscar un archivo subido mediante git
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/a9b0cb69-31d4-4cd9-ad56-0278c777f302)

2. Usando flog para calcular la complejidad
-Flog nos dará el calculo del churn que es una medida de cambio de nuestros archivos, que nos reflejará en cierta medida si se modifica mucho
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/c2e44248-c3a4-46f1-8c0b-6648d75f0976)

3. One liner que busca complejidad

find app/models -name "*.rb" | while read file; do echo -n "$file "; git log --format=oneline -- "$file" | wc -l; done | sort -k 2 -nr | head -n 10 | cut -d ' ' -f 1 | xargs -I {} sh -c 'echo -n "{} "; flog -s "{}" | grep -o "flog: [0-9.]*"'

Ese one liner me permite obtener los 10 con más complejidad con la ayuda de sort -k 2 -nr y xargs -I {} sh -c 'echo -n "{} "; flog -s "{}" | grep -o "flog: [0-9.]* me permite obtener el nombre y la complejidad correspondiente
En mi caso en la ruta app/models solo tengo un modelo llamado movie.rb por eso me da esto 
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/06eb3d6f-8730-42df-82c3-b2f30139d3b2)

Usando attractor 
La gema attractor nos permite tener una interfaz interactiva para visualizar los diferentes archivos con sus respectivas complejidades
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/b020e192-e842-4cc0-a50b-9b4a55b286b8)


Parte 3

**Pregunta 1**
El codigo permite modificar y borrar una cookie, que al inicio tiene valor nil
<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestión de Cookies</title>
</head>

<body>

    <script>
        function getCookie(name) {
            const cookies = document.cookie.split(';');
            for (const cookie of cookies) {
                const [cookieName, cookieValue] = cookie.trim().split('=');
                if (cookieName === name) {
                    return decodeURIComponent(cookieValue);
                }
            }
            return null;
        }

        function setCookie(name, value, days) {
            const expirationDate = new Date();
            expirationDate.setTime(expirationDate.getTime() + (days * 24 * 60 * 60 * 1000));
            const expires = `expires=${expirationDate.toUTCString()}`;
            document.cookie = `${name}=${encodeURIComponent(value)}; ${expires}; path=/`;
        }

        function deleteCookie(name) {
            document.cookie = `${name}=; expires=Thu, 01 Jan 2022 00:00:00 UTC; path=/;`;
        }

        console.log("Valor inicial de document.cookie:", document.cookie);

        setCookie('galleta', 'Registro 1', 1);
        console.log("Valor de la cookie: ", getCookie('galleta'));

        deleteCookie('galleta');
        console.log("Luego de eliminar galleta:", document.cookie);
    </script>

</body>

</html>
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/afd40339-3ce7-4996-b623-bf122ee123f0)


**Pregunta 2**
el archivo html quedería así
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Curso CC-3S2</title>
  <style>
    .hide {
      display: none;
    }
    .error {
      color: red;
      font-size: 0.8em;
      font-family: sans-serif;
      font-style: italic;
    }
    input {
      border-color: #ddd;
      width: 400px;
      display: block;
      font-size: 1.5em;
    }
  </style>
</head>
<body>

<form name="myform">
  Email: <input type="text" name="email"> <span class="error hide" id="emailError"></span><br>
  Password: <input type="password" name="password"> <span class="error hide" id="passwordError"></span><br>
  User Name: <input type="text" name="userName"> <span class="error hide" id="userNameError"></span><br>
  <input type="submit" value="Registrar" id="submitBtn">
</form>

<script>
  //Obtenemos los elementos del hmtl
  const form = document.forms.myform;
  const emailInput = form.elements.email;
  const passwordInput = form.elements.password;
  const userNameInput = form.elements.userName;
  const emailError = document.getElementById('emailError');
  const passwordError = document.getElementById('passwordError');
  const userNameError = document.getElementById('userNameError');
  const submitBtn = document.getElementById('submitBtn');

  // Utilizamos listeners para ocultar los errores
  form.addEventListener('submit', function (event) {    
    emailError.classList.add('hide');
    passwordError.classList.add('hide');
    userNameError.classList.add('hide');

  //Procedemos a validar el correo y posteriormente el password
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(emailInput.value)) {
      handleValidationError(emailError, 'Caracteres especiales no validos.');
      event.preventDefault();
      return;
    }
    const passwordRegex = /^[a-zA-Z0-9]{3,8}$/;
    if (!passwordRegex.test(passwordInput.value)) {
      handleValidationError(passwordError, 'Ingrese caracteres entre 3-8 y solo caracteres alfanumericos');
      event.preventDefault();
      return;
    }

    //Se crea el formulario y  se obtiene el valor, además de agregar una validación
    const formData = {};
    for (const input of form.elements) {
      if (input.type !== 'submit') {
        formData[input.name] = input.value;
      }
    }
    if (!hasErrors()) {
      console.log('Form data:', formData);
    } else {
      event.preventDefault();
    }
  });

  //Creación de funciones que manejan errores y modifican el comportamiento
  function handleValidationError(errorElement, errorMessage) {
    errorElement.textContent = errorMessage;
    errorElement.classList.remove('hide');
  }
  function hasErrors() {
    return !emailError.classList.contains('hide') || !passwordError.classList.contains('hide') || !userNameError.classList.contains('hide');
  }
</script>

</body>
</html>

Error cuando se exceden los limites
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/1d05b9b1-2ac1-4d7d-a8c0-d67e922aa0b3)

Error cuando falta @
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/1b0257be-6b50-42d5-9afc-c5ad10019714)


**Pregunta 3**
con las validaciones tenemos 
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/910a8d2a-e3a8-4ba1-8970-115e808cb2b2)

![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/e8a38680-ab4d-4bf0-bee8-294ef811507d)

![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/bd0ded1d-cd7f-45f1-983f-def47b015de5)

Así conseguimos que se eviten llenar campos vacios y con caracteres no permitidos usando las validaciones del modelo

**Pregunta 4**
Pregunta: ¿Dónde podemos obtener una instancia real de la clase Movie para utilizar en dicha prueba?

    Podemos obtener una instancia real de la clase Movie mediante el uso de factories o fixtures. Las factories pueden generar instancias dinámicamente, mientras que las fixtures proporcionan instancias predefinidas. En el contexto de las pruebas, las fixtures son comúnmente almacenadas en archivos YAML y se encuentran en la carpeta spec/fixtures.

Pregunta: ¿Qué hacen los siguientes códigos entregados y dónde se ubican? ¿Por qué hay que tener cuidado en su uso?

    Los códigos entregados consisten en un archivo YAML (movies.yml) y un archivo de pruebas en Ruby (movie_spec.rb). Estos archivos se ubican en la carpeta spec del proyecto. En el archivo YAML se definen instancias de Movie que se utilizan como fixtures en las pruebas. Al usar fixtures, debemos tener cuidado porque estas instancias pueden no cumplir con todas las restricciones o validaciones de nuestro modelo. Además, su mantenimiento manual puede llevar a fixtures desactualizadas o inconsistentes.

Pros y contras del uso de factories o fixtures en las pruebas:

Pros:

    Factories:
        Dinámicas y flexibles, permiten la creación de instancias con datos específicos para cada prueba.
        Facilitan la generación de datos válidos y coherentes.
    Fixtures:
        Proporcionan instancias predefinidas, lo que puede ser útil para ciertos escenarios de prueba.

Contras:

    Factories:
        Pueden requerir más código y configuración.
    Fixtures:
        Mantenimiento manual, pueden desactualizarse fácilmente.
        Menos flexibles para datos específicos en pruebas particulares.
  
Parte 4
    Crear la clase TennisScorer y ejecutar la primera especificación:





