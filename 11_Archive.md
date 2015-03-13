## La página de archivo: archive.php ##

Una de las características de una web, especialmente de un blog, es que guarda información. Wordpress tiene una página especial para este fin denominada archive.php. Pero además esta página, al igual que anteriormente index.php, nos puede servir como template para otras páginas similares como attachment.php, author.php, category.php.

¿Que es lo que hace archive.php y por extensión el resto de las páginas que la utilizarán como plantilla?.

Pues muestra post de acuerdo a un criterio de selección, como un rango de fechas, los mensajes de un autor, una categoría o una etiqueta.

Vamos a recuperar la estructura que anteriormente creamos para **single.php.**

```
<?php get_header(); ?>
 
  <div id="twocols"> 
   <div id="maincol">
 
    <div id="post-<?php the_ID(); ?>" <?php post_class(); ?>>
    </div><!– #post-<?php the_ID(); ?> –>   
    
    <div id="nav-below" class="navigation">
    </div><!– #nav-below –>     
 
   </div><!– #maincol –> 
 
	<?php get_sidebar(); ?> 
  
	</div><!– #twocols –>
 
<?php get_footer(); ?>
```

**Esta es la secuencia de una plantilla de archivo.**
  * Se llama mediante the\_post()
  * Comprueba el tipo de plantilla de que se trata.
  * Produce una plantilla adecuada.
  * Recopila los post con rewind\_posts()
  * Se utiliza el loop de wordpress.
  * Este es el código que se encierra en el #content de archive.php. Empieza trabajando con las etiquetas condicionales para determinar el tipo de plantilla en la que estamos.

```
	<?php the_post(); ?>                    
 
	<?php if ( is_day() ) : ?>
        <h1 class="page-title"><?php printf( __( 'Archivo diario: <span>%s</span>', 'your-theme' ), get_the_time(get_option('date_format')) ) ?></h1>
<?php elseif ( is_month() ) : ?>
        <h1 class="page-title"><?php printf( __( 'Archivo mensual: <span>%s</span>', 'your-theme' ), get_the_time('F Y') ) ?></h1>
<?php elseif ( is_year() ) : ?>
        <h1 class="page-title"><?php printf( __( 'Archivo anual: <span>%s</span>', 'your-theme' ), get_the_time('Y') ) ?></h1>
<?php elseif ( isset($_GET['paged']) && !empty($_GET['paged']) ) : ?>
        <h1 class="page-title"><?php _e( 'Archivo del Blog', 'your-theme' ) ?></h1>
	<?php endif; ?>
 
	<?php rewind_posts(); ?>                    
 
	<?php while ( have_posts() ) : the_post(); ?>
 
        <div id="post-<?php the_ID(); ?>" <?php post_class(); ?>>
            <h2 class="entry-title"><a href="<?php the_permalink(); ?>" title="<?php printf( __('Permalink %s', 'your-theme'), the_title_attribute('echo=0') ); ?>" rel="bookmark"><?php the_title(); ?></a></h2>
 
            <div class="entry-meta">
                <span class="meta-prep meta-prep-author"><?php _e('Por ', 'your-theme'); ?></span>
                <span class="author vcard"><a class="url fn n" href="<?php echo get_author_link( false, $authordata->ID, $authordata->user_nicename ); ?>" title="<?php printf( __( 'Ver todos los posts de %s', 'your-theme' ), $authordata->display_name ); ?>"><?php the_author(); ?></a></span>
                <span class="meta-sep"> | </span>
                <span class="meta-prep meta-prep-entry-date"><?php _e('Publicado ', 'your-theme'); ?></span>
                <span class="entry-date"><abbr class="published" title="<?php the_time('Y-m-d\TH:i:sO') ?>"><?php the_time( get_option( 'date_format' ) ); ?></abbr></span>
                <?php edit_post_link( __( 'Edit', 'your-theme' ), "<span class=\"meta-sep\">|</span>\n\t\t\t\t\t\t<span class=\"edit-link\">", "</span>\n\t\t\t\t\t" ) ?>
            </div><!-- .entry-meta -->
 
            <div class="entry-summary">     
			<?php the_excerpt( __( 'Continue reading <span class="meta-nav">&raquo;</span>', 'your-theme' )  ); ?>
            </div><!-- .entry-summary -->
 
            <div class="entry-utility">
                <span class="cat-links"><span class="entry-utility-prep entry-utility-prep-cat-links"><?php _e( 'Posted in ', 'your-theme' ); ?></span><?php echo get_the_category_list(', '); ?></span>
                <span class="meta-sep"> | </span>
                <?php the_tags( '<span class="tag-links"><span class="entry-utility-prep entry-utility-prep-tag-links">' . __('Tagged ', 'your-theme' ) . '</span>', ", ", "</span>\n\t\t\t\t\t\t<span class=\"meta-sep\">|</span>\n" ) ?>
                <span class="comments-link"><?php comments_popup_link( __( 'Leave a comment', 'your-theme' ), __( '1 Comment', 'your-theme' ), __( '% Comments', 'your-theme' ) ) ?></span>
                <?php edit_post_link( __( 'Edit', 'your-theme' ), "<span class=\"meta-sep\">|</span>\n\t\t\t\t\t\t<span class=\"edit-link\">", "</span>\n\t\t\t\t\t\n" ) ?>
            </div><!-- #entry-utility -->   
        </div><!-- #post-<?php the_ID(); ?> -->
 
	<?php endwhile; ?>                      
 
	<?php global $wp_query; $total_pages = $wp_query->max_num_pages; if ( $total_pages > 1 ) { ?>
	        <div id="nav-below" class="navigation">
	                <div class="nav-previous"><?php next_posts_link(__( '<span class="meta-nav">&laquo;</span> Older posts', 'your-theme' )) ?></div>
	                <div class="nav-next"><?php previous_posts_link(__( 'Newer posts <span class="meta-nav">&raquo;</span>', 'your-theme' )) ?></div>
	        </div><!-- #nav-below -->
	<?php } ?>
```

