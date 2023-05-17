# Docker:
Docker es una plataforma de software que le permite crear, probar e implementar aplicaciones rápidamente. Docker empaqueta software en unidades estandarizadas llamadas contenedores que incluyen todo lo necesario para que el software se ejecute, incluidas bibliotecas, herramientas de sistema, código y tiempo de ejecución.

# Componentes:

  - Imagenes: Una imagen es una especie de plantilla, una captura del estado de un contenedor. Una imagen de un contenedor es como un snapshot de una máquina virtual, pero mucho mucho más ligero.
  - DockerFile: Es un archivo de configuración que se utiliza para crear imágenes. En dicho archivo indicamos qué es lo que queremos que tenga la imagen, y los distintos comandos para instalar las herramientas. Ejemplo instalar ubuntu y git:
    FROM ubuntu:14.04
    RUN apt-get update
    ENV DEBIAN_FRONTEND noninteractive
    RUN apt-get -qqy install git
  - Contenedores: Son instancias en ejecución de una imagen. Son los que ejecutan cosas, los que ejecutarán nuestra aplicación. El concepto de contenedor es como si restauráramos una máquina virtual a partir de un snapshot. A partir de una única imagen, podemos ejecutar varios contenedores. Como las imágenes no cambian, si creas un contenedor a partir de una imagen, y mientras que se está ejecutando el contenedor cambias algo o instalas alguna herramienta, al parar dicho contenedor y después volver a ejecutar otra vez la misma imagen, esos cambios no se verán reflejados. Docker va trackeando los cambios en los contenedores como si fuera una herramienta de control de versiones, por lo que si realmente deseas esos cambios, haciendo un commit del contenedor puedes crear otra imagen que contenga dichos cambios. Por lo tanto otro beneficio de Docker, es el versionado de los contenedores. Si algo va mal en nuestra aplicación, podremos volver de forma sencilla a una versión anterior del contenedor, a una versión anterior del entorno.
  - Volumenes: No es una buena práctica guardar los datos persistentes dentro de un contenedor de Docker. Para eso están los volúmenes, fuera de los contenedores. Así podremos crear y borrar contenedores sin preocuparnos por que se borren los datos. Además los volúmenes se utilizan para compartir datos entre contenedores.
  -DockerCompose: Docker Compose es una herramienta de la plataforma dedicada a la orquestación local de dockers, es decir, se utiliza con el objetivo de definir y ejecutar aplicaciones Docker de varios contenedores de forma fácil y rápida. Con Compose haremos uso de un fichero de texto con la extensión YAML en el que realizaremos la configuración de los servicios (imágenes), redes y volúmenes para persistencia de datos que requieran nuestras aplicaciones. 

# Ejemplo
version: "1"

services:
  backend:
    # El build elemento define las opciones de configuración que aplican las implementaciones de Compose para crear una imagen de 
    # Docker desde el origen.
    build:
      # build se puede especificar como una cadena que contiene una ruta al contexto de compilación 
      # o como una estructura detallada:
      # Usando la sintaxis de cadena, solo el contexto de compilación se puede configurar como:

      # Una ruta relativa a la carpeta principal del archivo Compose. Esta ruta DEBE ser un directorio y debe contener unDockerfile
      # services:
      #   webapp:
      #     build: ./dir

      # Una URL del repositorio de git. Las URL de Git aceptan la configuración de contexto en su sección de fragmentos, 
      # separados por dos puntos ( :). La primera parte representa la referencia que Git extrae y puede ser una rama, 
      # una etiqueta o una referencia remota. La segunda parte representa un subdirectorio dentro del repositorio que se usa 
      # como contexto de compilación.
      