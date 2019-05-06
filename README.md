# FRON END MAGENTO

## Theme structure

ubicacion:
`app/design/frontend/<Vendor>/`

`<Vendor>` es el nomnbre del tema.

Luma es el tema que trae magento por defecto igual que el blank, pero este ultimo es el base:

`vendor/magento/theme-frontend-luma`

`vendor/magento/theme-frontend-blank`


Cada distribuidor de temas puede tener diferentes temas, y los puedes agrupar por el mismo distribuidor:
`app/design/frontend/<Same_Vendor>/theme1`
`app/design/frontend/<Same_Vendor>/theme2`
`app/design/frontend/<Same_Vendor>/theme3`

Estructura del tema de magento 2.0

* < theme_dir>/
    - < Vendor>_< Module>/
        - web/
        - css
            - source/
        - layout/
            -override
        - templates/
    - etc/
    - i18n/
    - media/
    - web/
        - css/
            - source/
        - fonts/
        - images/
        - js/
    - composer.json
    - registration.php
    - theme.xml

    ***< Vendor_module>*** : modulos o funcionalidades de su theme

    Las funcionalidades del tema de magento Luma se puede ver diferentes modulos en `vendor/magento/theme-frontend-luma`.

    La estructura de magento tiene tres archivos principales para administrar el comportamiento del tema: 
    * ***composer.json*** este archivo describe las dependencias y la meta información
    
    * ***registration.php*** archivo encargado de registrar tu tema

    * ***theme.xml*** este archivo declara el tema en el sistema y es usado por el tema sistema de magento para organizar el tema.


Los archivos del sistema pueden ser divididos en dos, en archivos de vistas estaticas y archivos de vistas dinamicas. Los archivos de vistas estaticas no son procesadas por el servidor (images, font y .js) y los dinamicos son procesados por el servidor antes de entregarle el contenido al usuario ( template y layout)

Los archivos estaticos generalmente se publican en alguno de estas carpetas:
`/pub/static/frontend/<Vendor>/< theme>/< language>` <br>
`< theme_dir>/media/` <br>
`< theme_dir>/web`

## EL TEMA MAGENTO LUMA

Tema que viene con la versión 2.0 de magento que implementa practicas RESPONSIVE WEB DESIGN (RWD).

Esta basado en las librerias de magento user interface y usa CSS3 media queries para trabajar con el ancho, adaptando el layout de acuerdo a dispositivos que accedan.

**Magento UI** es una gran caja de herramienta para el desarrollo de temas, contiene:

* The actions toolbar.
* Breadcrumbs.
* Buttons.
* Drop-down menus.
* Forms.
* Icons.
* Layout.
* Loaders.
* Messages
* Pagination.
* Popups.
* Ratings.
* Sections.
* Tabs and accordions.
* Tables.
* Tooltips.
* Typography.
* A list of theme variables.

Este a su vez usa carasteristicas del blank themes para ser funcional.
`vendor/magento/theme-frontend-blank`

Esto se realiza por medio de la `herencia`.

## HERENCIA EN TEMAS DE MAGENTO

El frontend de magento permite diseñar para crear nuevos temas basados en el tema blank básico, reusando el codigo principal sin cambiar su estructura. El sistema de retroceso tiene un mecanismo de herencia y permite desarrollar para crear solo los archivos que son necesarios para la personalización.

Por ejemplo el tema LUMA, usa el sistema de retroceso (fallbacks) para heredar la estrucutra básica del tema blank. El tema luma se declara de la siguiente manera:

```xml
    <theme xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNam
    espaceSchemaLocation="urn:magento:framework:Config/etc/theme.xsd">
        <title>Magento Luma</title>
        <parent>Magento/blank</parent>
        <media>
            <preview_image>media/preview.jpg</preview_image>
        </media>
    </theme>
```

```php
<?php
/**
* Copyright � 2015 Magento. All rights reserved.
* See COPYING.txt for license details.
*/
\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::THEME,
    'frontend/<Vendor>/<theme>',
    __DIR__
);
```

Se puede crear un tema usando uno ya existente (parents) y por reemplazo (overriding) un archivo existente con el mismo nombre pero en su folder de tema.

Por ejemplo crea un nuevo tema en `app/design/frontend/<Vendor>/<theme>/` y declaras `Magento/blank` como su tema padre, el archivo `theme.xml` y `registration.php`, tienes las estructura entera del tema blank lista para tu nuevo tema, incluyendo el diseño y estilos RWD.

