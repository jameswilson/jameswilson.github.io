---
layout: post
title: Los ABC de Multi-idioma
---

Esto es un guía que se puede utilizar para instalar Drupal en multiples
lenguajes. Fue creado originalmente para un taller de 2 horas en DrupalCamp
Ecuador el 23 de Octubre de 2014 en Guayaquil, Ecuador.

Como hacer tu sitio múlti-idioma con Entity Translation en Drupal 7.

OJO: No vamos a usar Content Translation, sino **Entity Translation.**

Instalar Drupal
===========

* Poner el archivo .po en la ruta: **profiles/standard/translations/**
* Instalar sitio con "Standard" profile.
* Escoger instalación en ingles (por defecto) o bien (de preferencia) en español.

Descargar modulos
==============

Descargar y habilitar todos los módulos que vamos a utilizar:


Core

* **Locale** (ya habilitado si instalaste en español)

Fields
Multilingual
Multilingual - Entity Translation
Multilingual - Internationalization

* **Internationalization** ([i18n][1]) VERSION DEV (7.x-1.x-dev) para evitar
    [este error][2].
    * **Field translation** (i18n_field submodule)
    * **Menu translation** (i18n_menu submodule)
    * **Variable translation** (i18n_variable submodule)
    * **String translation** (i18n_string submodule)

Variable

* **Variable** ([variable][3])
    * **Variable Realm** (variable_realm submodule)
    * **Variable Store** (variable_store submodule)

Configurar actualizaciones de traducciones.
================================

*   Localization update permite descargar y actualizar traducciones del core
    de Drupal y otros módulos instalados
*   Debes especificar donde almacenar las traducciones descargados:


**Admin » Configuración » Regional e idioma » Idiomas » Actualizaciones de traducciones**

URL: `admin/config/regional/language/update`

**Almacenar archivos descargados:** sites/all/translations

![][4]

Configurar la detección y selección de idioma.
==========================================

**Admin » Configuración » Regional e idioma » Idiomas » Detección y selección**

URL: `admin/config/regional/language/configure`

* Método de detección de la **INTERFAZ**
    * URL (prefijo de URL)
    * Navegador.
* Método de detección del **CONTENIDO**

![][5]

Agregar otra idioma
============================

Por ejemplo, agrega la idioma de Frances, y configurar los prefijos de rutas:

**Admin » Configuración » Regional e idioma » Idiomas**

URL: `admin/config/regional/language`

*   En este caso usamos códigos de idioma (en, es, fr) como prefijo de ruta.
*   Se podría también configurar diferente dominios (example.com, example.es,
    example.fr) o sub-dominios (en.example.com, es.example.com, fr.example.com).


![][6]

Configurar Fecha y Hora.
============================

Por defecto Drupal usa mes/día/año (el format común del ingles) lo que hay que
cambiar a día/mes/año.


URL: `/admin/config/regional/date-time`

![][7]

También se recomienda que creas formatos más comunes en español como "Lunes el
20 de Octubre de 2012 a las 11:16pm"


URL: `/admin/config/regional/date-time/formats`
Haz clic sobre: Añadir formato de fecha.

Long: `l el j de F del Y a las h:ga`
Medium: `l j de F Y - h:ga`

![][8]


Alternador de idioma
============================

**Admin » Estructura » Bloques**

URL: `/admin/structure/block`

Habilita el bloque que es para _Texto de la interfaz del usuario_ en la region
del _Encabezado_.

Hay dos opciones:

![][9]

* Si tienes muchas idiomas, se recomienda utilizar el módulo **lang_dropdown**.
* Siempre usar el bloque que es para _Texto de la interfaz del usuario._

Habilitar traducción para Nodos y Taxonomía
==========================================

**Admin » Configuración » Regional e idioma » Entity translation**

URL: `admin/config/regional/entity_translation`

![][10]

Esconder campos que no son por traducir
![][11]

Configurar traducción de campos
==========================================

Habilitar el soporte multi-lenguaje con field translation en todos los tipos de
contenido.

**Admin » Estructura » Tipos de contenido » Articulo » Editar**

URL: `admin/structure/types/manage/article`

**Admin » Estructura » Tipos de contenido » Basic Page » Editar**

URL: `admin/structure/types/manage/page`

Sección: Opciones de publicación

![][12]

Configurar modulo _Title_
==========================================

Habilitar traducción de los Títulos de contenido.

El campo del Titulo es un caso especial en Drupal 7. _Se utiliza el modulo
[Title][13] para convertir el campo en algo que se puede traducir con Entity
Translation como los otros campos._


**Admin » Configuración » Autoría del contenido » Opciones de título**

URL: `admin/config/content/title**`

![][14]

![][15]

Reemplazar todos los campos de **titulo** en todos los contenidos:

**Admin » Estructura » Tipos de contenido » Articulo » Gestionar Campos**

URL: `admin/structure/types/manage/article/fields`

![][16]

Reemplazar los campos del **Nombre** y **Descripción** de Taxonomía:

URL: `admin/structure/taxonomy/tags/fields`

![][17]
Comprobar que la traducción del campo esta habilitada.

admin/structure/taxonomy/tags/fields/name_field
admin/structure/taxonomy/tags/fields/description_field
![][18]

Traducir campos
============================

Habilitar traducción del campo de **body** en **todos los tipos de
contenido** (Article y Basic Page).

**Admin » Estructura » Tipos de contenido » Articulo » Gestionar Campos**

URL: `admin/structure/types/manage/article/fields`

![][19]

**Admin » Estructura » Tipos de contenido » Page » Gestionar Campos**

URL: `admin/structure/types/manage/page/fields`

![][20]

**No habilita** traducción para los campos:
Tags e Imagen.

Crear y revisar contenido!
============================


URL: `/node/add/article`

![][21]

![][22]

Traducir etiquetas de los Campos:
============================

Si mostras las etiquetas de campos como "Tags:" en el Front-end, tienes que
traducirles con el modulo _Field Translation_ (i18n_field)

**Admin » Estructura » Tipos de contenido » Article » Gestionar campos » Tags » Traducir**

URL: `admin/structure/types/manage/article/fields/field_tags/translate`

![][23]
¡Ahora sí!

![][24]

![][25]

![][26]

Traducir términos:
============================

**Admin » Estructura » Taxonomía » Lista**

URL: `admin/structure/taxonomy/tags`

![][27]

![][28]

Traducir variables (Site Name, Slogan, etc):
==========================================

**Admin » Configuración » Regional e idioma » Multilingual settings » Variables**

URL: `admin/config/regional/i18n/variable`

![][29]

**Admin » Configuración » Sistema » Información del sitio**

URL: `admin/config/system/site-information`

![][30]

Menus
==============

Escoger una metodologia para traducción de los menus.

**SI: Un solo menu, con links duplicados para todas las idiomas.**
NO: Multiples menus, uno para cada lenguaje.
Habilita i18n_menu, i18n_translation.

**Admin » Estructura » Menús » Menú principal » Editar menú**

URL: `admin/structure/menu/manage/main-menu/edit`

![][31]

Cada enlace debe tener una idioma:

![][32]
Debes traducir y vincular cada enlace en cada idioma.![][33]

Bloques
==============

Escoger una metodologia para traducir bloques:

*   Bloques con visibilidad según idioma.
    - Desventaja: duplicar bloques en cada lenguaje, poco manejable para
    detectar, agrupar, y sincronizar traducciones.
*   Beans con Entity Translation.
    - Ventaja: interfaz simple de traducción de cada campo, no hay bloques
    duplicados.
    - Desventaja: No puedes armar workflows de estados de traducción.
*   Nodos con Entity Translation.
*   Boxes con i18n_boxes + i18n_string.

Views
==============

Views no require modificación con Entity Translate, pero por defecto si un nodo
no tiene traducción, se mostrará el contenido en la idioma madre (source
language).

Para quitar el contenido que no ha sido traducido de tus vistas para no tener
contenido mezclado, puedes usar un filtro:

**Contenido: Idioma > El idioma del usuario actual**

![][34]

![][35]


Actualizar traducciones
============================

**Admin » Configuración » Regional e idioma » Traducir interfaz » Actualizar**

URL: `admin/config/regional/translate/update`

A veces, al habilitar un modulo, no se descarga las traducciones
automáticamente. Debes actualizar las traducciones manualmente de tiempo a
tiempo, para estar al día con las traducciones del interfaz, contribuido por la
comunidad.


Buscar y traducir interfaz
============================

**Admin » Configuración » Regional e idioma » Traducir interfaz » Traducir**

URL: `admin/config/regional/translate/translate`

Otros módulos
==============

*   [Localization Client][36] (l10n_client) -
    Facilita traducción de cadenas de texto del interfaz en tu sitio y
    contribución de los mismos al localize.drupal.org
*   [Transliteration][37] -
    convierte caracteres UTF8 a ASCII á => a, é => e etc. Bueno para URLs y
    para renombrar archivos que tengan caracteres extraños.
*   [Administration Language][38] (admin_language) -
    Cuando uno va a traducir el contenido de un nodo, el interfaz de
    administración se cambia al lenguaje del destino. Usar este modulo para
    dejar el backend en tu lenguaje preferida.

Referencias
==============

[1]: https://www.drupal.org/project/i18n
[2]: https://www.drupal.org/node/2227523
[3]: https://www.drupal.org/project/variable
[4]: http://cdn.images.postach.io/w600_815a54d96c61870820faffb46508857f.png
[5]: http://cdn.images.postach.io/w600_dacce216f0d8fb8e8a4bc8b9ad66d41d.png
[6]: http://cdn.images.postach.io/w600_a5a4fd56bd500b9c083de7b192548e76.png
[7]: http://cdn.images.postach.io/w600_8c271d9208ace62f4f997c3365780c20.png
[8]: http://cdn.images.postach.io/w600_47b6b60d6ebd26277ea34d561e13b5b2.png
[9]: http://cdn.images.postach.io/w600_b15571a9c4178ec82a374d4829208ff9.png
[10]: http://cdn.images.postach.io/w600_1b4c5d40848093131254181609bcd7a1.png
[11]: http://cdn.images.postach.io/w600_0bc9b398f2e1206de47bfedf16df7f29.png
[12]: http://cdn.images.postach.io/w600_2e17b5f86fd84d8df905a0472d5fca5a.png
[13]: https://www.drupal.org/project/title
[14]: http://cdn.images.postach.io/w600_b284a2657c688fbbe4dde3efb173d26d.png
[15]: http://cdn.images.postach.io/w600_b26b463976d555f1572534281112c435.png
[16]: http://cdn.images.postach.io/w600_3b791f821eab91e675ca6dff673a165f.png
[17]: http://cdn.images.postach.io/w600_52068353c954c6439893d73fe24c5efe.png
[18]: http://cdn.images.postach.io/w600_1546e751ac071bc940aaa0920a47c2a7.png
[19]: http://cdn.images.postach.io/w600_3d19364a4c98b151a8ccbac0e73d26c8.png
[20]: http://cdn.images.postach.io/w600_56624d110d7bb7c57363973bdd68ebd9.png
[21]: http://cdn.images.postach.io/w600_9af6522b45df95402f96fd20699318fc.png
[22]: http://cdn.images.postach.io/w600_6a3648f8d2fcdfdd9652a486f0bb3999.png
[23]: http://cdn.images.postach.io/w600_9dc4484aacb1eb36aaf269ecfc4de204.png
[24]: http://cdn.images.postach.io/w600_4ecd07e6a621389957eab67bab579e6a.png
[25]: http://cdn.images.postach.io/w600_df219f1bdc46cce09ff6f949ccdd40f3.png
[26]: http://cdn.images.postach.io/w600_4f510242388dcb259ecb704138485185.png
[27]: http://cdn.images.postach.io/w600_99a368c6d0d1077855ca5ca1f0cbfae2.png
[28]: http://cdn.images.postach.io/w600_beac75d492019f6c2102431a9166ccc4.png
[29]: http://cdn.images.postach.io/w600_4cc78e618ea6b262a032fbdc6eb3cde1.png
[30]: http://cdn.images.postach.io/w600_68f2c349eccd9a301cc63eca08826806.png
[31]: http://cdn.images.postach.io/w600_a13925812b5a6f5cd36d12098eef91ba.png
[32]: http://cdn.images.postach.io/w600_c37c9e0b0b0f08cf89134aa548e31998.png
[33]: http://cdn.images.postach.io/w600_b4f35f45d16e26048efe3fbdbb94346e.png
[34]: http://cdn.images.postach.io/w600_a56ace65ffa934bcacde3f75ea901c20.png
[35]: http://cdn.images.postach.io/w600_37d7df223ea3ef1462ede420f4a2f003.png
[36]: https://www.drupal.org/project/l10n_client
[37]: https://www.drupal.org/project/transliteration
[38]: https://www.drupal.org/project/admin_language

