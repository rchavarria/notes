# Montar un blog con Jekyll

El objetivo es poder montar un blog, un sitio web estático o una *landing page* sobre Jekyll. 
Para no guarrear la máquina de desarrollo, se utilizará un contenedor Docker donde ya esté instalado
Jekyll y ruby.

## Tecnologías

- [ruby](https://www.ruby-lang.org/en/)
- [Jekyll](https://jekyllrb.com/)
- [Docker](https://www.docker.com/)
- [Docker compose](https://docs.docker.com/compose/): es un amigo genial para Docker y para la falta
de memoria. Ayuda a no tener que recordar con qué comando `docker` hay que crear el contenedor.

## Elegir un tema de Jekyll

1. [Airspace](https://github.com/ndrewtl/airspace-jekyll): este diseño está muy curioso.
Ver [ejemplo](http://www.devempathybook.club/).
2. [Landing page](http://www.jekyllthemes.io/theme/24792726/landing-page-theme): este
también está bien. Es sencillo, pero es resultón, con unas pocas imágenes podría quedar bien.
El [ejemplo](http://shaneweng.com/landing-page-theme/) se ve sencillo y simple.
3. [Agency](https://y7kim.github.io/agency-jekyll-theme/): este también está muy bien, me
gusta mucho los círculos conectados donde cada círculo es un año (como un línea del tiempo
o algo así). A lo mejor exactamente igual no es lo que podría ir bien, pero está curioso.
Ver [ejemplo](https://y7kim.github.io/agency-jekyll-theme/).
4. [One page wonder](https://www.jekyllthemes.io/theme/34391076/one-page-wonder-jekyll):
este diseño quizá es muy simplón. En el
[ejemplo](https://mushishi78.github.io/one-page-wonder-jekyll/), el problema que tiene,
es que como no ponen imágenes, queda muy soso.
5. [Grayscale](https://www.jekyllthemes.io/theme/30191476/grayscale-theme): no está mal
del todo, pero quizá quede muy oscuro

## Levantar el blog con el tema elegido

Muy bien, vamos a utilizar el tema *Airspace*.

Lo primero que hay que hacer es clonar el repositorio con el código fuente del tema:

```
git clone https://github.com/ndrewtl/airspace-jekyll
```

El comando crea un directorio llamado `airspace-jekyll`. Desde ese directorio, levantaremos el blog
a través de un comando `docker-compose`. Pero antes, necesitamos el fichero para dicha
herramienta.

El fichero de configuración de `docker-compose` es un fichero `.yml` donde se pueden configurar
prácticamente todos los parámetros para crear un contenedor. El fichero utilizado es similar
a éste (para ver la última versión, echar un vistazo a este
[repo](https://github.com/rchavarria/web-server-jose/blob/master/docker-compose-master.yml). El
fichero se llamará `docker-compose.yml` para simplificar el proceso:

```
version: '3'

services:
  # a container to serve the blog
  blog:
    image: jekyll/jekyll   # build from latest jekyll
    container_name: blog
    ports:
      - 4000:4000          # expose this port
    volumes:
      - .:/srv/jekyll      # share local source files with the container
      - ./vendor/bundle:/usr/local/bundle     # cache ruby gems
      
    entrypoint:
      - jekyll
      - serve
```

Con él, se indica a `docker-compose` que cree un contenedor (o `service`) llamado `blog`,
a partir de la imagen `jekyll/jekyll` (imagen con la última versión de Jekyll), que exponga
el puerto `4000` y que mapee un par de directorios del sistema host al sistema ^*dockerizado*
(`volumes`). Como último paso, se debe ejecutar el comando (o `entrypoint`) `jekyll serve`.

Otros comandos que se pueden ejecutar serían:

- `bundle install`: para instalar las gemas de ruby necesarias para ejecutar el blog. Aunque
este paso ya se hace automáticamente, puede servir para ir depurando y averiguar si tenemos
algún problema con alguna gema en particular
- `jekyll build`: para construir el blog, generar los ficheros estáticos, pero no servirlos
todavía. Igual que el comando anterior, ya se ejecuta automáticamente con `jekyll serve` pero
puede servir para depurar.

En definitiva, para tener el blog corriendo en local, basta con teclear:

```
cd airspace-jekyll
sudo docker-compose docker-compose.yml
```

Ya tenemos el blog ejecutándose, ahora llega la hora de personalizarlo a nuestro gusto e ir añadiendo
posts

## Estudiando la organización de ficheros del tema

Para poder saber qué debemos personalizar, entendamos primero la organización de los ficheros
del tema:

Comenzaremos por `_config.yml`, porque es el fichero que configura todos los proyectos Jekyll. En él
encontramos los siguientes valores a configurar:

- `title` y `subtitle`
- `url`: será la URL a través de la cual accederán a nuestra web
- `baseurl`: parte de la URL que se añadirá a `url` para completar la ruta a nuestra web. Puede
ser simplemente `""` para indicar que la web estará servida desde el directorio raiz
- `cover` y `logo`: diversas imágenes
- `markdown`: motor de parseo de Markdown
- `descriptions` (lista de `cat` y `desc`): para enumerar cada categoría y sus descripciones
para los posts del blog

Mirando las imágenes incluidas en el tema Airspace, `img/slider-bg.jpg` parece interesante, ya que es la imagen que aparece en todas las Páginas de la web del tema.

## ¿Qué mas?

## Referencias

- [Jekyll + Docker + Github Pages](http://cowsandcode.com/2018/jekyll-docker-github-pages/):
de aquí surgió la idea original de este proyecto. No he seguido los pasos uno por uno, he
tenido que improvisar e investigar por mi cuenta, pero eso no le quita mérito al post.
