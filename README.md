
<div align="center">
    <h1>Web Scraping: Extracción de Datos en la Web</h1>
    <img src="https://imgur.com/UbfjsMl.png" width="">
</div>

## Introducción al documento

El contenido de este documento son **3 proyectos prácticos** del [Curso de Web Scraping: Extracción de Datos en la Web](https://platzi.com/cursos/webscraping/) y busca ser una guía para futuros trabajos. El mismo está dictado por Martín Sokolowicz, Ingeniero electrónico y ayudante experto en [Digital House](https://www.digitalhouse.com/ar). El curso es de [Platzi](https://platzi.com).

Web Scraping es el proceso de adquisición previo al análisis de los datos. En el curso se conocerán y usarán herramientas como Scrapy y Selenium para hacer Web Scraping. Se automatizará el proceso utilizando técnicas para extraer contenido de sitios web. Estructuraremos el código HTML e identificaremos la información requerida para análisis usando BeautifulSoup.

## Objetivos del documento

- Comprender la importancia de la ética en las prácticas de Web Scraping
- Estructurar HTML con BeautifulSoup
- Extraer información de sitios web con técnicas de web scraping
- Hacer scraping de de sitios web dinámicos con Selenium
- Hacer Scraping usando APIs
- Usar Scrapy para extracción de datos a gran escala

## Tabla de contenido
- [Web Scraping: Extracción de Datos en la Web](#web-scraping-extracción-de-datos-en-la-web)
  - [Introducción, definiciones y ética](#introducción-definiciones-y-ética)
    - [Introducción y definiciones](#introducción-y-definiciones)
    - [Ética y Legalidad](#ética-y-legalidad)
      - [Robots.txt](#robotstxt)

# Web Scraping: Extracción de Datos en la Web

## Introducción, definiciones y ética

### Introducción y definiciones
- **Web Scraping**: Proceso de extracción de datos almacenados en la Web.
**Objetivo**: Recopilar información almacenada de un servidor web.
**Ejemplos**: Podemos scrapear los productos de una Eccomerce y sus reseñas, noticias de un pagina, tweets

- **Web Crawling**: Proceso de mapeo e indexación de páginas web para conocer su contenido.
**Objetivo**: Conocer la estructura de la Web.

Proyectos del curso
1. Obtener artículos publicados en la web del diario [Pagina 12](https://www.pagina12.com.ar/). Se utilizarán las siguientes bibliotecas:
   - Requests
   - Beautiful Soup
2. Scrapear la web [Latam Airlines](https://www.latam.com/es_es/). El objetivo será obtener información y precios de múltiples vuelos. Vamos a trabajar en este proyecto con:
   - Selenium
3. Como usar las APIs de [Spotify](https://www.spotify.com/es/) para obtener información sobre artistas, discos y canciones.

¿Hacer web scraping es legal? ¿Es hacer hacking? Eso lo vemos ahora...

### Ética y Legalidad

¿Es legal scrapear un sitio? Hay preguntas que hay que hacerce antes de hacer scraping y estas son:

- **¿Estoy violando alguna reglamentación local?**
  - Cada país y cada region tiene distinta reglamentación y leyes. Hay que estar al tanto si las estamos violando en el proyecto.
- **¿Estoy violando "Términos y condiciones" del sitio?**
- **¿Estoy accediendo a lugares no autorizados?**
- **¿Es legal el uso que le vamos a dar a los datos?**

Hay un archivo importante revisar antes de hacer scraping en alguna pagina y este es el robots.txt.

#### Robots.txt

Este archivo encontramos información sobre el sitio y nos muestra que sitio o rutas, el dueño de la página no quiere que acudamos.

Disallow: Rutas que no quieren que se le haga scraping o que sean indexadas.

Crawl-delay: 30: Demora en segundos entre cada solicitud del sitio. Para no sobrecargar este sitio.

**¿Como accedemos a el?** De la siguiente forma:
https://www.PAGINA_A_SCRAPEAR.com/robots.txt