Si necesita un archivo y no esta en el tema hijo, lo va a buscar en el tema padre, pero en el caso que si existiese en el hijo no va hasta el padre, se queda con el hijo.

# CMS BLOCKS AND PAGES

Magento tiene un sistema flexible de temas. Desde el backend del admin se puede crear bloques y contenido. Se puede crear Home, Page, About us, u otra página estatica. Se puede da la oportunidad de embeber HTML en tu página.

Se ubica ***Content | Pages***

## Variables personalizables

Son piezas de HTML que continen valores especificos como variables programables. Para crear un variable personalizables, tu puedes aplicarlo a multiples areas de tu sitio. Un ejemplo de la estrucutura de la personalización se muestra aquí:

`{{config path="web/unsecure/base_url"}}`

Esta variable muestra la URL de la tienda.

Ahora vamos a crear una variable personalizable para ver como trabaja:

1. En el administrador ir a `System | Custom Variables`.
2. click en el boton `Add new Variables`.
3. En el campo Variable code, ingrese la variable en lowercase sin espacios. Ejemplo: `dev_name`
4. Ingrese el nombre de la variable, el cual explica el proposito de la variable.
5. Ingrese el HTML y valores texto plano en de las variables personalizables en `Variables HTML values` and `Variables Plain Value` y guardalo.

Ahora, nostros tenemos un variable personalizada que almacena un dato que puede ser algo como el nombre del desarrollador o el telefono de contacto. Usemosla dentro de cualquier página, puede ser el `Content | Pages` elegimos la pagina y en el codigo ingresamos algo como esto:

`{{CustomVar code = "<variable_code>"}}`

luego guardas y el valor se va a visualizar en el contenido de la página.

# CREANDO UN TEMA BASICO DE MAGENTO 2.0

Para crear una estructura de un tema básico:
1. Crear un nuevo distribuidor de temas: `<Magento root directory>/app/design/frontend/<Vendor>`
primera letra en máyuscula.

2. Dentro de esta carpeta crea el directorio del tema basico: `<Magento root directory>/app/design/frontend/<Vendor>/<tema>`

quedaria algo así:
`<Magento root directory>/app/design/frontend/Empresa/basic`

El siguiente paso es declarar la información para Magento lo reorganice como un nuevo tema. 

1. En tu editor preferido.
2. Crea un archivo llamado `theme.xml`
`<Magento root directory>/app/design/frontend/<Vendor>/<tema>/theme.xml`
3. Así seria el codigo:

```xml
<theme xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:n
oNamespaceSchemaLocation="urn:magento:framework:Config/etc/theme.
xsd">
    <title>nombre_del_tema</title>
    <!-- nombre del tema padre -->
<parent>Magento/blank</parent>
<!-- <media>
    <preview_image>media/preview.jpg</preview_image>
</media>-->
</theme>
```

Esta es una declaración básica del sistema de magento para reorganizar nuestro tema como un tema oficial. La imagen preview no es obligatoria, pero si se quiere usar se descomenta las etiquetas `<media>`


Ahora vamos a registrarlo:

1. editor
2. Crea archivo `registration.php` en el mismo directorio.
3. ingresa el siguiente codigo en `registration.php`

```php
<?php
/**
* Copyright © 2016 Magento. All rights reserved.
* See COPYING.txt for license details.
*/
\Magento\Framework\Component\ComponentRegistrar::register(
\Magento\Framework\Component\ComponentRegistrar::THEME,
'frontend/Nombre_del_vendor/nombre_del_tema',
__DIR__
);
```

Este codigo registra el tema de magento

## Configuración simple de imagen de producto

En tu tema, tu puedes configurar las propiedades de los productos en el MAGENTO CATALOG module creando el archivo `view.xml`. Tu puedes controlar esto con la configuración especifica usando el atributo id de cada producto con los elementos HTML5:

1. Editor.
2. Crea un nuevo directorio llamado `etc` dentro del tema 
3. Crea un archivo llamado `view.xml` dentro de `etc`(`<Magento root directory>/app/design/frontend/<Vendor>/<tema>/etc/view.xml` ).
4. Usa el siguiente codigo en view.xml y guarda el archivo:

```xml
<image id="category_page_grid" type="small_image">
    <width>250</width>
    <height>250</height>
</image>
```

Aquí declaramos el ancho y el alto de la imagen de producto.
El id y el tipo especifica el tipo de imagen que sus reglas seran aplicadas.

## Creando 