### author.php ###

Muy parecida a la anterior lo que hace es localizar los post de un escritor determinado.
Para crearla duplica la anterior página y sustituye.

```
<?php if ( is_day() ) : ?>
        <h1 class="page-title"><?php printf( __( 'Archivo diario: <span>%s</span>', 'your-theme' ), get_the_time(get_option('date_format')) ) ?></h1>
	<?php elseif ( is_month() ) : ?>
	        <h1 class="page-title"><?php printf( __( 'Archivo mensual: <span>%s</span>', 'your-theme' ), get_the_time('F Y') ) ?></h1>
	<?php elseif ( is_year() ) : ?>
	        <h1 class="page-title"><?php printf( __( 'Archivo anual: <span>%s</span>', 'your-theme' ), get_the_time('Y') ) ?></h1>
	<?php elseif ( isset($_GET['paged']) && !empty($_GET['paged']) ) : ?>
	        <h1 class="page-title"><?php _e( 'Archivo del Blog', 'your-theme' ) ?></h1>
	<?php endif; ?>
por:
<h1 class="page-title author"><?php printf( __( 'Author Archives: <span class="vcard">%s</span>', 'your-theme' ), "<a class='url fn n' href='$authordata->user_url' title='$authordata->display_name' rel='me'>$authordata->display_name</a>" ) ?></h1>
	<?php $authordesc = $authordata->user_description; if ( !empty($authordesc) ) echo apply_filters( 'archive_meta', '<div class="archive-meta">' . $authordesc . '</div>' ); ?>
```

Listo.

### category.php ###

La plantilla de categoría es otra página fácil de hacer si partimos de una buena plantilla como archive.php. De modo que como ya hemos hecho en el caso anterior duplicamos archive.php y le cambiamos el nombre por category.php.

