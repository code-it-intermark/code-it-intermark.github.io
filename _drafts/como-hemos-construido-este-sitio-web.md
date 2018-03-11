---
layout: 2018_post
title: Queremos ser auténticos ninjas
excerpt: Te explicamos que herramientas hemos utilizado y que pasos hemos seguido para construir el sitio web del evento.
featured-img: github-ninja.jpg
date: 2018-03-11 18:01:00 +0100
category: blog
tags: ['2018', 'jekyll', 'github']
author: miguelangelvilaf
comments: true
---

Cuando surgió la iniciativa de organizar este evento, uno de los primeros temas que se puso sobre la mesa fue la necesidad o no de disponer de un sitio web donde todas las personas intersadas pudieran encontrar más información sobre el evento y las charlas que se iban a impartir.

Al tratarse de una experiencia piloto y hacerse este año a nivel interno, es decir, solo para **Intermark IT**, no teníamos claro si debíamos difundir hacia el exterior este tipo de eventos, pero como una de las razones de organizar el primer **Code IT** era ponernos en valor a nosotros mismos pensamos, que mejor manera también de darnos a conocer que tener un sitio web en el que compartir las charlas que se van a dar y donde otros desarrolladores, pertenezcan a Intermark IT o no, puedan dar su opinión y aportar su granito de arena.

Así que nos pusimos manos a la obra. Disponíamos de muy poco tiempo para prepararlo así que lo primero que hicimos, aparte de registrar el dominio, fue decidir que para no complicarnos mucho la vida ibamos a montar un **WordPress** de los de toda la vida, además tampoco queríamos incurrir en demasiados costes, y buscar un alojamiento sin demasiadas pretensiones para WordPress no es complicado.

Pero teníamos un regusto amargo, porque **somos desarrolladores** y nos gustan los retos, y uno de los retos era intentar montar algo que tuviera el menor coste posible (sin contar la dedicación personal en horas de cada uno de los miembros del equipo), no porque no pudieramos disponer de dichos recursos, sino porque queríamos demostrar que es posible hacer una web de calidad con muy poquito dinero, para ser exactos, solo lo que nos costó registrar el dominio. 

Además queríamos salir de nuestra zona de confort y probar algo nuevo que no hubiéramos utilizado hasta la fecha. Así que enseguida lo desechamos y pensamos... **_¿Qué plataforma de bloggin podemos usar que sea open source y no tenga costes de alojamiento?_**

Y pensamos en **GitHub Pages**. 

> Si vamos a compartir el código de nuestras charlas en **GitHub**, porque no aprovechar la infraestructura que nos brinda y que la propia web sea **un proyecto más de código abierto** que compartir con todo el mundo.

Así que nos pusimos manos a la obra.

## Jekyll + GitHub al rescate

![GitHub + Jekyll]({{ "/assets/2018/img/posts/jekyll-github.png" | relative_url}}){:class="img-reponsive" width="100%"}

