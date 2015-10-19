---
layout: post
title: Crear un sitio multi-idioma con Drupal 8
---

Esto es un guía que se puede utilizar para instalar Drupal en multiples
idiomas. Fue creado originalmente para un taller de 1 hora en DrupalCamp
Ecuador el 16 de Octubre de 2015 en Quito, Ecuador.

Para crear un sitio multi-idioma en Drupal 7 revisa mi post del año pasado: [Los ABC de Multi-idioma en Drupal 7][1].

1. Crear un Sitio
--------------
* Abrir una cuenta en [Pantheon.io][2].
* Crear un sitio en el Dashboard de Pantheon.
* Instalar Drupal 8 RC-1.


2. Instalar Drupal
--------------
- Selecciona español como lenguaje predeterminado.
- Crear cuenta de Administrador.


3. Agregar idioma
--------------
- Ingresar como Administrador.
- Administrar > Configuración > Regional e idioma > Idiomas<br>
  URL: `admin/config/regional/language`
- Click botón: *Agregar idioma* y selecciona el inglés.


4. Detección y selección
---------------------
Qué idioma utilizar y cuándo?

- Administrar > Configuración > Regional e idioma > Idiomas: Detección y selección
- Habilitar "URL" como método principal de detección.


5. Alternador de idiomas
-------------------
Colocar el bloque del alternador de idiomas en la primera barra lateral del sitio.

- Administrar > Estructura > Diseño de bloques<br>
  URL: `admin/structure/block`
- En la region de la Primera barra lateral, aplasta el botón: *Colocar bloque*.
- Buscar y colocar el bloque *Alternador de idioma*.
- Deshabilitar la opción: *Mostrar título* y cliquear *Guardar el bloque*.
- *Regresar al sitio* para visualizar el Alternador.


6. Configurar fecha y hora
--------------------------
Por defecto Drupal usa mes/día/año (el format común del ingles) lo que hay que cambiar a día/mes/año.

URL: `/admin/config/regional/date-time`

También se recomienda crear formatos más comunes en español como:

- Long: `admin/config/regional/date-time/formats/manage/long`<br>
  "Lunes el 19 de Octubre de 2015 a las 11:15 pm"<br>
  `l \e\l j \d\e F \d\e\l Y \a \l\a\s h:g a`
- Medium: `admin/config/regional/date-time/formats/manage/medium`<br>
  "Lunes 19 de Octubre 2015 - 11:15 pm"<br>
  `l j \d\e F Y - h:g a`
- Short: `admin/config/regional/date-time/formats/manage/short`<br>
  "19/10/2015 - 11:15 pm"<br>
  `d/m/Y - h:i a`


7. Habilitar módulos para traducción
------------------------------------
- Administrar > Extender<br>
  URL: `admin/modules`
  - *Dejar deshabilitado Configuration Translation. <sup><a href="#fn">1</a></sup>*
  - Seleccionar los siguientes módulos:
      - Content Translation
      - Interface Translation (se habilita este modulo automáticamente cuando se instala Drupal en español).
- Entender la diferencia entre traducción *de Contenido* y traducción *de la Interfaz de usuario*.
  - La interfaz del usuario
      - Son cadenas de texto traducible en el núcleo de Drupal y sus módulos.
      - [localize.drupal.org][3]: Contribuir, descargar, y actualizar las traducciones.
      - Gestionar (buscar, traducir, exportar, importar, actualizar) a través de una sola interfaz: `admin/config/regional/translate`
  - El contenido (o sea entidades y campos)
      - Son datos y textos almacenados dentro del contenido creado para tu sitio a través del sistema de entidades y campos en Drupal.
      - No se puede compartir ni exportar las traducciones de contenido con Drupal core.
      - No hay un solo lugar para ver todas las traducciones de contenido. La gestión se encuentra como pestaña en la configuración de cada entidad creado en tu sitio.


8. Habilitar traducción de Entidades
---------------------------------
- Administrar > Configuración > Regional e idioma > Content language and translation<br>
  URL: `admin/config/regional/content-language`
- Seleccionar las siguientes entidades:
  - Contenido
  - Bloque personalizado
  - Enlace de menú personalizado
  - Término de taxonomía
- Habilitar las siguientes opciones para todas las entidades seleccionadas:
  - *Traducible*. (Dejar seleccionados los campos predeterminados.)
  - *Muestra el selector de idioma al crear y editar paginas*.
  - Idioma predeterminado: *Interface text language selected for page*.
- Click botón: Guardar configuración


9. Crear página con enlace de menú y traducirlo
--------------------------------------------
- Administrar > Contenido: Agregar contenido: Página básica<br>
  URL: `node/add/page`
