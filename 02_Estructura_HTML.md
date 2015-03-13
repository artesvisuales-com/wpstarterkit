## Estructura HMTL ##

### Estructura del código html. ###
AHORA ESTAMOS EMPEZANDO a entrar en la verdadera esencia de WordPress el desarrollo del tema: la estructura de codificación HTML

Un elemento fundamental antes de realizar un tema para wordpress es pensar cual es la estructura html óptima para el mismo. Como es lógico cada diseñador puede tener una, pero nuestra idea es aportar un esquema básico de diseño.

Para ello utilizamos el menor número posible de etiquetas con la idea de crear un código limpio que podamos reutilizar en cualquiera de nuestros diseños.

No se trata tanto de crear un “diseño”, sino un contenedor que pueda dar forma ordenada y limpia  al código, de modo que podamos recuperarlo fácilmente.

Para conseguirlo utilizamos id y class como elementos semánticos y estructurales. Expliquemos esto.
SIn duda has visto etiquetas div en el código de páginas web y en otras plantillas de wordpress. Piensa en ellas como contenedores de información que puede ser formateada mediante html y css. Lo mismo sucede con las etiquetas class.

La diferencia entre ambas desde mi perspectiva es que los div los utilizamos como elementos que definen la estructura, y las class como recursos de formato que podemos utilizar de forma recurrente.

Vamos a trabajar con ambos elementos desde una perspectiva de economía, utilizaremos los menos posibles, aquellos que tengan sentido en un código límpio y reutilizable, que pueda ser enriquecido a posteriori, o que simplemente sirva de contenedor para recuperar las etiquetas que utilizaremos en otros diseños.

Echemos un vistazo a la estructura HTML que vamos a utilizar para el cuerpo de nuestro tema de WordPress.
En todo caso es una buen idea copiar este código, que define la estructura de el tema de wordpress que vamos a crear, en tu editor de texto y guardarlo en algún lugar a mano.

Vamos a usarlo más tarde, cuando construyamos la estructura de archivos para nuestro tema de WordPress. Pero antes de hacer eso, hay algunas cosas que debemos ver del código siguiente.

En primer lugar, el atributo de clase hfeed. hfeed es parte del esquema de microformatos hAtom . La adición de esa clase hfeed a nuestra página, le dice a las distintas máquinas que visitan nuestro sitio como los robots de los buscadores, o algún otro servicio, que nuestro sitio publica el contenido sindicado, como entradas de blog. Y esto tiene una importancia que veremos a lo largo del tema.

En cuanto al div para el encabezado lo he divido en dos div para poder estructurar la información con más detalle. Lo mismo podría haber hecho en el caso del footer, pero he optado por simplificarlo.
En el área principal de nuestro HTML tenemos dos columnas dentro de un div contenedor de modo que cambiando alguno de los atributos del css podemos tener el contenido a la izquierda o derecha de la página.

Hemos optado por dos columnas para simplificar la estructura contenedora.

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html>
 
<head>
<title>Layout</title>
<meta http-equiv="content-type" content="text/html;charset=utf-8" />
 <link rel="stylesheet" type="text/css" href="styles/layout.css" />
</head>
 
<body>
 
<div id="pagewidth" class="hfeed">
 
	<div id="header"><h2>Head</h2>
		<div id="branding"> </div><!– #branding –> 
		<div id="access"> </div><!– #access –> 
	</div> <!– #header –>
 
	<div id="wrapper" class="clearfix">
 
		<div id="twocols"> 
			<div id="maincol"><h1>Main Content Column</h1></div>
			<div id="rightcol"> <h2>right Column</h2></div>
		</div> <!– #twocols –> 
 
	</div> <!– #wrapper –> 
 
	<div id="footer"><h2>Footer</h2></div>
 
</div> <!– #pagewidth –> 
 
</body>
</html>
```