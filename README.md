# SustiDesarrollo

Parte 2: Ruby on Rails
Pregunta 1 (1 punto)
¿Por qué la abstracción de un objeto de formulario pertenece a la capa de presentación y no a la capa
de servicios (o inferior)?
    Separación de Responsabilidades:
    La arquitectura de software suele seguir el principio de separación de responsabilidades para mejorar la modularidad y la mantenibilidad del código. La capa de presentación se centra en la representación y manipulación de la interfaz de usuario, mientras que las capas inferiores (como la capa de servicios) se centran en la lógica de negocios y la manipulación de datos. Separar estas responsabilidades facilita el desarrollo y la comprensión del código.

    Reutilización de Componentes de Interfaz de Usuario:
    La abstracción de un objeto de formulario generalmente está estrechamente relacionada con la interfaz de usuario y su interacción con el usuario. Al mantener esta abstracción en la capa de presentación, puedes reutilizar fácilmente componentes de interfaz de usuario en diferentes partes de tu aplicación o incluso en diferentes aplicaciones sin depender de la lógica de negocios subyacente.

    Adaptación a Diversas Interfaces de Usuario:
    Diferentes plataformas y tecnologías pueden tener diferentes requisitos y convenciones para la representación de formularios. Mantener la abstracción en la capa de presentación permite adaptarse fácilmente a estas variaciones sin afectar la lógica de negocios subyacente. Por ejemplo, un formulario puede representarse de manera diferente en una aplicación web que en una aplicación móvil.

    Facilita las Pruebas Unitarias:
    La capa de presentación, al centrarse en la representación de la interfaz de usuario, facilita las pruebas unitarias. Puedes realizar pruebas de forma más efectiva sobre la presentación y la interacción del usuario sin depender de la capa de servicios o de la capa de acceso a datos.

    Escalabilidad y Cambios en la Interfaz de Usuario:
    Los cambios en la interfaz de usuario son comunes y pueden ocurrir con más frecuencia que los cambios en la lógica de negocios. Mantener la abstracción del objeto de formulario en la capa de presentación facilita la escalabilidad de la aplicación al permitir cambios en la interfaz de usuario sin afectar otras capas.
Pregunta 2 (1 punto)
¿Cuál es la diferencia entre autenticación y autorización?

La autenticación y la autorización son dos conceptos distintos pero interrelacionados en el contexto de la seguridad de la información. Ambos términos se utilizan comúnmente en sistemas de software, redes y otros entornos para gestionar el acceso a recursos y servicios. Aquí hay una breve explicación de cada uno:

    Autenticación:
        Definición: La autenticación se refiere al proceso de verificar la identidad de un usuario, sistema o entidad.
        Objetivo: Garantizar que la persona o entidad que intenta acceder a un sistema o recurso es quien dice ser.
        Métodos: Puede implicar el uso de credenciales como nombres de usuario y contraseñas, tarjetas inteligentes, biometría (huellas dactilares, reconocimiento facial, etc.) o cualquier otro método que permita verificar la identidad.

    En resumen, la autenticación responde a la pregunta: "¿Eres quien dices ser?".

    Autorización:
        Definición: La autorización se refiere al proceso de conceder o negar permisos y privilegios a un usuario o sistema después de que se ha autenticado.
        Objetivo: Determinar qué acciones o recursos específicos tiene permitido acceder o manipular un usuario autenticado.
        Métodos: Se basa en roles, permisos y políticas que definen qué acciones o recursos están permitidos para usuarios específicos.

    En resumen, la autorización responde a la pregunta: "Después de autenticarte, ¿qué estás autorizado a hacer?".

Ejemplo:

    Autenticación: Imagina un sistema que te pide un nombre de usuario y una contraseña para iniciar sesión. Si proporcionas las credenciales correctas, se considera que te has autenticado con éxito.
    Autorización: Después de autenticarte, el sistema determina qué acciones puedes realizar. Por ejemplo, un usuario regular puede tener permisos para leer información, pero no para realizar cambios, mientras que un administrador puede tener permisos más amplios que incluyan la capacidad de modificar datos.