- Titulo: `Acerca de`
- Cuerpo: `Cuerpo de texto para la pagina de Acerca de.`
- Proporciona un enlace de menu en la barra lateral: *Opciones del Menú*
- Click botón: *Guardar y publicar*
- Click pestaña: Editar
- Click pestaña: Translate
- Agregar traducción para inglés.
  - Title:  `About us`
  - Body:  `Body text for the About us page.`
  - No tocar la traducción del menú.
- Administrar > Estructura > Menus > Main navigation > Edit menu<br>
  URL: `admin/structure/menu/manage/main`
- Seleccionar operación: *Traducir* para el enlace de "Acerca de" y proporcionar una traducción al inglés: `About us`


10. Crear artículo con categoría e imagen y traducirlo
--------------------------------------------------
- Administrar > Contenido: Agregar contenido: Página básica<br>
  URL: `node/add/article`
  - Titulo: `Un artículo`
  - Cuerpo: `Un artículo en español.`
  - Etiquetas: `Noticias`
  - Proporcionar una imagen con texto alternativo `Drupal Ocho` en español.
  - Click botón: *Guardar y publicar*
- Click pestaña: Editar
- Click pestaña: Translate
- Agregar una traducción en inglés.
  - Titulo: `An article`
  - Cuerpo: `An article in English.`
  - *Deja las Etiquetas tales como están.*
  - Alternative Text: `Drupal Eight`.


11. Traducir etiqueta 'Noticias' al inglés
--------------------------------------
- Administrar > Estructura > Taxonomía<br>
  Cliquear *Lista de términos* para el vocabulario *Etiquetas*.<br>
  URL: `admin/structure/taxonomy/manage/tags/overview`
- Cliquear la operación *Traducir* para el termino 'Noticias'.
- Agregar una traducción en inglés: `News` y Guardar.
- *Regresar al sitio* y busca la version en inglés del artículo para verificar que esta traducido.


12. Agregar un bloque personalizado
-------------------------------
- Administrar > Estructura > Diseño de bloques<br>
  URL: `admin/structure/blocks`
- Colocar bloque > Añadir bloque personalizado
  - Descripción del bloque: `Un bloque lateral`
  - Cuerpo: `Hola! Esto es un sitio de prueba para mostrar la funcionalidad de traducción de Drupal 8.`
  - Click botón: *Guardar*
  - Seleccionar region: `Primera barra lateral`
  - Click botón: *Guardar el bloque*
- Regresar al sitio, encuentra el bloque en la barra lateral y haz click en la opción de *Traducir*.
- Agregar una traducción en inglés:
  - Block description<sup><a href="#fn">2</a></sup>: `A sidebar block`
  - Body: `Hello! This is a test site to demonstrate the translation functionality in Drupal 8.`
  - Click botón: *Save*


13. Personalizar y traducir el nombre del sitio y slogan
-------------------------------------

- Abrir: `admin/config/system/site-information`
  - Nombre de sitio: `D8 Multilenguaje`
  - Lema: `Instalando Drupal 8 en varias idiomas`
  - *Guardar configuración*.
- Habilitar el modulo *Configuration Translation* <sup><a href="#fn">3</a></sup>.
- Abrir: `admin/config/regional/config-translation`
- Buscar 'System information' y click *Traducir*.
- Agregar traducción al inglés.
  - Site name: `D8 Multilanguage`
  - Slogan: `Installing Drupal 8 in various languages`
  - *Guardar traducción*.


Extras
======


1. Alternador de idiomas como menú desplegable
-------------------------------------------

OJO: parece que esta funcionalidad está fallando en Pantheon.

- Buscar en la página del proyecto [Language Switcher Dropdown][4] un enlace para el archivo zip del modulo para Drupal 8.
- Copiar el enlace al portapapeles.
- Abrir Administrar > Extender > Instalar nuevo modulo.
- Pegar el enlace y hacer click en *Instalar*.

Subir el módulo descomprimido dentro de la carpeta `/modules` mediante SFTP o GIT (dependiendo de tu configuración en Pantheon). Ambas requiere una aplicación

------

<sub id="fn">Notas al pie:</sub>

<sub>
1, 3. Actualmente hay un error del PHP Runtime en la gestión de tipos de contenido cuando instalas Drupal en español y habilitas el modulo de *Configuration Translation*. Ver [Issue #2584603](https://www.drupal.org/node/2584603).
</sub>

<sub>
2. El campo de la *Descripción del bloque* tiene un problema en la traducción y por lo tanto la versión traducido del cuerpo del bloque siempre saldrá con el título en el idioma original.
</sub>


[1]: /2014-10-23-los-abc-de-multi-idioma-en-drupal-7.html
[2]: https://pantheon.io
[3]: http://localize.drupal.org
[4]: https://www.drupal.org/project/lang_dropdown
