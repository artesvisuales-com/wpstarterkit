## El índex. ##

**Index.php****es la página más importante de un tema de wordpress, no solo porque la aplicación lo utilizará siempre que falte alguna de las páginas del tema como category.php o tag.php, sino porque el trabajo que desarrollemos en el index nos ayudará en el resto de las páginas a excepción de la de contenidos que tiene un tratamiento aparte.**

Empecemos a montar index.php haciendo la primera llamada para cargar la cabecera de la página.

`<?php get_header(); ?>`

### El loop ###

Es el proceso encargado de mostrar los post en pantalla, es una llamada recursiva que recorre el número de entradas de la base de datos y los muestra de acuerdo a unos criterios, “su funcionalidad es compleja pero su utilización es fácil de narices” como dice anieto2k.

```
<?php while ( have_posts() ) : the_post() ?>
<?php endwhile; ?>
```

Así de simple. Mientras tengamos mensajes en la base de datos se recorren, esperando hacer algo con cada uno de ellos, precisamente este “hacer algo” es la parte difícil del tema, pero incluso esto puede ser simple.

**Algunos previos.**

Para empezar vamos a probar esto colocando el siguiente código en en el `div #maincol` de index.php

```
<?php while ( have_posts() ) : the_post() ?>
<?php the_content(); ?>
<?php endwhile; ?>

// ¿Que obtenemos? Todo el contenido del mensaje. Podemos ordenarlo.

<ul>
<?php while ( have_posts() ) : the_post() ?>
<li>
    <?php the_excerpt(); ?>
</li>
<?php endwhile; ?>  
</ul>
```

Ahora tenemos una lista desordenada de estractos de entradas.

Básicamente hacemos un bucle que empieza con while y termina con endwhile.

Ok vamos a seguir trabajando con el bucle dando forma a index.php.

Bueno vamos a empezar a escribir el loop.

Como ves voy introduciendo comentarios dentro del código para que sea más fácil de entender que es lo que estamos haciendo.

```
<?php /* El Loop con comentarios! */ ?>
 
<?php while ( have_posts() ) : the_post() ?>
 
<?php /* Creamos un div con un único ID mediante the_ID() y clases semánticas con post_class() */ ?>
    <div id="post-<?php the_ID(); ?>" <?php post_class(); ?>>
```

Y ahora nos encargamos del título del post usando el código de la etiqueta de plantilla the\_title() para obtener el título de la entrada y vincularla al enlace permanente de la misma que definimos mediante the\_permalink() . También vamos a añadir un atributo de título y otro microformato (bookmark) que le dice a Google que este es el enlace permanente a una entrada del blog.

```
<?php /* Introducimos el Título en h2 */ ?>
     <h2 class="entry-title"><a href="<?php the_permalink(); ?>" title="<?php printf( __('Permalink to %s', 'your-theme'), the_title_attribute('echo=0') ); ?>" rel="bookmark"><?php the_title(); ?></a></h2>
```

Ahora nos toca incluir los aspectos adicionales del cualquier entrada de un blog, como quien lo escribió, cuando se publicó, categoría de la entrada, tag, link, comentarios, etc. Vamos a dividirlo en dos secciones, el autor y la fecha de publicación antes del contenido, y categorías, etiquetas, comentarios y enlaces después del mismo.

Vemos como queda el código:

```
<?php /* Microformatted, para los post meta */ ?>
    <div class="entry-meta">
            <span class="meta-prep meta-prep-author"><?php _e('Por ', 'your-theme'); ?></span>
            <span class="author vcard"><a class="url fn n" href="<?php echo get_author_link( false, $authordata->ID, $authordata->user_nicename ); ?>" title="<?php printf( __( 'Ver todos los post de %s', 'your-theme' ), $authordata->display_name ); ?>"><?php the_author(); ?></a></span>
            <span class="meta-sep"> | </span>
            <span class="meta-prep meta-prep-entry-date"><?php _e('Publicado ', 'your-theme'); ?></span>
            <span class="entry-date"><abbr class="published" title="<?php the_time('Y-m-d\TH:i:sO') ?>"><?php the_time( get_option( 'date_format' ) ); ?></abbr></span>
    </div><!-- .entry-meta -->
```