Y resulta que **GitHub Pages** soporta **Jekyll**. Para los que no lo conozcais, [Jekyll](https://jekyllrb.com/) es un software de creación de blogs estáticos, escrito en Ruby por _Tom Preston-Werner_, uno de los creadores de Github, por lo que está perfectamente integrado con este.

Jekyll tiene una serie de características que lo hacen especialmente interesante para desarrolladores, como son:

* **Alojamiento gratuito en GitHub Pages**, tal y como te hemos comentado.
* **Está enfocado a desarrolladores**, por lo que te resultará muy sencillo incluir código en tus artículos que se transformará a HTML sin ningún problema. Además puedes usar [markdown](https://es.wikipedia.org/wiki/Markdown) para crear el contenido de tu web o los posts, como por ejempo, este mismo que ahora estás leyendo.
* **Es geek**, y eso hace que nos sintamos como verdaderos ninjas.
* **Puedes tener varios colaboradores de forma muy sencilla**, ya que como te comentamos es un repositorio más de cógigo alojado en GitHub, por lo que solo tienes que hacer un clone del proyecto y empezar a trabajar en local hsata que decidas integrar tus cambios con el repositorio remoto de GitHub donde esté alojada tu web.

Aquí no te vamos a explicar como crear un blog desde cero con Jekyll, ya que en la [documentación oficial](https://jekyllrb.com/docs/home/) encontrarás todo lo que necesitas para construir tu propio sitio web.

Te invitamos, eso sí, a que clones o hagas un fork del proyecto y empieces a experimentar tú mismo con la herramienta.

{% highlight plaintext %}
git clone https://github.com/code-it-intermark/code-it-intermark.github.io.git
{% endhighlight %}

Dado que Jekyll está escrito en Ruby necesitarás tenerlo instalado en tu equipo, pero para facilitarte un poco las cosas hemos, y dado que la mayoría **desarrollamos sobre Windows 10** hemos creado un script de _PowerShell_ que utiliza la imagen oficial de [Jekyll para Docker](https://hub.docker.com/r/jekyll/jekyll/), eso sí, necesitarás tener instalado [Docker](https://www.docker.com/docker-windows) en tu equipo.

Para arrancar Jekyll en tu equipo tan solo debes ejecutar el script de arranque desde la propia carpeta del proyecto:

{% highlight plaintext %}
.\jekyll-docker.ps1
{% endhighlight %}

La primera vez que lo arranques tardará un par de minutos, ya que debe descargarse e instalar la imagen de Docker.

Una vez arrancado puedes acceder al sitio web a través de la url http://localhost:4000

Pero teníamos un problema... GitHub Pages te ofrece un subdominio propio en **github.io** con el nombre de tu repositorio, en este caso, https://code-it-intermark.github.io, con certificado SSL incluido pero nosotros queríamos alojarlo bajo un dominio propio, en este caso https://code-it.es.

GitHub, una vez más, te ofrece la posibilidad de usar un dominio propio subiendo al raíz de tu repositorio un archivo CNAME con el nombre del dominio que queremos usar, es decir, **code-it.es**.

El problema es que ya no podemos hacer uso del certificado SSL, sino que necesitaríamos uno propio para el dominio **code-it.es** pero como decíamos al principio, queríamos construir un sitio web para el evento sin tener que hacer ningún desembolso económico... a ser posible claro (a excepción del registro del dominio, evidentemente) ya que pretendíamos mostrar como cualquier desarrollador podría tener su página web personal de manera practicamente gratuita.

Para resolver el problema del certificado SSL recurrimos a **CloudFlare**.

## CloudFlare también al rescate

![CloudFlare]({{ "/assets/2018/img/posts/cloudflare.png" | relative_url}}){:class="img-reponsive" width="40%"}

**CloudFlare** es una herramienta **gratuita** que actúa como un CDN (Red de Distribución de Contenidos) y un proxy (intermediario) entre los visitantes de tu sitio web y el servidor. Al actuar como un proxy, CloudFlare guarda temporalmente contenido estático del sitio, el cual disminuye el número de peticiones al servidor pero sigue permitiendo a los visitantes el acceso al sitio web.

![Cómo funciona CloudFlare]({{ "/assets/2018/img/posts/como-funciona-cloudflare.jpg" | relative_url}}){:class="img-reponsive" width="80%"}


Con esto conseguimos que el sitio web se muestre más rápido, y aparte también conseguimos una capa extra de seguridad.

**Cloudflare** te da la oportunidad, en caso de ser atacado, de adoptar determinadas soluciones, como bloquear IPs o incluso bloquear países enteros en caso de ser necesario, también te libra de por sí de muchos robots y rastreadores maléficos conocidos.

Pero además de todo esto, lo que más nos interesaba es que incluso en su plan gratuito te ofrece un **certificado SSL gratis para tu dominio** en su modalidad _Flexible SSL_.

Lo único que tuvimos que hacer fue **crear una cuenta gratuita en CloudFlare** y seguir estos pasos:

1. Importar el dominio **code-it.es** para recuperar la información actual de DNS que estaban apuntando a los servidores DNS de **GitHub**.
2. En el proveedor con el que registrarmos el dominio, cambiar las DNS para que apuntaran a las DNS de **CloudFlare**.

## Otras herramientas open source

Al ser **Jekyll** un generador de sitios web estáticos, para poder implementar ciertas funcionalidades dinámicas, como el formulario de contacto o los comentarios de los posts, tuvimos que apoyarnos en otras herramientas de código abierto que nos ayudaran a solventar estos problemas.

* Para el envío de correos hicimos uso de [**Formspree**](https://formspree.io/), un servicio online que te da la posibilidad de crear formularios HTML funcionales sin la necesidad de disponer de un backend que trate los datos recibidos.
* En el caso de los comentarios de los posts recurrimos a un herramienta muy conocida, [**Disqus**](https://disqus.com/), un servicio de gestión de comentarios que se puede insertar en un sitio web sea del tipo que sea: blog, tienda online, marketplace... Pero además hace la función de red social y de lector de feeds gracias a su comunidad que permite seguir canales y personas e interactuar con ellas.

## Referencias

Si estás interesado en profundizar más sobre Jekyll, Markdown, Liquid, GitHub Pages, CloudFlare, etc. te dejamos unos enlaces donde podrás encontrar información que puede ser de tú interes.

* [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
* [GitHub Pages](https://help.github.com/categories/github-pages-basics/)
* [GitHub Pages - Jekyll Dependencies](https://pages.github.com/versions/)
* [Jekyll Docs](https://jekyllrb.com/docs/home/)
* [Jekyll Cheatsheet](https://devhints.io/jekyll)
* [Liquid](https://shopify.github.io/liquid/)
* [Rouge (Pygments) - List of supported languages and lexers](https://github.com/jneen/rouge/wiki/List-of-supported-languages-and-lexers)
* [Jekyll, Docker, Windows, and 0.0.0.0](https://tonyho.net/jekyll-docker-windows-and-0-0-0-0/)

>¿Y tú? A que esperas para ser un auténtico ninja!!!.