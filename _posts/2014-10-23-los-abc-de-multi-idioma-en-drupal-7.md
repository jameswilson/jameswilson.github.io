---
layout: post
title: Instalar Drupal 7 en multiples idiomas
lang: es
description: >-
  Este post te guiará con 20 pasos en cómo crear un sitio web en multiples
  lenguajes utilizando la técnica de *Entity Translation* para Drupal 7.
---

Este post te guiará con 20 pasos en cómo crear un sitio web en multiples lenguajes utilizando la técnica de *Entity Translation* para Drupal 7, como alternativa más atractiva de traduccion que la que brinda el módulo de *Content Translation*. Estos apuntes se presentaron en un taller durante DrupalCamp Ecuador el 23 de Octubre de 2014 en Guayaquil, Ecuador.

<!--more-->

## 1. Instalar Drupal

*   Poner el archivo .po en la ruta: **profiles/standard/translations/**
*   Instalar el sitio con "Standard" profile.
*   Escoger instalación en ingles (por defecto) o mejor en
    español.


## 2. Modulos adicionales

Descargar y habilitar los siguientes módulos que vamos a utilizar:

* **Locale** (ya habilitado si instalaste en español)
* **Fields**
* **Multilingual**
* **Multilingual - Entity Translation**
* **Multilingual - Internationalization**
* **Internationalization** ([i18n][1]) VERSION DEV (7.x-1.x-dev) para evitar
    [este error][2].
    * **Field translation** (i18n_field submodule)
    * **Menu translation** (i18n_menu submodule)
    * **Variable translation** (i18n_variable submodule)
    * **String translation** (i18n_string submodule)
* **Variable** ([variable][3])
    * **Variable Realm** (variable_realm submodule)
    * **Variable Store** (variable_store submodule)


## 3. Configurar actualizaciones de traducciones

*   Localization update permite descargar y actualizar traducciones del core
    de Drupal y otros módulos instalados
*   Debes especificar donde almacenar las traducciones descargados:

**Admin » Configuración » Regional e idioma » Idiomas » Actualizaciones de traducciones**

URL: `admin/config/regional/language/update`

**Almacenar archivos descargados:** sites/all/translations

![almacenar-traducciones](https://user-images.githubusercontent.com/243532/47866413-af5d6300-ddcc-11e8-8a1d-f5abf3e7c14c.png)


## 4. Configurar la detección y selección de idioma.

**Admin » Configuración » Regional e idioma » Idiomas » Detección y selección**

URL: `admin/config/regional/language/configure`

* Método de detección de la **INTERFAZ**
    * URL (prefijo de URL)
    * Navegador.
* Método de detección del **CONTENIDO**

![seleccion-de-idioma](https://user-images.githubusercontent.com/243532/47866422-b3898080-ddcc-11e8-8bab-93b5c8671125.png)

## 5. Agregar otra idioma

Por ejemplo, agrega la idioma de Frances, y configurar los prefijos de rutas:

**Admin » Configuración » Regional e idioma » Idiomas**

URL: `admin/config/regional/language`

*   En este caso usamos códigos de idioma (en, es, fr) como prefijo de ruta.
*   Se podría también configurar diferente dominios (example.com, example.es,
    example.fr) o sub-dominios (en.example.com, es.example.com, fr.example.com).

![agregar-idioma](https://user-images.githubusercontent.com/243532/47866427-b71d0780-ddcc-11e8-8813-983ba8ec4805.png)

## 6. Configurar fecha y hora

Por defecto Drupal usa mes/día/año (el format común del ingles) lo que hay que
cambiar a día/mes/año.


URL: `/admin/config/regional/date-time`

![fecha-y-hora](https://user-images.githubusercontent.com/243532/47866429-ba17f800-ddcc-11e8-8e0a-a454b11851f5.png)

También se recomienda que creas formatos más comunes en español como "Lunes el
20 de Octubre de 2012 a las 11:16pm"

URL: `/admin/config/regional/date-time/formats`
Haz clic sobre: Añadir formato de fecha.

Long: `l el j de F del Y a las h:ga`
Medium: `l j de F Y - h:ga`

![regionalizar-fecha-y-hora](https://user-images.githubusercontent.com/243532/47866432-bd12e880-ddcc-11e8-8f8d-f30decebd3ca.png)


## 7. Alternador de idioma

**Admin » Estructura » Bloques**

URL: `/admin/structure/block`

Habilita el bloque que es para _Texto de la interfaz del usuario_ en la region
del _Encabezado_.

Hay dos opciones:

![lang-selector](https://user-images.githubusercontent.com/243532/47866435-c00dd900-ddcc-11e8-9f8b-9f8ab3e3b397.png)

* Si tienes muchas idiomas, se recomienda utilizar el módulo **lang_dropdown**.
* Siempre usar el bloque que es para _Texto de la interfaz del usuario._


## 8. Habilitar traducción de entidades

Necesitamos traducir el contenido del sitio, representado en los nodos y las taxonomías.

**Admin » Configuración » Regional e idioma » Entity translation**

URL: `admin/config/regional/entity_translation`

![entity_translation](https://user-images.githubusercontent.com/243532/47866444-c308c980-ddcc-11e8-9a03-29a8177ee86a.png)

Esconder campos que no son por traducir

![hide-shared-fields](https://user-images.githubusercontent.com/243532/47866448-c56b2380-ddcc-11e8-8105-d9f1ac9d7563.png)


## 9. Configurar traducción de campos

Habilitar el soporte multi-lenguaje con field translation en todos los tipos de
contenido.

**Admin » Estructura » Tipos de contenido » Articulo » Editar**

URL: `admin/structure/types/manage/article`

**Admin » Estructura » Tipos de contenido » Basic Page » Editar**

URL: `admin/structure/types/manage/page`

Sección: Opciones de publicación

![soporte-multilenguaje](https://user-images.githubusercontent.com/243532/47867249-fb110c00-ddce-11e8-9fcd-8aa29ef0eb6c.png)

## 10. Configurar modulo _Title_

Habilitar traducción de los Títulos de contenido.

El campo del Titulo es un caso especial en Drupal 7. _Se utiliza el modulo
[Title][4] para convertir el campo en algo que se puede traducir con Entity
Translation como los otros campos._


**Admin » Configuración » Autoría del contenido » Opciones de título**

URL: `admin/config/content/title**`


![Node Title automatic field replacement](https://user-images.githubusercontent.com/243532/47866466-d451d600-ddcc-11e8-8a96-7d4ffbc04034.png)

![Term Name automatic field replacement](https://user-images.githubusercontent.com/243532/47866558-1d098f00-ddcd-11e8-97fc-c6e960f13ae7.png)


Reemplazar todos los campos de **titulo** en todos los contenidos:

**Admin » Estructura » Tipos de contenido » Articulo » Gestionar Campos**

URL: `admin/structure/types/manage/article/fields`

![remplazar campos article](https://user-images.githubusercontent.com/243532/47866570-2266d980-ddcd-11e8-870a-e1b92114e73e.png)

Reemplazar los campos del **Nombre** y **Descripción** de Taxonomía:

URL: `admin/structure/taxonomy/tags/fields`

![Reemplazar campos taxonomia](https://user-images.githubusercontent.com/243532/47866579-25fa6080-ddcd-11e8-8d43-4f77a6761b5e.png)

Comprobar que la traducción del campo esta habilitada.

admin/structure/taxonomy/tags/fields/name_field
admin/structure/taxonomy/tags/fields/description_field

![tags translation](https://user-images.githubusercontent.com/243532/47866583-2a267e00-ddcd-11e8-8153-1c62975b84e2.png)

## 11. Traducir campos

Habilitar traducción del campo de **body** en **todos los tipos de
contenido** (Article y Basic Page).

**Admin » Estructura » Tipos de contenido » Articulo » Gestionar Campos**

URL: `admin/structure/types/manage/article/fields`

![habilitar traduccion de campos](https://user-images.githubusercontent.com/243532/47866590-2eeb3200-ddcd-11e8-9bc7-f5d1093069e4.png)

**Admin » Estructura » Tipos de contenido » Page » Gestionar Campos**

URL: `admin/structure/types/manage/page/fields`

![body_field-translation](https://user-images.githubusercontent.com/243532/47866596-33174f80-ddcd-11e8-8aa6-f047cd5ca83f.png)

**No habilita** traducción para los campos:
Tags e Imagen.


## 12. Crear y revisar contenido!

URL: `/node/add/article`

![crear-articulo](https://user-images.githubusercontent.com/243532/47866602-390d3080-ddcd-11e8-8caf-ccdcff0c3f7b.png)

![articulo-espanol-untranslated-tag](https://user-images.githubusercontent.com/243532/47866607-3d394e00-ddcd-11e8-9c43-a6bdd1585828.png)


## 13. Traducir etiquetas de los campos

Si mostras las etiquetas de campos como "Tags:" en el Front-end, tienes que
traducirles con el modulo _Field Translation_ (i18n_field)

**Admin » Estructura » Tipos de contenido » Article » Gestionar campos » Tags » Traducir**

URL: `admin/structure/types/manage/article/fields/field_tags/translate`

![translate-field-label](https://user-images.githubusercontent.com/243532/47866611-41656b80-ddcd-11e8-81a4-f3812ef84a93.png)

¡Ahora sí!

![articulo-espanol](https://user-images.githubusercontent.com/243532/47866617-45918900-ddcd-11e8-8d74-a7570e5ad42f.png)

![translate-english](https://user-images.githubusercontent.com/243532/47866625-49251000-ddcd-11e8-85d0-742263160cb2.png)

![english](https://user-images.githubusercontent.com/243532/47866627-4cb89700-ddcd-11e8-8b92-16415ebf6411.png)

## 14. Traducir términos

**Admin » Estructura » Taxonomía » Lista**

URL: `admin/structure/taxonomy/tags`

![tags-edit](https://user-images.githubusercontent.com/243532/47866628-504c1e00-ddcd-11e8-940e-25ff238fb2f3.png)

![tags-traducir](https://user-images.githubusercontent.com/243532/47866633-53dfa500-ddcd-11e8-8529-6955be97abfa.png)

## 15. Traducir variables (Site Name, Slogan, etc):

**Admin » Configuración » Regional e idioma » Multilingual settings » Variables**

URL: `admin/config/regional/i18n/variable`

![traducir-variables](https://user-images.githubusercontent.com/243532/47866636-57732c00-ddcd-11e8-98e3-3436662138f6.png)

**Admin » Configuración » Sistema » Información del sitio**

URL: `admin/config/system/site-information`

![variables-multi-idioma](https://user-images.githubusercontent.com/243532/47866643-5b9f4980-ddcd-11e8-9bce-29af1e7370fc.png)


## 16. Menus

Escoger una metodologia para traducción de los menus.

**SI: Un solo menu, con links duplicados para todas las idiomas.**
NO: Multiples menus, uno para cada lenguaje.
Habilita i18n_menu, i18n_translation.

**Admin » Estructura » Menús » Menú principal » Editar menú**

URL: `admin/structure/menu/manage/main-menu/edit`

![menu-translation](https://user-images.githubusercontent.com/243532/47866647-5e9a3a00-ddcd-11e8-9a66-33f550a4961d.png)

Cada enlace debe tener una idioma:

![menu-idioma](https://user-images.githubusercontent.com/243532/47866656-62c65780-ddcd-11e8-8d67-4cfe8b2e7b30.png)

Debes traducir y vincular cada enlace en cada idioma.

![traducir-menu](https://user-images.githubusercontent.com/243532/47866660-66f27500-ddcd-11e8-8d08-1ee37dc1655f.png)

## 17. Bloques

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

## 18. Views

Views no require modificación con Entity Translate, pero por defecto si un nodo
no tiene traducción, se mostrará el contenido en la idioma madre (source
language).

Para quitar el contenido que no ha sido traducido de tus vistas para no tener
contenido mezclado, puedes usar un filtro:

**Contenido: Idioma > El idioma del usuario actual**

![views-multilenguaje-config](https://user-images.githubusercontent.com/243532/47866666-6bb72900-ddcd-11e8-9340-fc85f8583311.png)

![views-multilenguaje](https://user-images.githubusercontent.com/243532/47866679-6fe34680-ddcd-11e8-9fdf-d51fdf34f5ca.png)


## 19. Actualizar traducciones

**Admin » Configuración » Regional e idioma » Traducir interfaz » Actualizar**

URL: `admin/config/regional/translate/update`

A veces, al habilitar un modulo, no se descarga las traducciones
automáticamente. Debes actualizar las traducciones manualmente de tiempo a
tiempo, para estar al día con las traducciones del interfaz, contribuido por la
comunidad.

![translation-update-views1](https://user-images.githubusercontent.com/243532/47866684-740f6400-ddcd-11e8-9c5f-4e8438df0293.png)

![translation-update-views2](https://user-images.githubusercontent.com/243532/47866690-783b8180-ddcd-11e8-9956-11f82404995a.png)

![translation-update-views3](https://user-images.githubusercontent.com/243532/47866699-7b367200-ddcd-11e8-8122-85f3d07a1ba0.png)

![translation-update-views4](https://user-images.githubusercontent.com/243532/47866703-7d98cc00-ddcd-11e8-8102-060cd0984b13.png)


## 20. Buscar y traducir interfaz

**Admin » Configuración » Regional e idioma » Traducir interfaz » Traducir**

URL: `admin/config/regional/translate/translate`


## Otros módulos

*   [Localization Client][5] (l10n_client) -
    Facilita traducción de cadenas de texto del interfaz en tu sitio y
    contribución de los mismos al localize.drupal.org
*   [Transliteration][6] -
    convierte caracteres UTF8 a ASCII á => a, é => e etc. Bueno para URLs y
    para renombrar archivos que tengan caracteres extraños.
*   [Administration Language][7] (admin_language) -
    Cuando uno va a traducir el contenido de un nodo, el interfaz de
    administración se cambia al lenguaje del destino. Usar este modulo para
    dejar el backend en tu lenguaje preferida.

[1]: https://www.drupal.org/project/i18n
[2]: https://www.drupal.org/node/2227523
[3]: https://www.drupal.org/project/variable
[4]: https://www.drupal.org/project/title
[5]: https://www.drupal.org/project/l10n_client
[6]: https://www.drupal.org/project/transliteration
[7]: https://www.drupal.org/project/admin_language
