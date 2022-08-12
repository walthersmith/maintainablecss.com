---
id: semantics
number: 2
title: Semántica
permalink: /chapters/semantics/
description: Por que nombrar algo basado en lo que es, en lugar de como luce o se comporta, este es el fundamento de un CSS bien diseñado y mantenible 
next:
  text: Reutilizar
  href: /chapters/reuse
---
Un HTML semantico no es solo sobre los elementnos que usamos,  es obio que deberiamos usar `<a>` para links, `<table>` para tabular datos  y `<p>` para parrafos etc. Lo que es menos obio son los nombres que usamos para las clases.

Como Phil Karton dice, “there are only two hard things in Computer Science: cache invalidation and **naming things**.” ("Solo hay 2 cosas dificiles en Ciencias de la computacion: validacion de cache y **nombrar cosas**."), hablar de todos un capitulo sobre como nombrar cosas es esencial. 

Nombrar es el aspecto mas importante de escribir CSS mantenible. Existen dos enfoques: El enfoque semantico  y el enfoque no semantico. 

## Semantico vs no-semantico

	<!-- non semantic -->
	<div class="red pull-left pb3">
	<div class="grid row">
	<div class="col-xs-4">

	<!-- semantic -->
	<div class="basket">
	<div class="product">
	<div class="searchResults">

Las clases No semanticas  no transmiten *que*  elemento replecentan, como mucho te daran una idea de  como *luce* el  elemento. Atomico, visual, conductual y clases de utilidad  todas son formas no semanticas.

La clases no semanticas no transmiten sus estilos (su forma de representacion), pero eso esta bien, para eso es el CSS. Las clases semanticas significan algo para HTML, CSS, Javascript y test funcionales automaticos. 

Veamos porque las clases semanticas usualmente funcionan mejor.  

## 1. Porque son legibles 
Este es un trozo de Html  usando  clases Atómicas:  

	<div class="pb3 pb4-ns pt4 pt5-ns mt4 black-70 fl-l w-50-l">
	  <h1 class="f4 fw6 f1-ns lh-title measure mt0">Heading</h1>
	  <p class="f5 f4-ns fw4 b measure dib-m lh-copy">Tagline</p>
	</div>

- Las palabras son geneneralmente faciles de entender,  que las abreviaciones que tienen que ser entenedidas e interpretadas antes de saber que significan.
- No es claro donde inicia y termina el módulo
- Las clases  carecen de claridad por ejemplo, no es claro si `black-70` hace referencia al color del primer plano o al color de fondo 
- El contenido se encuentra ofuscado por la gran cantidad de HTML al rededor 
- El HTML es grande en tamaño 

Este es el mismo HTML con clases semanticas:

	<div class="hero">
	  <h1 class="hero-title">Heading</h1>
	  <p class="hero-tagline">Tagline</p>
	</div>

- Estas clases son faciles de leer sin la necesidad de ser interpretadas
- Es claro don de inicia y termina el modulo 
- El CSS es facil de leeer por que usa un sintaxis estandard para este proposito
- El contenido ya no esta ofuscado. 
- El html tiene la mitad de tamaño 

## 2. Porque hacen facil la construccion de sitios responsivos
Imagina codificar una grilla de dos columnas por lo cual: 
* cada columnas tiene de padding `20px` y `50px` en pantallas pequeñas y grandes respectivamente
* cada columna tiene un tamaño de fuente de `2em` y `3em` en pantallas pequeñas y grandes respectivamente
* Las pilas de columnas en pequeñas pantallas. tengamos en cuenta que ahora *column*  es un nombre engañoso para un nombre de clase. 

Con clases no semanticas esto luciria de esta forma:

	<div class="grid clearfix">
	  <div class="col pd20 pd50 fs2 fs3">Column 1</div>
	  <div class="col pd20 pd50 fs2 fs3">Column 2</div>
	</div>

