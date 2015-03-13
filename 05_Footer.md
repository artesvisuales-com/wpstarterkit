## Footer.php ##

Es la parte de cierre de la página, su pie. Hay muchos, y algunos muy buenos, modos de cerrar la página y que muestran distintas informaciones.

Puedes inspirarte en páginas como esta para ver y determinar que tipo de información mostrar en este área, y como mostrarla.

http://webdesignledger.com/inspiration/35-inspiring-headers-and-footers

Nosotros ahora no vamos a complicarnos pero para hacernos una idea en el pie de la página podemos mostrar:

- Páginas.
- Categorías.
- Tag.
- RSS o enlaces recomendados.
- Citas y anuncios.
- Créditos y (c).
- Fotos.

Otro elemento que debemos incluir en el pie - bueno en las últimas versiones de analytics pide colocarlo antes del cierre de la etiqueta `</head>` - es el código de tracking para controlar los accesos a nuestra web. Hablo lógicamente de Analitycs.

Vamos a ello.

**Estructura html.**

```
	</div> <!– #wrapper –> 
 
	<div id="footer"><h2>Footer</h2></div>
 
</div> <!– #pagewidth –> 
 
</body>
</html>
```

Una vez definida su estructura html, la más simple posible y que tu puedes y debes enriquecer en tus trabajos profesionales, vamos a ir completando los datos.

Introducimos la información del sitio.

```
 <p class="small">
	Powered by <a href="http://wordpress.org/" title="WordPress">WordPress</a>  diseñado por <a href="http://fbtemplate.wordpress.com/" title="Example Web Design">fbtemplate</a>
	</p>
	<p><a href="feed:<?php bloginfo('rss2_url'); ?>"><img src="http://icons.iconarchive.com/icons/fasticon/web-2/16/Feed-icon.png" alt="RSS Feed Icon" />Posts RSS</a>
| <a href="feed:<?php bloginfo('comments_rss2_url'); ?>"><img src="http://icons.iconarchive.com/icons/fasticon/web-2/16/Feed-icon.png" alt="RSS Feed Icon" /> Comentarios RSS</a>
	</p>
```

El resultado es un línea en la parte inferior de cada página en la que podemos leer Powered by WordPress diseñado por fbtemplate. Lógicamente debemos personalizar el texto y link de diseñado por.

Otras opciones para mostrar información en el footer.

Podemos mostrar por ejemplo los feed tanto de los post como de los comentarios.

```
<div id="site-info">
	<p><a href="<?php bloginfo('name'); ?>" title="<?php bloginfo('name'); ?>"><?php bloginfo('name'); ?></a> is dedicated to blogging about blogging.</p>
	<p>Powered by <a href="http://wordpress.org/" title="WordPress">WordPress</a>  diseñado por <a href="http://fbtemplate.wordpress.com/" title="Fred Example Web Design">fbtemplate</a></p>
	<p><a href="feed:<?php bloginfo('rss2_url'); ?>"><img src="http://icons.iconarchive.com/icons/fasticon/web-2/16/Feed-icon.png" alt="RSS Feed Icon" />Posts RSS</a>
	| <a href="feed:<?php bloginfo('comments_rss2_url'); ?>"><img src="http://icons.iconarchive.com/icons/fasticon/web-2/16/Feed-icon.png" alt="RSS Feed Icon" /> Comentarios RSS</a>
	</p>            
    </div><!-- #site-info -->
```

Así además de la información del sitio mostramos sus enlaces rss.
￼
### Mostrando páginas y categorías. ###

Podemos listar ambos elementos con el siguiente código:

```
 <div id="site-info">	
	<p>
	<ul class="footerlinks">
	<?php wp_list_pages('title_li='); ?>
	</ul>
	<ul class="footerlinks">
	<?php wp_list_categories('title_li='); ?>
	</ul>
	Powered by <a href="http://wordpress.org/" title="WordPress">WordPress</a>  diseñado por <a href="http://fbtemplate.wordpress.com/" title="Fred Example Web Design">fbtemplate</a></p>
<p><a href="feed:<?php bloginfo('rss2_url'); ?>"><img src="http://icons.iconarchive.com/icons/fasticon/web-2/16/Feed-icon.png" alt="RSS Feed Icon" />Posts RSS</a>
| <a href="feed:<?php bloginfo('comments_rss2_url'); ?>"><img src="http://icons.iconarchive.com/icons/fasticon/web-2/16/Feed-icon.png" alt="RSS Feed Icon" /> Comentarios RSS</a></p>
     </div><!-- #site-info -->
```

Posiblemente no tenga mucho sentido mostrar aquí información que ya aportamos en el menú o el sidebar, pero podemos hacerlo. Incluso podemos sofisticar un poco más la información filtrando las páginas o categorías a mostrar.

Por ejemplo podemos sustituir `<?php wp_list_pages('title_li='); ?>`  por `<?php wp_list_pages( 'include=2,5,6&title_li=' ); ?>` de forma que solo se muestren estas páginas. Esto es muy interesante si queremos resaltar información concreta de la web dándole más visibilidad.

Lo mismo podemos hacer con las categorías si sustituimos `<?php wp_list_categories('title_li='); ?>` por `<?php wp_list_categories('orderby=name&include=2,14,19&title_li='); ?>` . El potencial de utilización y los resultados son los mismos que con las páginas pero con las categorías.

### Imágenes. Mejor dicho Flickr. ###

Puede ser que para el contenido del blog una galería sea importante, en el caso de un diseñador es fundamental.

Y si tenemos galería gráfica no hay mejor sitio que Flickr, de modo que el primer paso es hacerse un módulo en html y en horizontal.

Empieza con ello desde el siguiente link http://www.flickr.com/badge.gne

Una vez configurado obtenemos el código que será algo así:

```
<!-- Start of Flickr Badge -->

<style type="text/css">
#flickr_badge_source_txt {padding:0; font: 11px Arial, Helvetica, Sans serif; color:#666666;}
#flickr_badge_icon {display:block !important; margin:0 !important; border: 1px solid rgb(0, 0, 0) !important;}
#flickr_icon_td {padding:0 5px 0 0 !important;}
.flickr_badge_image {text-align:center !important;}
.flickr_badge_image img {border: 1px solid black !important;}
#flickr_www {display:block; text-align:left; padding:0 10px 0 10px !important; font: 11px Arial, Helvetica, Sans serif !important; color:#3993ff !important;}
#flickr_badge_uber_wrapper a:hover,
#flickr_badge_uber_wrapper a:link,
#flickr_badge_uber_wrapper a:active,
#flickr_badge_uber_wrapper a:visited {text-decoration:none !important; background:inherit !important;color:#3993ff;}
#flickr_badge_wrapper {background-color:#ffffff;border: solid 1px #000000}
#flickr_badge_source {padding:0 !important; font: 11px Arial, Helvetica, Sans serif !important; color:#666666 !important;}
</style>
<table id="flickr_badge_uber_wrapper" cellpadding="0" cellspacing="10" border="0"><tr><td><a href="http://www.flickr.com" id="flickr_www">www.<strong style="color:#3993ff">flick<span style="color:#ff1c92">r</span></strong>.com</a><table cellpadding="0" cellspacing="10" border="0" id="flickr_badge_wrapper">
<tr>
<script type="text/javascript" src="http://www.flickr.com/badge_code_v2.gne?show_name=1&count=3&display=latest&size=t&layout=h&context=in%2Fpool-digital-designer%2F&source=group&group=1497188%40N25"></script>
<td id="flickr_badge_source" valign="center" align="center">
<table cellpadding="0" cellspacing="0" border="0"><tr>
<td width="10" id="flickr_icon_td"><a href="http://www.flickr.com/groups/digital-designer/pool/"><img id="flickr_badge_icon" alt="elementos de alumnosartesvisuales" src="http://farm5.static.flickr.com/4148/buddyicons/1497188@N25.jpg?1287295769" align="left" width="48" height="48"></a></td>
<td id="flickr_badge_source_txt">Más <a href="http://www.flickr.com/groups/digital-designer/pool/">en el mural de alumnosartesvisuales</a></td>
</tr></table>
</td>
</tr>
</table>
</td></tr></table>
<!-- End of Flickr Badge -->
```