Resumen:
La autenticación se ocupa de verificar la identidad, mientras que la autorización se ocupa de determinar los privilegios y permisos asociados con esa identidad autenticada. Ambos conceptos son fundamentales para garantizar la seguridad y el control de acceso en sistemas y entornos informáticos.



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


Parte 1

Previamente ejecutando todos los comandos para inizializar el proyecto se verifica cucumber es así que nuestro proyecto queda así

![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/ddd97dc4-e0bf-4af3-997b-fdfbec3a7162)

Con los escenarios fallidos

![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/491150b3-6675-413d-bbfa-1864efe93bf3)

Cobertura de codigo 
El index.html nos muestra un informde nuestras pruebas en general
![imagen](https://github.com/brei004/SustiDesarrollo/assets/153737279/3b5697d2-3964-4860-a5fa-cc4229fc9663)



Parte 3

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

* Pregunta 4 *
Pregunta: ¿Dónde podemos conseguir una instancia de Movie real para utilizarla en dicha prueba?
- Podemos acceder a instancias reales de Movie mediante un archivo yml, el cual nos servirá en el entorno de pruebas y se le pueden crear muchas instancias de objetos Movie, así simular un entorno real. Este se debe de ubicar en la carpeta spec/fixtures
Pregunta: ¿Qué hacen los siguientes códigos entregados y donde se ubican? . ¿Por qué hay que tener
cuidado en su uso?
- Los códigos entregados son un archivo yml y un archivo de pruebas de ruby, se ubican dentro de la carpeta spec en nuestro proyecto. Por el lado de movies.yml se inicializa una película milk_movie con 4 parametros y documentary_movie con 3 parametros, mientras que el archivo movie_spec nos proporcia el test de nuestro modelo, describiendo como debería comportarse al solicitarle el metodo name_with_rating a el modelo movie, el cual utilizando milk_movie nos debería retorna su respectivo rating para pasar la prueba.
- Hay que tener cuidado al usar los fixtures ya que son una representación a mano de una instancia de Movie y puede que no cumpla con ciertas restricciones que deseamos aplicar a nuestras instancias
Pros
- Creación de una instancias real de un objeto
- Realizar un analisis del comportamiento con objetos reales
Contras
- Falta de generalidad
  
Parte 4
    Crear la clase TennisScorer y ejecutar la primera especificación:

ruby

# tennis_scorer.rb

class TennisScorer
  def initialize
    @score_sacador = 0
    @score_receptor = 0
  end

  def puntuacion
    "#{score_to_text(@score_sacador)}-#{score_to_text(@score_receptor)}"
  end

  def marcar_punto_sacador
    @score_sacador += 1
  end

  def marcar_punto_receptor
    @score_receptor += 1
  end

  private

  def score_to_text(score)
    case score
    when 0
      "0"
    when 1
      "15"
    when 2
      "30"
    when 3
      "40"
    else
      raise "Puntuación no válida"
    end
  end
end

    Ejecutar la especificación:

bash

rspec

Esto debería mostrar un fallo en todas las expectativas porque aún no hemos implementado la lógica.

    Desarrollar las expectativas restantes:

ruby

# tennis_spec.rb

RSpec.describe "TennisScorer" do
  describe "puntuación básica" do
    before(:each) do
      @scorer = TennisScorer.new
    end

    it "empieza con un marcador de 0-0" do
      expect(@scorer.puntuacion).to eq("0-0")
    end

    it "hace que el marcador sea 15-0 si el sacador gana un punto" do
      @scorer.marcar_punto_sacador
      expect(@scorer.puntuacion).to eq("15-0")
    end

    it "hace que el marcador sea 0-15 si el receptor gana un punto" do
      @scorer.marcar_punto_receptor
      expect(@scorer.puntuacion).to eq("0-15")
    end

    it "hace que el marcador sea 15-15 después de que ambos ganen un punto" do
      @scorer.marcar_punto_sacador
      @scorer.marcar_punto_receptor
      expect(@scorer.puntuacion).to eq("15-15")
    end
  end
end

    Ejecutar las expectativas restantes:

bash

rspec

Esto mostrará fallas para las expectativas restantes.

    Corregir duplicación en la especificación y desarrollar las dos últimas expectativas:

ruby

# tennis_spec.rb

RSpec.describe "TennisScorer" do
  describe "puntuación básica" do
    before(:each) do
      @scorer = TennisScorer.new
    end

    it "empieza con un marcador de 0-0" do
      expect(@scorer.puntuacion).to eq("0-0")
    end

    it "hace que el marcador sea 15-0 si el sacador gana un punto" do
      @scorer.marcar_punto_sacador
      expect(@scorer.puntuacion).to eq("15-0")
    end

    it "hace que el marcador sea 0-15 si el receptor gana un punto" do
      @scorer.marcar_punto_receptor
      expect(@scorer.puntuacion).to eq("0-15")
    end

    it "hace que el marcador sea 15-15 después de que ambos ganen un punto" do
      @scorer.marcar_punto_sacador
      @scorer.marcar_punto_receptor
      expect(@scorer.puntuacion).to eq("15-15")
    end

    it "40-0 después de que el sacador gane tres puntos" do
      3.times { @scorer.marcar_punto_sacador }
      expect(@scorer.puntuacion).to eq("40-0")
    end

    it "W-L después de que el sacador gana cuatro puntos" do
      4.times { @scorer.marcar_punto_sacador }
      expect(@scorer.puntuacion).to eq("W-L")
    end

    it "L-W después de que el receptor gane cuatro puntos" do
      4.times { @scorer.marcar_punto_receptor }
      expect(@scorer.puntuacion).to eq("L-W")
    end

    it "Deuce después de cada uno gana tres puntos" do
      3.times do
        @scorer.marcar_punto_sacador
        @scorer.marcar_punto_receptor
      end
      expect(@scorer.puntuacion).to eq("Deuce")
    end

    it "El sacador con ventaja después de cada uno gana tres puntos y el sacador obtiene uno más" do
      3.times do
        @scorer.marcar_punto_sacador
        @scorer.marcar_punto_receptor
      end
      @scorer.marcar_punto_sacador
      expect(@scorer.puntuacion).to eq("Advantage-Sacador")
    end
  end
end

Si deseas utilizar Ruby on Rails para crear un proyecto que incluya la estructura básica junto con RSpec para las pruebas, puedes seguir estos pasos:

    Crear un nuevo proyecto de Rails:

bash

rails new tennis_project

Esto creará un nuevo directorio llamado tennis_project con la estructura básica de un proyecto de Ruby on Rails.

    Navegar al directorio del proyecto:

bash

cd tennis_project

    Agregar la gema RSpec al archivo Gemfile:

Abre el archivo Gemfile en un editor de texto y agrega la siguiente línea:

ruby

group :development, :test do
  gem 'rspec-rails'
end

Luego, ejecuta:

bash

bundle install

    Configurar RSpec en el proyecto:

bash

rails generate rspec:install

Esto generará la configuración necesaria para RSpec en tu proyecto.

    Crear la clase TennisScorer y las especificaciones:

Puedes crear la clase TennisScorer en el directorio app/lib y las especificaciones en el directorio spec.

bash

mkdir -p app/lib
touch app/lib/tennis_scorer.rb

mkdir spec
touch spec/tennis_spec.rb

    Ejecutar las pruebas:

Ahora, puedes ejecutar las pruebas utilizando RSpec:

bash

rspec

Esto ejecutará las pruebas ubicadas en el directorio spec.



