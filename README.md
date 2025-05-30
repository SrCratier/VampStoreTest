# CÓDIGO CREADO POR @SrCratier (Nvx) o simplemente Cratier. Este es un proyecto personal PROTEGIDO por derechos de autor.

1. Estructura del Documento (HTML - index.html)
El archivo index.html define la estructura fundamental de la página web y organiza el contenido visible.
<head>: Configuración y Metadatos
charset="UTF-8": Especifica la codificación de caracteres para asegurar la correcta visualización del texto.
viewport: Configura la ventana de visualización para asegurar la adaptabilidad del diseño en diferentes dispositivos (responsive design).
<title>: Establece el título de la página visible en la pestaña del navegador: "Vamp Store - Cuentas Premium".
<link rel="stylesheet" href="style.css">: Vincula el documento HTML con la hoja de estilos CSS para la presentación visual.
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">: Importa la biblioteca Font Awesome para la inclusión de iconos escalables.
<link href="https://fonts.googleapis.com/css2?family=MedievalSharp&family=Roboto:wght@400;500;600;700&display=swap" rel="stylesheet">: Carga fuentes personalizadas de Google Fonts (MedievalSharp para elementos distintivos como el logo y Roboto para el texto general).
<body>: Contenido Visible de la Página
Contiene todos los elementos que el usuario final visualiza e interactúa.
<header class="navbar">: Barra de Navegación Principal
Implementada con position: fixed para mantenerla visible en la parte superior de la ventana de visualización durante el desplazamiento.
Logo (.logo-link, .logo-container, .logo-v, .store-name): Representa la identidad visual de "Vamp Store" y funciona como enlace a la página principal.
Barra de Búsqueda (.search-container, #search-input): Un campo de entrada de texto (input type="text") con un icono de búsqueda (i.fas.fa-search). Permite a los usuarios buscar productos por palabras clave, con filtrado en tiempo real.
Selector de Moneda (.currency-selector-container, #currency-selector): Un elemento select que permite la selección de diferentes monedas. Los precios de los productos se actualizan dinámicamente según la moneda elegida.
<aside id="filter-sidebar" class="filter-sidebar">: Barra Lateral de Filtros
Implementada como una barra deslizable (position: fixed, transform: translateX) desde el lado izquierdo de la pantalla. Se abre automáticamente al cargar la página y se puede cerrar manualmente.
Su posición superior se alinea dinámicamente con la parte inferior del navbar para una integración visual fluida.
Encabezado (.filter-sidebar-header, <h2>): "Filtrar Servicios".
Controles de Filtrado por Categoría (.filter-nav, .filter-btn): Un conjunto de botones que permiten filtrar los productos por categorías de servicio (ej., Spotify, Disney+, HBO Max). El botón "Todos" desactiva los filtros de categoría individuales.
Sección de Filtros por Precio (.price-filter-section):
Título (.price-filter-heading): "FILTRAR POR PRECIO".
Rango de Precio Actual (.current-price-range): Muestra el rango de precios mínimo y máximo seleccionado en la moneda actual.
Sliders de Rango (#min-price-slider, #max-price-slider): Dos elementos input type="range" que permiten a los usuarios definir un rango de precios. Los valores seleccionados se muestran numéricamente junto a sus etiquetas.
Botón de Reset (#reset-price-filters): Restablece los sliders de precio a sus valores predeterminados.
Botón de Cierre (#sidebar-close-btn): Un botón integrado en la parte inferior de la sidebar para ocultarla.
<div class="page-content-wrapper" id="page-content-wrapper">: Contenedor de Contenido Principal
Este div abarca el product-grid y el footer. Se desplaza horizontalmente (margin-left) y ajusta su ancho (width) cuando la sidebar se abre o cierra, permitiendo que el product-grid se adapte y los productos se reorganicen sin quedar ocultos ni generar scroll horizontal no deseado.
Botón de Apertura de Sidebar (#sidebar-open-btn): Un botón flotante que aparece cuando la sidebar está cerrada, permitiendo al usuario volver a abrirla.
<main class="product-grid">: Cuadrícula de Productos
Implementa un diseño de cuadrícula flexible (display: grid; grid-template-columns: repeat(auto-fit, minmax(Xpx, 1fr))) que ajusta automáticamente el número de columnas de productos según el ancho disponible de la pantalla.
div class="product-card": Tarjetas de Producto
Cada tarjeta representa un producto individual con su imagen, título, duración, descripción inicial, precio (con data-price-usd para conversión) y lista de características.
data-category: Atributo crucial para el filtrado por servicio.
Acciones (.product-card-actions): Contiene enlaces/botones para añadir al carrito (con enlace a Discord) y realizar pagos vía PayPal.
<footer class="footer">: Pie de Página
Una sección en la parte inferior de la página con enlaces a plataformas de contacto (Discord para carrito y servidor).
2. Funcionalidad Interactiva (JavaScript - Integrado en index.html)
El código JavaScript, embebido al final del index.html, es responsable de la interactividad dinámica de la plataforma.
Gestión de Altura Dinámica del Navbar (updateNavbarHeightCssVariable):
Al cargar la página y al redimensionar la ventana, esta función calcula la altura real del navbar (offsetHeight).
Este valor se asigna a una variable CSS (--navbar-height) en el :root, lo que permite que la filter-sidebar, page-content-wrapper y sidebar-open-btn ajusten sus posiciones y tamaños relativos al navbar de manera precisa y adaptable.
Conversión de Moneda (updatePrices):
Obtiene la moneda seleccionada por el usuario y su tasa de cambio.
Itera sobre todos los precios de los productos (almacenados en USD en el atributo data-price-usd) y los convierte a la moneda seleccionada, actualizando la visualización del precio.
Actualización de Interfaz de Filtros de Precio (updatePriceFilterUI):
Sincroniza la visualización numérica de los valores mínimo y máximo seleccionados en los sliders de precio, mostrando la cantidad en la moneda actual.
Reinicio de Filtros de Precio (resetPriceFilters):
Restablece los sliders de precio a sus valores mínimos y máximos predeterminados y actualiza la interfaz.
Aplicación de Filtros Combinados (applyFilters):
Esta es la función central para el filtrado de productos. Se invoca ante cualquier cambio en los filtros de categoría, rangos de precio o la consulta de búsqueda.
Lógica de Filtrado: Evalúa cada tarjeta de producto basándose en tres criterios principales:
Categoría: Si la categoría del producto coincide con las categorías seleccionadas (o "todos").
Precio: Si el precio del producto en USD se encuentra dentro del rango definido por los sliders.
Búsqueda por Texto: Si el título del producto (insensible a mayúsculas/minúsculas) contiene la cadena de texto ingresada en la barra de búsqueda (filtrado en tiempo real a medida que se escribe).
Los productos que cumplen con todos los criterios se hacen visibles, y los que no, se ocultan.
Actualización de Interfaz de Botones de Categoría (updateFilterButtonsUI):
Asegura que el botón de categoría actualmente seleccionado (active) sea visualmente distinguible.
Control de la Barra Lateral (toggleSidebar):
Gestiona la apertura y el cierre de la filter-sidebar mediante la adición/eliminación de la clase open y el desplazamiento del page-content-wrapper con la clase shifted.
Persiste el estado de la sidebar (abierta/cerrada) en localStorage para recordar la preferencia del usuario entre sesiones.
Controla la visibilidad de los botones de abrir y cerrar la sidebar.
Manejo de Eventos (Event Listeners):
Se implementan escuchadores de eventos para detectar interacciones del usuario (cambios en el selector de moneda, clics en botones de filtro, entradas en la barra de búsqueda, movimientos de sliders, etc.) y desencadenar las funciones de actualización y filtrado correspondientes.
3. Estilos y Presentación (CSS - style.css)
El archivo style.css define la presentación visual de la plataforma, adhiriéndose a una estética oscura con acentos neón y asegurando un diseño responsivo.
Variables CSS (:root):
Define un conjunto de variables para colores (fondo principal, tarjetas, texto, acento, precio), tipos de fuente y duraciones de transición. Esto centraliza la personalización del tema visual. --navbar-height se inicializa con un valor por defecto, pero es controlado dinámicamente por JavaScript.
Estilos Base (body, *):
Establece la configuración de fuentes, colores de texto predeterminados y un fondo con gradientes radiales sutiles para la atmósfera visual.
navbar:
Estilizado con un fondo semi-transparente y backdrop-filter para un efecto de desenfoque. Utiliza flexbox para la alineación de sus elementos (logo, búsqueda, selector de moneda) y flex-wrap para su adaptabilidad en pantallas más pequeñas. position: fixed asegura su visibilidad constante.
search-container y search-input:
Diseño minimalista con bordes redondeados y un icono integrado, reflejando la estética neón.
currency-selector-container y currency-selector:
Similar al campo de búsqueda, con un icono de moneda y un select personalizado para la selección de divisas. Incluye un tooltip (::before) que aparece al pasar el cursor.
filter-sidebar:
Estilos para la barra lateral fija: fondo oscuro, borde derecho sutil, y una transición suave al deslizarse.
Ocultamiento de Scrollbar: Se implementan reglas CSS específicas (-ms-overflow-style: none; scrollbar-width: none; ::-webkit-scrollbar { display: none; }) para ocultar visualmente la barra de desplazamiento predeterminada del navegador, manteniendo la capacidad de desplazamiento vertical.
Filtros de Categoría (filter-nav, filter-btn):
Botones con bordes acentuados que cambian de color a un morado brillante cuando están active, proporcionando una retroalimentación visual clara. Los iconos se alinean con los botones.
Filtros de Precio (price-filter-section, slider-group, input[type="range"]):
Diseño integrado con el tema, incluyendo estilos personalizados para los sliders de rango que se ajustan al esquema de color neón.
sidebar-close-btn y sidebar-open-btn:
Botones de control para la sidebar, con el color de acento y transiciones de hover.
page-content-wrapper:
Esencial para el diseño responsivo con la sidebar. Su margin-top se ajusta a la altura dinámica del navbar. Su margin-left y width se adaptan cuando la sidebar se abre, forzando al product-grid a reorganizar sus columnas dentro del espacio disponible y previniendo el desbordamiento horizontal.
product-grid y product-card:
El product-grid utiliza CSS Grid para una distribución de productos fluida y responsiva.
Cada product-card tiene un fondo oscuro, bordes sutiles, sombras y efectos de hover y active que mejoran la interacción visual, con transiciones suaves.
Los iconos de "✦" en la lista de características son pseudo-elementos (::before) para mayor eficiencia.
product-card-actions:
Estilos para los botones de compra (add-to-cart-btn, paypal-btn), con sus respectivos colores y efectos de interacción.
footer:
Pie de página simple con enlaces a las redes sociales, con iconos grandes y efectos de hover para interactividad.
Media Queries (@media):
Definen estilos específicos para diferentes tamaños de pantalla (escritorio, tablet, móvil). Esto asegura que la página se adapte y optimice su diseño para una experiencia de usuario consistente, incluyendo la transición del navbar a un diseño apilado y la sidebar a un comportamiento de "overlay" en dispositivos móviles, donde no desplaza el contenido.

NOTA*
Estos solo son aspectos visuales para los usuarios, algunos de los mas importantes no fueron ni serán añadidos en actualizaciones.
Los aspectos técnicos como código, lógica y proceso no serán compartidos con el usuario.
Este código está disponible para la venta PRIVADA por único contacto en discord : srcratier (username).