- Hay 7 clases algunas de las cuales se sobreescriben unas a otras 
- Para hacer que las columnas funcionen de forma responsiva tenemos neceditariamos  una clase `fs3largue` que significa crear una convension de nombres que recree las ya provistas por CSS
-En algunos puntos de ruptura, las clases pueden ser engañosas  y deduntantes-por ejemplo `.clearfix` nno limpia en pantallas pequeñas 

-Con clases semantias luciria de esta forma: 

	<div class="thing">
	  <div class="thing-thingA"></div>
	  <div class="thing-thingB"></div>
	</div>

- Las clases estan encapsuladas al diseno y contenido del modulo
- Es facil dar estilos a los elementos sin tener que escribir multiples clases  y cambiar el HTML 
- Las clases tienen  significado en pequeñas y grandes pantallas 
- los `media queries` pueden ser usados para limpiar elementos que se necesiten. 


> Pregunta: Que tan valioso es un sistema de grillas codificado? Un [diseño debe adaptarse al contenido](http://adamsilver.io/articles/stop-using-device-breakpoints/), y no al revés.

## 3. Porque son faciles de buscar
## 3. Because they're easier to find

Buscar HTML con clases no-semanticas arroja muchos resultados. Buscar HTML  con clases semasnticas deberia dar un resultado y y seria mas facil de ubicar.

Searching HTML with non-semantic classes yields many results. Searching HTML with semantic classes should yield one result which makes it quick to track down.

## 4. Porque reducen la probabilidad de regresion 

Actualizar una clase no semantica puede provocar una regresion  a traves de multiples elementos. actualizar una clase semantica solo aplica al modulo especifico,  elimianando el riesgo de regresion. 
 
## 5. Porque las clases visuales no son necesariamente valiosas 

`Atomic CSS` y `inline CSS` no son totalmente equivalentes. Por ejemplo, `inline CSS` no puede usar `media queries` y diseñar en el HTML nos inmpide  almacenarlo en cache. 

Atomic CSS and inline CSS aren't totally equivalent. For example, inline CSS can't use media queries and styling in HTML stops us from being able to cache it.

But, in some ways we may as well use inline styles—at least it's explicit and reduces the CSS footprint to zero.

> Question: isn't `.red` the exact same abstraction that CSS already gives us for free with `color: red`?

## 6. Because they provide hooks for automated tests

Automated functional tests work by searching for and interacting with elements. For example, a test might involve:

1. clicking a link
2. finding a text box
3. typing in text
4. submitting a form
5. verifying some criteria

We can't use non-semantic classes to target specific elements. And adding hooks specifically for tests is wasteful as the user now has to download extra code.

## 7. Because they provide hooks for JavaScript

We can't use non-semantic classes to target specific elements in order to enhance them with JavaScript.

## 8. Because they need less maintaining

When you name an element based on what it is, you don't have to update the HTML. That's because, a heading, for example, is always a heading, no matter what it looks like.

With visual classes, both the HTML and the CSS need updating—assuming there aren't any selectors available for use.

## 9. Because they're easier to debug

Inspecting an element with multiple atomic classes, means having to wade through many selectors. With a semantic class, there's only one which is much easier to work with.

## 10. Because the standards recommend it

On using the class attribute, HTML5 specs say in 3.2.5.7:

> "[...] authors are encouraged to use values that describe the nature of the content, rather than values that describe the desired presentation of the content."

## 11. Because styling state is easier

Consider this HTML:

	<a class="padding-left-20 red" href="#"></a>

Changing the padding and colour on hover is a difficult task. Try to avoid having to fix self-induced problems like this.

## 12. Because they produce a small HTML footprint

Atomic classes create extra code in HTML. Semantic classes result in less code. And while the CSS may increase in size, it can be cached.

## Final thought

Semantic classes are a cornerstone of MaintainableCSS. Without them, everything else makes little sense. Name something based on what it is and everything else falls into place.