Y lo integramos en el footer.

```
<div id="site-info">	
	<p>
	<!-- Start of Flickr Badge -->
	<style type="text/css">
	#flickr_badge_source_txt {padding:0; font: 11px Arial, Helvetica, Sans serif; color:#666666;}
	#flickr_badge_icon {display:block !important; margin:0 !important; border: 1px solid rgb(0, 0, 0) !important;}
	#flickr_icon_td {padding:0 5px 0 0 !important;}
	.flickr_badge_image {text-align:center !important;}
	.flickr_badge_image img {border: 1px solid black !important;}
	#flickr_www {display:block; text-align:left; padding:0 10px 0 10px !important; font: 11px Arial, Helvetica, Sans serif !important; color:#3993ff !important;}
	#flickr_badge_uber_wrapper a:hover,
	#flickr_badge_uber_wrapper a:link,
	#flickr_badge_uber_wrapper a:active,
	#flickr_badge_uber_wrapper a:visited {text-decoration:none !important; background:inherit !important;color:#3993ff;}
	#flickr_badge_wrapper {background-color:#ffffff;border: solid 1px #000000}
	#flickr_badge_source {padding:0 !important; font: 11px Arial, Helvetica, Sans serif !important; color:#666666 !important;}
	</style>
	<table id="flickr_badge_uber_wrapper" cellpadding="0" cellspacing="10" border="0"><tr><td><a href="http://www.flickr.com" id="flickr_www">www.<strong style="color:#3993ff">flick<span style="color:#ff1c92">r</span></strong>.com</a><table cellpadding="0" cellspacing="10" border="0" id="flickr_badge_wrapper">
	<tr>
	<script type="text/javascript" src="http://www.flickr.com/badge_code_v2.gne?show_name=1&count=5&display=latest&size=t&layout=h&context=in%2Fpool-digital-designer%2F&source=group&group=1497188%40N25"></script>
	<td id="flickr_badge_source" valign="center" align="center">
	<table cellpadding="0" cellspacing="0" border="0"><tr>
	<td width="10" id="flickr_icon_td"><a href="http://www.flickr.com/groups/digital-designer/pool/"><img id="flickr_badge_icon" alt="elementos de alumnosartesvisuales" src="http://farm5.static.flickr.com/4148/buddyicons/1497188@N25.jpg?1287295769" align="left" width="48" height="48"></a></td>
	<td id="flickr_badge_source_txt">Más <a href="http://www.flickr.com/groups/digital-designer/pool/">en el mural de alumnosartesvisuales</a></td>
	</tr></table>
	</td>
	</tr>
	</table>
	</td></tr></table>
	<!-- End of Flickr Badge -->
	Powered by <a href="http://wordpress.org/" title="WordPress">WordPress</a>  diseñado por <a href="http://fbtemplate.wordpress.com/" title="Fred Example Web Design">fbtemplate</a>
	</p>
	<p><a href="feed:<?php bloginfo('rss2_url'); ?>"><img src="http://icons.iconarchive.com/icons/fasticon/web-2/16/Feed-icon.png" alt="RSS Feed Icon" />Posts RSS</a>
| <a href="feed:<?php bloginfo('comments_rss2_url'); ?>"><img src="http://icons.iconarchive.com/icons/fasticon/web-2/16/Feed-icon.png" alt="RSS Feed Icon" /> Comentarios RSS</a>
	</p>        
</div><!-- #site-info -->
```
￼
Bien podríamos seguir trabajando en el footer pero entiendo que es suficiente lo que hemos hecho hasta ahora.

En el área web encontrarás la versión más simple de footer.php pero tu puedes ajustarla según tus necesidades.