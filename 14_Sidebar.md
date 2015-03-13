## sidebar.php ##

Es una de las páginas fundamentales de wodpress.

Para empezar vamos a personalizar las funciones de la barra lateral.

Vamos a crear un sidebar con dos áreas para los widget y otras dos para los menús de la última versión de
wordpress. De esta forma podemos volver a utilizar este código para temas con dos o tres columnas. De
todos modos creo que vamos sobrados y es posible que no utilicemos todos los recursos en todo caso de lo
que se trata es de aprender a hacerlo.

**functions.php**

Abrimos la página functions.php en la que vamos a registrar las áreas de widget con el siguiente código:

```
// Declara la zona de sidebar widget 
        if (function_exists('register_sidebar')) {
                register_sidebar(array(
                        'name' => 'Sidebar Widgets I',
                        'id'   => 'sidebar-widgets',
                        'before_widget' => '<div id="%1$s" class="widget %2$s">',
                        'after_widget'  => '</div>',
                        'before_title'  => '<h2>',
                        'after_title'   => '</h2>'
                ));
        }
          if (function_exists('register_sidebar')) {
                register_sidebar(array(
                        'name' => 'Sidebar Widgets II',
                        'before_widget' => '<div id="%1$s" class="widget %2$s">',
                        'after_widget'  => '</div>',
                        'before_title'  => '<h2>',
                        'after_title'   => '</h2>'
                ));
        }
```

En todo caso ahora al acceder a la administración de los Widgets veremos las dos zonas creadas. Ahora tenemos dos areas widget: Sidebar Widgets I y Sidebar Widgets II. Si por ejemplo arrastramos el
Archivos a Sidebar Widgets I veremos como se mostrará en nuestra página sidebar.

