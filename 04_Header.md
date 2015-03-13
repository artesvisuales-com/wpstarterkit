## Header.php ##

Comenzamos con la creación de la página de cabecera. Vamos a colocar un doctype que le diga al navegador como interpretar el código html que está viendo.

Vamos a utilizar XHTML Transitional Doctype, hay otras opciones pero es el más adecuado para un tema de wordpress.

Abre header.php y copia el siguiente código.

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

Vamos a añadir algunos atributos de apertura html, de modo que coloque la etiqueta `<html>` con la siguiente línea:

```
<html xmlns="http://www.w3.org/1999/xhtml" <?php language_attributes(); ?>
```

Una vez hechas las presentaciones vamos a entrar en la sección `<head>` del tema. Esta sección contiene meta información de la página web, como el título del documento, enlaces a las hojas de estilo o los feed RSS.

En primer lugar vamos a abrir el archivo **functions.php**, y a añadirle una función que nos será útil cuando creemos el título del documento.

Abrimos functions.php y comenzamos el código con <?php. Déjamos un par de líneas libres para ir ordenando el código y escribimos las siguientes dos funciones de php:

```
<?php
 
// Prepara el tema para su traducción
// Traducción con el fichero que se encuentra en /languages/ directory
load_theme_textdomain( 'your-theme', TEMPLATEPATH . '/languages' );
 
$locale = get_locale();
$locale_file = TEMPLATEPATH . "/languages/$locale.php";
if ( is_readable($locale_file) )
        require_once($locale_file);
 
// Obtener el número de página
function get_page_number() {
    if (get_query_var('paged')) {
        print ' | ' . __( 'Page ' , 'your-theme') . get_query_var('paged');
    }
} // end get_page_number
?>
```

La primera función prepara a nuestro tema para ser traducido y que los archivos de la traducción se encuentran en nuestra carpeta de tema en una carpeta llamada languages.

La siguiente función get\_page\_number() como puedes ver se articula mediante un condicional if para ver si estamos en una página de paginado. Si es así esta función se imprimirá un separador de barras y el número de página actual.

Además si eres nuevo en php quédate con un detalle más. Cualquier cosa después de la doble barra // es usado como un comentario y por lo tanto obviado.

Volvemos a la sección `<head>` de **header.php**. Complete head con el siguiente código:

```
<head profile="http://gmpg.org/xfn/11">
    <title><?php
        if ( is_single() ) { single_post_title(); }      
        elseif ( is_home() || is_front_page() ) { bloginfo('name'); print ' | '; bloginfo('description'); get_page_number(); }
        elseif ( is_page() ) { single_post_title(''); }
        elseif ( is_search() ) { bloginfo('name'); print ' | Search results for ' . wp_specialchars($s); get_page_number(); }
        elseif ( is_404() ) { bloginfo('name'); print ' | Not Found'; }
        else { bloginfo('name'); wp_title('|'); get_page_number(); }
    ?></title>
 
 <meta http-equiv="content-type" content="<?php bloginfo('html_type'); ?>; charset=<?php bloginfo('charset'); ?>" />
 
 <link rel="stylesheet" type="text/css" href="<?php bloginfo('stylesheet_url'); ?>" />
 
 <?php if ( is_singular() ) wp_enqueue_script( 'comment-reply' ); ?>
 
 <?php wp_head(); ?>
```

Veamos lo que estamos haciendo.

-Para comenzar el título lo definimos mediante una serie de condicionales  if y elseif que dependiendo del contenido, single, home, page, etc, mostrará un título u otro.

-Después introducimos alguna información meta y el vínculo al estilo css.

- Ahora incluimos también un script para utilizar los comentarios y enlaces a los feed rss y pingbacks.

```
<link rel="alternate" type="application/rss+xml" href="<?php bloginfo('rss2_url'); ?>" title="<?php printf( __( '%s latest posts', 'your-theme' ), wp_specialchars( get_bloginfo('name'), 1 ) ); ?>" />
 <link rel="alternate" type="application/rss+xml" href="<?php bloginfo('comments_rss2_url') ?>" title="<?php printf( __( '%s latest comments', 'your-theme' ), wp_specialchars( get_bloginfo('name'), 1 ) ); ?>" />
 <link rel="pingback" href="<?php bloginfo('pingback_url'); ?>" />
```

- Añadimos el código de google analytics justo antes del cierre de `</head>` para poder obtener estadísticas de tráfico de nuestro sitio.

```
<script type="text/javascript">
 
  var _gaq = _gaq || [];
  _gaq.push(['_setAccount', 'UA-11642988-1']);
  _gaq.push(['_trackPageview']);
 
  (function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
  })();
 
</script>
```

Un par de aclaraciones. **El código UA-11642988-1 es ficticio**. Existen plugin que nos permiten introducir el código de analytics sin necesidad de editar el pie de la página, pero personalmente prefiero introducirlo directamente en vez de cargar un plugin más al sistema.

Después cerramos head.

`</head>`

Abrimos el body y empezamos a trabajar con el contenido del documento mediante la sección de header.

```
<body>
 
<div id="pagewidth" class="hfeed">
La sección del header

<div id="header">
	<div id="branding">
		<div id="blog-title"><span><a href="<?php bloginfo( 'url' ) ?>/" title="<?php bloginfo( 'name' ) ?>" rel="home"><?php bloginfo( 'name' ) ?></a></span></div>
		<?php if ( is_home() || is_front_page() ) { ?>
		    <h1 id="blog-description"><?php bloginfo( 'description' ) ?></h1>
		<?php } else { ?>
		    <div id="blog-description"><?php bloginfo( 'description' ) ?></div>
		<?php } ?>
	</div><!– #branding –>
```

Dependerá de criterios seleccionar la información pero en este caso nos parece relevante mostrar el nombre del blog y la descripción dentro del id=” branding”. Utilizamos una etiqueta llamada bloginfo() mediante la que obtenemos la dirección del blog, su nombre y descripción.

Como ves y esto es importante vamos utilizando la estructura html creada previamente y en ella vamos incluyendo llamadas, mediante condicionales if, a etiquetas php de wordpress que se encargarán de mostrar la información precisa.

De modo que completemos el header.

Añadimos un método para que los visitantes puedan ir directamente al contenido saltándose el menú mediante skip to content, esto es más que nada para que veas como se puede implementar y su utilización depende de si lo consideras útil o no, y por último mostramos el menú de la página mediante una etiqueta con un solo argumento.

```
<div id="access">
            <div class="skip-link"><a href="#content" title="<?php _e( 'Skip to content', 'your-theme' ) ?>"><?php _e( 'Skip to content', 'your-theme' ) ?></a></div>
            <?php wp_page_menu( 'sort_column=menu_order' ); ?>                      
    </div><!-- #access -->
 
  </div><!– #header –>
 
  <div id="wrapper" class="clearfix">
```

Una vez hecho header.php, estamos en condiciones de afrontar la segunda página que utilizaremos en el montaje de todas las demás: footer.php.