Bien ya tenemos los datos meta del post. Ahora colocamos el post propiamente dicho.
`<?php /* El contenido de la entrada*/ ?>`

```
<div class="entry-content">
	<?php the_content( __( 'Continue reading <span class="meta-nav">&raquo;</span>', 'your-theme' )  ); ?>
	<?php wp_link_pages('before=<div class="page-link">' . __( 'Pages:', 'your-theme' ) . '&after=</div>') ?>
</div><!-- .entry-content -->
```

Añadimos ahora la información de categoría, tag, y el link a los comentarios.

```
<?php /* Microformatted de categoría y tag, y el link a los comentarios */ ?>
    <div class="entry-utility">
            <span class="cat-links"><span class="entry-utility-prep entry-utility-prep-cat-links"><?php _e( 'Post en ', 'your-theme' ); ?></span><?php echo get_the_category_list(', '); ?></span>
            <span class="meta-sep"> | </span>
            <?php the_tags( '<span class="tag-links"><span class="entry-utility-prep entry-utility-prep-tag-links">' . __('Tag ', 'your-theme' ) . '</span>', ", ", "</span>\n\t\t\t\t\t\t<span class=\"meta-sep\">|</span>\n" ) ?>
            <span class="comments-link"><?php comments_popup_link( __( 'Leave a comment', 'your-theme' ), __( '1 Comment', 'your-theme' ), __( '% Comments', 'your-theme' ) ) ?></span>
            <?php edit_post_link( __( 'Edit', 'your-theme' ), "<span class=\"meta-sep\">|</span>\n\t\t\t\t\t\t<span class=\"edit-link\">", "</span>\n\t\t\t\t\t\n" ) ?>
    </div><!-- #entry-utility -->

//Cerramos las etiquetas y finalizamos el loop.
	</div><!-- #post-<?php the_ID(); ?> -->
 
<?php /* Cerramos post div */ ?>
 
<?php endwhile; ?>
```

### Navegación inferior. ###

Ahora necesitamos una manera de navegar a través del blog. La vamos a conseguir mediante dos etiquetas de wordpress: next\_posts\_link() y previous\_posts\_link(). Estas dos funciones hacen justo lo contrario que piensas que hacen :-)

- next\_posts\_link() crea un enlace a los post anteriores.
- previous\_posts\_link() crear un vínculo a los próximos post.

Podemos utilizarlas o no y podemos colocarlas en la parte superior de la página, en la inferior o en ambas. Yo voy a colocarlas en la parte inferior pero realmente es sólo para ver como funcionan. En mis trabajos con wordpress no suelo utilizarlas. Seguimos trabajando a renglón seguido dentro de content.

Contamos el número de página que tenemos y siempre que sea mayor que 1 damos salida a la navegación
Introducimos el sistema de navegación inferior:

```
<?php /* Realizamos un conteo de páginas*/ ?>
<?php global $wp_query; $total_pages = $wp_query->max_num_pages; if ( $total_pages > 1 ) { ?>	
<?php /* Hacemos la navegación inferior*/ ?>        
    <div id="nav-below" class="navigation">
            <div class="nav-previous"><?php next_posts_link(__( '<span class="meta-nav">&laquo;</span> Older posts', 'your-theme' )) ?></div>
            <div class="nav-next"><?php previous_posts_link(__( 'Newer posts <span class="meta-nav">&raquo;</span>', 'your-theme' )) ?></div>
    </div><!-- #nav-below -->
<?php } ?>	           
Cerramos los dos div content y container, llamando previamente a sidebar.php.
</div><!-- #maincol -->      
 
<?php get_sidebar(); ?> 
 
</div><!-- #twocols -->
```

Un último toque y hemos terminado index.php, vamos a cargar la barra lateral antes de get\_footer().

```
<?php get_footer(); ?>
```

Tienes el código completo en index.php.