Ahora abrimos **functions.php.**

Vamos a colocar una función personalizada desde el tema Sandbox que va a hacer nuestra plantilla de categoría un poco más fiable.

```
// Para listar categorías en los archivos de categoría. Devuelve otras categorías salvo la actual para evitar redundancias.
function cats_meow($glue) {
        $current_cat = single_cat_title( '', false );
        $separator = "\n";
        $cats = explode( $separator, get_the_category_list($separator) );
        foreach ( $cats as $i => $str ) {
                if ( strstr( $str, ">$current_cat<" ) ) {
                        unset($cats[$i]);
                        break;
                }
        }
        if ( empty($cats) )
                return false;
 
        return trim(join( $glue, $cats ));
} // end cats_meow
```

La función personalizada cats\_meow() remueve la categoría actual de las páginas de categoría. En otras palabras se deshace de las categorías redundantes en la lista de categorías.

Ahora y de nuevo en **category.php** reemplazamos la sección de título de la página con el siguiente código:

```
<h1 class="page-title"><?php _e( 'Category Archives:', 'your-theme' ) ?> <span><?php single_cat_title() ?></span></span></h1>
    <?php $categorydesc = category_description(); if ( !empty($categorydesc) ) echo apply_filters( 'archive_meta', '<div class="archive-meta">' . $categorydesc . '</div>' ); ?>
Y en el div .entry-utility remplace 
    <span class="cat-links"><span class="entry-utility-prep entry-utility-prep-cat-links"><?php _e( 'Posted in ', 'your-theme' ); ?></span><?php echo get_the_category_list(', '); ?></span>
por:
<?php if ( $cats_meow = cats_meow(', ') ) : // Returns categories other than the one queried ?>
   <span class="cat-links"><?php printf( __( 'Also posted in %s', 'your-theme' ), $cats_meow ) ?></span>
   <span class="meta-sep"> | </span>
<?php endif ?>
```

### tag.php ###

Esta es la última de estas página especiales y está encargada de trabajar con las etiquetas.

Como en la página anterior vamos a crearla a partir de archive.php de modo que copie esta página y cambie su nombre por tag.php.

Vamos a utilizar de nuevo el tema Sandbox para utilizar una de las funciones definidas, abrimos por lo tanto **functions.php** y debajo de cats\_meow copiamos el código:

```
// Para listas de tag y archivos. Devuelve otras salvo la actual para evitar redundancias.
function tag_ur_it($glue) {
        $current_tag = single_tag_title( '', '',  false );
        $separator = "\n";
        $tags = explode( $separator, get_the_tag_list( "", "$separator", "" ) );
        foreach ( $tags as $i => $str ) {
                if ( strstr( $str, ">$current_tag<" ) ) {
                        unset($tags[$i]);
                        break;
                }
        }
        if ( empty($tags) )
                return false;
 
        return trim(join( $glue, $tags ));
} // end tag_ur_it
```

Salvamos y volvemos a **tag.php** y remplazamos el título de la página con:

```
<h1 class="page-title"><?php _e( 'Tag Archives:', 'your-theme' ) ?> <span><?php single_tag_title() ?></span></h1>
```

y en .entry-utility remplace:

```
<?php the_tags( '<span class="tag-links"><span class="entry-utility-prep entry-utility-prep-tag-links">' . __('Tagged ', 'your-theme' ) . '</span>', ", ", "</span>\n\t\t\t\t\t\t<span class=\"meta-sep\">|</span>\n" ) ?>
```

por el código modificado:

```
<?php if ( $tag_ur_it = tag_ur_it(', ') ) : // Returns tags other than the one queried ?>                                               
  <span class="tag-links"><?php printf( __( 'Also tagged %s', 'your-theme' ), $tag_ur_it ) ?></span>
<?php endif; ?>
```