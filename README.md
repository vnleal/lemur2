# HTML, SVG y CSS

### Clase 2 → 23-11-2021

- - - - - - - 

## Presentación

Ya aprendimos que **HTML (HyperText Markup Language) es un lenguaje estándar que describe la estructura de las páginas web (qué es lo que contiene la página)**. Este se complementa con otro lenguaje estándar, el **CSS (Cascading Style Sheets) que describe la presentación de las páginas web (cómo se muestra lo que contiene la página)**. 

Ahora corresponde aprender algo sobre un "primo hermano" de HTML: El **SVG (Scalable Vector Graphics)**. 

Con este lenguaje se describen gráficos vectoriales (qué formas los componen y cuáles son sus atributos). 

En los gráficos vectoriales podemos encontrarnos con lineas rectas, líneas quebradas, círculos, elipses, rectángulos, polígonos simples y trazados complejos, formas que serán descritas con los atributos correspondientes a su geometría:

```
<line x1="0" y1="0" x2="200" y2="200" />

<polyline points="20,20 40,25 60,40 80,120 120,140 200,180" />

<circle cx="50" cy="50" r="40" />

<ellipse cx="50" cy="50" rx="30" ry="50" />

<rect width="50" height="50" />

<polygon points="200,10 250,190 160,210" />

<path d="M150 0 L75 200 L225 200 Z" />
```

Estas formas también pueden ser afectas mediante CSS, con propiedades particulares, distintas de las que afectan al hipertexto (del HTML), así, por ejemplo, podría agregar la clase `enrojecido` como atributo en un círculo, y este se pintaría de rojo: 

```
.enrojecido{
  fill: red;
}
```

No confundamos las propiedades `fill` y `background`; la primera pueden afectar a elementos gráficos en el SVG, mientras que las segunda puede afectar a elementos HTML.

Esta regla de CSS podría afectar al elemento gráfico si se incrusta, vincula o importa en la cabeza del documento HTML que contendrá al SVG, y también lo puede afectarlo si se le incluye dentro del mismo SVG:

```
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous" />
        <title>Primer ejemplo</title>
    </head>
    <body>
        <div class="container">
            <div class="row">
                <div class="col-12 my-4">
                    <svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100">
                        <style>
                            .enrojecido {
                                fill: red;
                            }
                            .enrojecido:hover {
                                fill: pink;
                                transform: scale(110%) translate(-5%, -5%);
                                transition: all ease 0.5s;
                                cursor: pointer;
                            }
                        </style>
                        <circle cx="50" cy="50" r="40" class="enrojecido" />
                    </svg>
                </div>
            </div>
        </div>
    </body>
</html>
```

En el ejemplo recién presentado tenemos dos reglas de CSS, la primera tiene como selector a cualquier elemento de clase "enrojecido" y la segunda tiene como selector a cualquier elemento de la misma clase para cuando el mouse le pasa por encima.

En el SVG tenemos un elemento gráfico de clase "enrojecido", que se ubica justo al centro, esto por sus atributos y los atributos del SVG; noten que el `circle` tiene su centro horizontal (`cx`) en 50 y su centro vertical (`cy`) en 50, mientras el `svg` tiene un ancho de 100 y alto de 100, que se mantienen  por su `viewBox`.

Cuando creamos un SVG con un editor de gráfica vectorial como Adobe Illustrator, en la revisión del código podrán encontrar un CSS que define las propiedades visuales de los elementos gráficos a través de selectores tales como `.st0`, `.st1`, `.st2`, etc. 

Conviene acotar que el código que resulta de guardar o exportar un SVG desde Adobe Illustrator no es tan pulcro (como veremos en un rato, dentro del *template* preparado), y podría limpiarse con el uso de algunas herramientas en línea: https://www.svgminify.com/ o https://jakearchibald.github.io/svgomg/

- - - - - - - 

## Exploración

Entre la gráfica vectorial descrita en el SVG podemos vincular gráficos rasterizados (imágenes de mapa de bits), para dibujar sobre ellos y/o enmascararlos. Lo clave es saber mantener el vínculo en algún lugar donde siempre pueda encontrarse. 

En el siguiente ejemplo podemos ver un documento HTML completo, que incluye, entre líneas, al SVG, y dentro de tal SVG se vincula a una imagen:

```
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
        <title>Segundo ejemplo</title>
    </head>
    <body>
        <div class="container">
            <div class="row">
                <div class="col-12 my-4">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 450" class="w-100">
                        <style type="text/css">
                            .enrojecido { fill: #cc0000; }
                        </style>
                        <image width="1600" height="900" xlink:href="https://picsum.photos/id/411/1600/900?grayscale" transform="matrix(0.5 0 0 0.5 0 0)" />
                        <polygon class="enrojecido" points="372 216 372 150 371 150 371 137 369 137 369 131 368 131 368 128 367 128 367 125 365 125 365 124 364 124 364 122 363 122 363 116 362 116 362 108 361 108 361 106 360 86 359 106 359 108 358 108 358 116 357 116 357 122 356 122 356 124 355 124 355 125 353 125 353 128 352 128 352 131 351 131 351 137 349 137 349 150 348 150 348 216 345 216 345 243 375 243 375 216 "
                        />
                        <text transform="matrix(1 0 0 1 366.2178 78.1255)">Empire State Building</text>
                    </svg>
                </div>
            </div>
        </div>
    </body>
</html>
````

Reemplazando la referencia de hypertexto (`href`) en `xlink:href="https://picsum.photos/id/411/1600/900?grayscale"`, podrían incluir una imagen ya preparadas para la versión impresa de su infografía, o podrían aprovechar el trabajo que ya hicieron en Illustrator o InkScape, cuidando mucho el orden (porque el código que se obtiene de tales programas es algo desordenado). 

¡Pero corresponde ajustar cada imagen para su uso en línea! Nunca CMYK, nunca 300 DPI, nunca más de 999kb de peso (ojalá un tercio de tal peso).

Los ajustes para el uso en línea puede hacerse con:

- https://helpx.adobe.com/es/photoshop-elements/using/optimizing-images.html

- https://tinypng.com/

- https://squoosh.app/

Para contar con más información sobre los ajustes:

- https://bluekea.com/blog/fotografia/cual-es-la-resolucion-correcta-para-fotografia-en-web 

- https://nbadiola.com/peso-ideal-fotografia-para-web/

- https://www.adslzone.net/como-se-hace/photoshop/guardar-imagen-para-web/

**Si ustedes incluyen en su infografía digital recursos para la infografía impresa: Abusarán de la transferencia de datos en la conexión a Internet de cada visitante. Esta transferencia puede demorar más de 5 segundos**:

- [Tienes 5 segundos](http://www.tienes5segundos.cl/) se llama un viejo clásico local sobre gestión de contenidos digitales. 

- [5-Second Usability Test](https://www.nngroup.com/videos/5-second-usability-test/) se llama una técnica que permite evaluar la primera impresión de un sitio web. 

**Si demora más de 5 segundos en cargar: ¡Esto no funciona, me voy a otro lugar!**.

- - - - - - - - -

En los ejemplos de **presentación** y **exploración**, el `SVG` está contenido entre líneas de `HTML`. Esto implica que se abre un espacio para que la descripción del gráfico vectorial en el mismo código fuente. Pero también podríamos tener esa descripción como un documento independiente, al que se vaya a buscar de la siguiente manera: 

```
<object data="grafica.svg" type="image/svg+xml"></object>
```
La ventaja de usar `object` es que su descripción puede ser afectada por el CSS del documento HTML, lo que ya no ocurre cuando se le usa como imagen:

```
<img src="grafica.svg" />
```

Y podrán encontrar una forma más de incluir gráfica de vectores en un documento HTML, que se puede ver como sigue: 

```
<img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100' height='100' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40'/%3E%3C/svg%3E">
```

Noten que se trata de un elemento HTML de imagen (`img`) en el que el atributo de recurso (`src`) incluye el SVG con un ajuste en las comillas, siempre simples entre dobles, y los signos `<` y `>`, que son reemplazados por`%3C` y `%3E` respectivamente.

Para esto último, se necesita un Codificador SVG a Base64, como https://yoksel.github.io/url-encoder/, https://codebeautify.org/svg-to-base64-converter o https://image2base64.online/

- - - - - - - 

## Aplicación

Como en la clase recién pasada, vamos a tomar el código fuente de la página https://profesorfaco.github.io/infografia/clase-2/

- - - - - - - -

###### [← CLASE PASADA](https://github.com/profesorfaco/infografia/tree/main/clase-1) — [CLASE SIGUIENTE →](https://github.com/profesorfaco/infografia/tree/main/clase-3) 