![http://stream.artesvisuales.com/images/wp_sidebar_widgets.jpg](http://stream.artesvisuales.com/images/wp_sidebar_widgets.jpg)

Ahora vamos a registrar los menús mediante un array que nos permitirá tener dos menús llamados
respectivamente Top Navigation Menu y Cat Navigation Menu.

```
//Registro de los menús
        if (function_exists('register_nav_menus')) {
                register_nav_menus(
                        array(
                                'main_nav' => 'Top Navigation Menu',
                                'cat_nav' => 'Cat Navigation Menu',
                        )
                );
        } 
```

Bien tenemos registrados tanto los widgets como los 2 menús, ahora depende de nosotros utilizarlo o no
pero en todo caso los tenemos a nuestra disposición.

Vamos a **sidebar.php.**

Es la última página que nos falta por crear. Se mostrará a la izquierda o derecha del sitio, dependiendo del
css, y en ella cargamos información adicional al contenido. Por ejemplo podemos integrar nuestras redes
sociales como facebook o twitter mediante widgets, cargar un rss, mostrar el menú, categorías, link, etc... A
nuestro gusto.

Empecemos con su código.

Lo primero que hacemos es cargar la búsqueda:

```
<?php get_search_form(); ?>
```

En este caso vamos a optar por la página de búsqueda con el motor de wordpress, pero de igual modo podemos cargar el sistema de búsqueda personalizada de google.

Seguimos cargando el menú:

```
<nav>
<?php wp_nav_menu(array('menú' => 'Categorias')); ?>
</nav>
```

Y a posteriori lo configuramos en wordpress. Para ello vamos a Apariencia > Menús, creamos el menú Categorias que se corresponde con el código de sidebar.php

![http://stream.artesvisuales.com/images/wp_sidebar_menus_I.jpg](http://stream.artesvisuales.com/images/wp_sidebar_menus_I.jpg)

Seleccionamos las categorías que queremos mostrar y las añadimos al menú.

![http://stream.artesvisuales.com/images/wp_sidebar_menus_II.jpg](http://stream.artesvisuales.com/images/wp_sidebar_menus_II.jpg)

Por último guardamos el menú y sus cambios de modo que se vería así:

![http://stream.artesvisuales.com/images/wp_sidebar_menus_III.jpg](http://stream.artesvisuales.com/images/wp_sidebar_menus_III.jpg)

Ahora al previsualizar la página veríamos como son estas categorías las que se muestran en el sidebar.

### Cargar un rss externo: ###

A mi esto me gusta controlarlo manualmente mediante código, de modo que el código es el siguiente:

```
<div class="widget-rss"> <!-- Comienzo del RSS--> 

    <h4>FAQ</h4>
    
    <?php if (function_exists('fetch_feed')) { ?>
            
            <?php include_once(ABSPATH . WPINC . '/feed.php'); 
            
                  $feed = fetch_feed('feed://wordpress.org/news/feed/');
            
                      $limit = $feed->get_item_quantity(3);
                    
                      $items = $feed->get_items(0, $limit);
                    
                    if (!$items) {
                            
                            echo "problem";
                            
                    } else {
                            
                            // Mostramos las entradas del RSS
                            
                            foreach ($items as $item) { ?>
                                    
                                    <div class="sidebar-post">
                                            <p class="date"><?php echo $item->get_date('F j, Y'); ?></p>
                                            <h5><a href="<?php echo $item->get_permalink(); ?>"><?php echo $item->get_title(); ?></a></h5>
                                            <p><?php echo $item->get_content(); ?></p>
                                    </div>
                            
                    <?php } 
                    
                } ?>

    <?php } ?>

</div> <!-- Fin del RSS--> 
```

Debemos fijarnos como:

  * Mediante $feed = fetch\_feed('feed://www.formspring.me/profile/artesvisuales.rss'); cargamos la fuente
rss que vamos a leer.
  * Con $limit = $feed->get\_item\_quantity(5); seleccionamos el número de entradas que mostramos.
  * Por ultimo configuramos el estilo de las entradas mostradas.

Y para finalizar la página vamos a los widget. Por último cerramos el div.

```
     <div class="widget">  <!-- widget--> 
       <?php if (function_exists('dynamic_sidebar') && dynamic_sidebar('Sidebar Widgets')) : else : ?>

       <!-- Contenido que se muestra si no hay contenido en el widget I-->
                
       <?php endif; ?>    
       <!-- Fin widget--> 
         
       <!-- Segundo widget-->       
       <?php if ( !function_exists('dynamic_sidebar') || !dynamic_sidebar("Sidebar Widgets II") ) : else: ?>                 
       <?php endif; ?> 
      <!-- Fin segundo widget-->

</div><!– #rightcol –> 
```

Bien tenemos la página lista ahora mediante wordpress vamos a cargar contenido en los widgets.

Me voy al área de administración de widgets, arrastro el recuadro de texto a Sidebar Widgests I y dentro del
mismo coloco el código de inserción de una página de facebook, como puedes ver en la imagen siguiente.

![http://stream.artesvisuales.com/images/wp_sidebar_widgets_I.jpg](http://stream.artesvisuales.com/images/wp_sidebar_widgets_I.jpg)

Ahora en el sidebar se muestra el contenido de nuestra página en facebook.

![http://stream.artesvisuales.com/images/wp_sidebar_widgets_II.jpg](http://stream.artesvisuales.com/images/wp_sidebar_widgets_II.jpg)

Repito el proceso con twitter pero ahora colocando el código en Sidebar Widgets II.

```
<script src="http://widgets.twimg.com/j/2/widget.js"></script>
<script>
new TWTR.Widget({
version: 2,
type: 'profile',
rpp: 5,
interval: 6000,
width: 250,
height: 300,
theme: {
shell: {
background: '#f7f7f7',
color: '#949294'
},
tweets: {
background: '#fcfcfc',
color: '#706970',
links: '#fa0808'
}
},
features: {
scrollbar: false,
loop: false,
live: false,
hashtags: true,
timestamp: true,
avatars: false,
behavior: 'all'
}
}).render().setUser('usuario_twitter').start();
</script>
```

El template está terminado, solo nos queda darle una estructura básica mediante css.