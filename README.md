# Clase 7 → Miércoles 18 de abril

### SVG

SVG es un elemento HTML. También es un dialecto, con [sus propios elementos](https://developer.mozilla.org/es/docs/Web/SVG/Element#Categories) y correspondientes atributos: 

```
<svg width="100" height="100" style="background:#CCCCCC">
	<circle cx="50" cy="50" r="25" fill="#FF0000" fill-opacity="0.25"/>
</svg>
```

Algunos de los atributos en el ejemplo son viejos conocidos, porque son atributos en elementos HTML (`width`, `height`, `style`), pero hay otros que son atributos en elementos SVG (`cx`, `cy`, `fill`, `fill-opacity`). Entre los atributos recién mencionados, algunos son atributos específicos del elemento `circle`, porque son requerimientos mínimos para dibujarlo (`cx`, `cy`, `r`). Los demás (`fill`, `fill-opacity`) son atributos globales, que podemos usar tanto en [este elemento](https://developer.mozilla.org/es/docs/Web/SVG/Element/circle) como en otros.

### D3.js

[D3.js (Data-Driven Documents)](https://d3js.org/) es una biblioteca de JavaScript, que nos simplifica el trabajo con datos y nos permite crear visualizaciones trabajando con **SVG, HTML y CSS**.

Podrían recordar (o [revisar](https://github.com/profesorfaco/dno037-2018-05/blob/gh-pages/ej_people_2.html)) como podíamos "agregar" ítems dentro de una lista de identidad astronautas, según los datos contenidos en un JSON que está actualizándose, constantemente, en línea. El script tenía que decir más o menos así:

```
var request = new XMLHttpRequest();
request.open('GET', 'http://api.open-notify.org/astros.json', true);
request.onload = function () {
	var data = JSON.parse(this.response);
	var count = data.number;
	function Creada(n) {
		var que = [];
		var donde = document.getElementById('astronautas');
		for (var x = 0; x < n; x++) {
			que[x] = document.createElement('li');
			que[x].textContent = data.people[x].name;
			donde.appendChild(que[x]);
		}
	};
	Creada(count);
}
request.send();	
```

**Ya dijimos que D3.js es una biblioteca de JavaScript que simplifica el trabajo con datos**. Para probarlo, favor revisen el siguiente script, que hace exactamente lo mismo que el anterior:

```
d3.json("http://api.open-notify.org/astros.json").then(function(data) {
	var astros = d3.values(data.people);
	d3.select("#astronautas").selectAll("li").data(astros).enter().append("li").text(function(d) { return d.name });
})
```

Pueden notar que voy por el json, para luego, en caso que se cargue ({crear una variable que toma parte de esa data; luego selecciono la identidad de la lista , y todos los ítem en ella, los que irán creándose en la medida que sean necesarios para escribir cada dato en la variable)}.

**También dijimos que D3.js trabaja con SVG**. Para probarlo, crearé, mediante un script, un SVG de 100 de ancho y 100 de alto, con un color de fondo gris. Dentro suyo, incluiré un círculo con un centro a 50 pixeles del borde izquierdo y 50 del borde superior, con un radio de 25 pixeles. Este círculo será de color rojo, con una opacidad del 25%.

```
d3.select("body").append("svg").attr("width",100).attr("height",100).style("background-color","#CCCCCC").append("circle").attr("cx",50).attr("cy",50).attr("r","25").attr("fill","#FF0000").attr("fill-opacity",0.25)
```
Así como puedo ir a buscar los nombres de los astronautas en el espacio, y puedo crear un SVG que contenga un círculo con determinados atributos, bien puedo crear un varios de elementos SVG, cada uno con sus atributos asignados desde determinados datos. Esa es la base con la que se puede crecer para crear visualizaciones de datos tan completas como las que pueden encontrar en la [galería oficial de ejemplos de D3.js](https://github.com/d3/d3/wiki/Gallery)

### Referencias

- [D3 — Scott Murray — alignedleft](http://alignedleft.com/tutorials/d3)
- [D3 Basics](https://website.education.wisc.edu/~swu28/d3t/concept.html)
- [D3 in Depth](http://d3indepth.com/)
- [D3.js Tutorials - Learn D3.js Step by Step](http://www.tutorialsteacher.com/d3js/)
- [INTRO TO D3.JS](https://square.github.io/intro-to-d3/)

Cuando usen estas referencias, favor revisen la versión de D3.js en uso. Entre las versiones hay cambios: https://github.com/d3/d3/blob/master/CHANGES.md 

- - - - - - - - - 

[Clase anterior](https://github.com/profesorfaco/dno037-2018-06) | [Siguiente clase](https://github.com/profesorfaco/dno037-2018-08)
