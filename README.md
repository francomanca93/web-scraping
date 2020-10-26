
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
  - [Proyecto Scraper de Noticias. HTML: Requests y BeautifulSoup](#proyecto-scraper-de-noticias-html-requests-y-beautifulsoup)
    - [0. Prepraramos el entorno](#0-prepraramos-el-entorno)
    - [1. Descargando la página web](#1-descargando-la-página-web)
    - [2. Parseando HTML con BeautifulSoup](#2-parseando-html-con-beautifulsoup)
    - [3. Extrayendo información](#3-extrayendo-información)
    - [4. Manejo de errores](#4-manejo-de-errores)
    - [5. Descargando contenido](#5-descargando-contenido)

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

## Proyecto Scraper de Noticias. HTML: Requests y BeautifulSoup

En este módulo veremos cómo utilizar las bibliotecas `requests` y `bs4` para programar scrapers de sitios HTML. Nos propondremos armar un scraper de noticias del diario <a href='www.pagina12.com.ar'>Página 12</a>.

Supongamos que queremos leer el diario por internet. Lo primero que hacemos es abrir el navegador, escribir la URL del diario y apretar Enter para que aparezca la página del diario. Lo que ocurre en el momento en el que apretamos Enter es lo siguiente:
1. El navegador envía una solicitud a la URL pidiéndole información.
2. El servidor recibe la petición y procesa la respuesta.
3. El servidor envía la respuesta a la IP de la cual recibió la solicitud.
4. Nuestro navegador recibe la respuesta y la muestra **formateada** en pantalla.

Para hacer un scraper debemos hacer un programa que replique este flujo de forma automática y sistemática para luego extraer la información deseada de la respuesta. Utilizaremos `requests` para realizar peticiones y recibir las respuestas y `bs4` para *parsear* la respuesta y extraer la información.

Te dejo unos links que tal vez te sean de utilidad:
- [Códigos de status HTTP](https://developer.mozilla.org/es/docs/Web/HTTP/Status)
- [Documentación de requests](https://requests.kennethreitz.org/en/master/)
- [Documentación de bs4](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

### 0. Prepraramos el entorno

Para este caso particular al ser un proyecto personal no hay problemas con compartir la información y por ende utilizaré [google colab](https://colab.research.google.com/notebooks/welcome.ipynb?hl=es_US) para que el trabajo sea mas rápido, pero los pasos para configurar el entorno de trabajo de un proyecto profesional en Linux o Mac, es el siguiente:

1. Crear una carpeta con el nombre del proyecto: `mkdir webscraping_noticias`
2. Ingresar carpeta del proyecto y crear un entorno virtual: `python3 -m venv nombre_entorno`
3. Activar el entorno virtual: `source nombre_entorno/bin/activate`
4. Instalar jupyter notebook (no hace falta instalar toda la suite Anaconda) : `python3 pip install jupyter`
5. Instalar requests: `pip install requests`
6. Instalar Beautiful Soup: `pip install beautifulsoup4`
7. Verificar que todo se instalo utilizando el comando `pip freeze`

### 1. Descargando la página web

Importamos el módulo requests y trabajamos con él. 

- `p12 = requests.get(url)`: realiza la solicitud.
- `p12.status_code`: muestra el código de status HTTP de la respuesta.
- `print(p12.text)`: muestra el HTML de la página sin formatear.
- `p12.content`: muestra el contenido de la respuesta, puede ser bytes, imágenes, audio.
- `p12.headers`: muestra el encabezado de la respuesta.
- `p12.request.headers`: muestra el encabezado de la solicitud. El contenido de esta request avisa al servidor que se está utilizando requests en python y que no es un navegador convencional. Puede ser modificado.
- `p12.request.url`: muestra la url a la que se le hizo la solicitud.

### 2. Parseando HTML con BeautifulSoup

Lo que hacemos ahora es importar BeautifulSoup: `from bs4 import BeautifulSoup`

Con el atributo `html.parser` separamos el texto largo en pedazos mas pequeños y mas fácil de identificar

```py
s = BeautifulSoup(p12.text, 'html.parser')

# Imprimimos html estructurado
print (s.prettify())

#extraemos la clase
s.find('ul', attrs={'class':'main-sections'})

#especificamos todos los li
s.find('ul', attrs={'class':'main-sections'}).find_all('li')

#extraemos la etiqueta a
s.find('ul', 'main-sections').find_all('a')
```

### 3. Extrayendo información

En esta sección se crean 3 funciones para poder extraer información de Pagina12. Las funciones son las siguientes:

```py
def get_section_links(url):
  ''' Funcion para traer los links de las secciones'''
  p12 = requests.get(url) # Hacemos un requests a la url que ingresamos
  links_secciones = [] # Lista de links a secciones
  # Intentamos y si hay un error lo atrapamos
  try:
    if p12.status_code == 200:
      s = BeautifulSoup(p12.text, 'html.parser') # Objeto soup
      secciones = s.find('ul', attrs={'class':'main-sections'}).find_all('li') # Buscamos las secciones
      links_secciones = [seccion.a.get('href') for seccion in secciones] # Extraemos los links
  except Exception as e: # Capturamos error
    print('Error')
    print(e)

  return links_secciones
```

Extraidos los links de cada sección, elegimos cual queremos scrapear:

```py
def get_section_soup(link_section):
  ''' Obtengo una seccion deseada pasandole el link a la sección'''
  section = requests.get(link_section)
  try: 
    if section.status_code == 200:
      soup_section = BeautifulSoup(section.text, 'lxml')
  except Exception as e:
    print('Ocurrio un error')
    print(e)
    print('\n')
  
  return soup_section
```

Scrapeada la sección que deseamos, obtenemos los links de las noticias de la sección parseando el objeto soup:

```py
def get_links_for_section(soup):
  ''' Busca en un objeto soup los links de los articulos'''
  try:
    news = soup.find_all('div', attrs = {'class':'article-item__content'})
    links_news = [new.a.get('href') for new in news]
  except Exception as e:
    print('Error')
    print(e)

  return links_news
```

Para finalizar llamamos todas las funciones en orden para extraer lo que deseamos:

```py
def main():
  ''' Funcion principal que junta a todas las funciones anteriores'''
  links_secciones = []
  links_scrapeados = []

  print('Extrayendo links de la seccion que queremos')
  url = 'https://www.pagina12.com.ar'
  links_secciones = get_section_links(url)

  print('Selecciona el link a scrapear')
  for i, link in enumerate(links_secciones):
    print(f'Opcion {i}: {link}')
  
  user = int(input('Opcion: ')) # Entrada de usuario

  try:
      section_text = get_section_soup(links_secciones[user]) # Obtenemos texto
  except IndexError:
      print('Invalid Option')

  links_scrapeados = get_links_for_section(section_text) # Scraper de links

  for link in links_scrapeados:
    print(f'Link: {link}')

if __name__ == '__main__':
  main()
```

### 4. Manejo de errores

Cuando ocurre algún error en el código, Python detiene la ejecución y nos devuelve una **excepción**, que no es más que una señal que ha occurrido un funcionamiento no esperado o error en el programa, indicándonos aproximadamente qué fue lo que ocurrió.

Para hacer esto podemos usar la sentencia `try-except`, que nos permite **probar (Try)** una sentencia y **capturar un eventual error** y hacer algo al respecto **(except)** en lugar de detener el programa directamente.

```py
try:
  codigo...
except Exception as e:
  print('Error')
  print(e)
```

Excelente link para aprender como tratar errores con mas detalles: [Tratamiento de errores. Sentencia try-except](http://research.iac.es/sieinvens/python-course/source/errores_depuracion.html).

### 5. Descargando contenido

En esta sección se desarrollo una función que recibe la url de la nota y devuelve un diccionario con el scrapper, listo para ser guardado en una base de datos.

Se utilizará la siguiente imagen para saber que datos extraer del periodico.

![diario](https://imgur.com/eoj37pn.png)

Para extraer información se utiliza el inspector de elementos del navegador que se esté utilizando. Con F12 abrimos las herramientas de desarrollador y en él utilizamos el inspector de elementos.

```py
def extract_data(url_nota):
  ''' Función que recibe la url de la nota de devuelve un diccionario con el scrapper'''
  
  dict_info_scraper = {}
  
  try:
    nota = requests.get(url_nota)
    if nota.status_code == 200:
      s_nota = BeautifulSoup(nota.text, 'lxml')

      # Extraer el titulo
      titulo = s_nota.find('h1', attrs = {'class': 'article-title'})
      dict_info_scraper['Titulo'] = titulo.text
      # Extraer autor
      autor = s_nota.find('div', attrs={'class':'article-author'})
      dict_info_scraper['Autor'] = autor.text
      # Extraer fecha del titulo
      fecha = s_nota.find('span', attrs = {'pubdate': 'pubdate'}).get('datetime')
      dict_info_scraper['Fecha'] = fecha
      # Extraer el volanta
      volanta = s_nota.find('h2', attrs = {'class': 'article-prefix'})
      dict_info_scraper['Volanta'] = volanta.text
      # Extraer copete
      try:
        copete = s_nota.find('div', attrs = {'class': 'article-summary'})
        dict_info_scraper['Copete'] = copete.text
      except:
        print(None)
        print('\n')
      # Extraer epigrafe
      epigrafe = s_nota.find('span', attrs = {'class': 'article-main-media-text-image'})
      dict_info_scraper['Epigrafe'] = epigrafe.text
      # Extraer cuerpo
      cuerpo = s_nota.find('div', attrs = {'class': 'article-body diario'}).find_all('p')
      articulo_texto = []
      for parrafo in cuerpo:
        articulo_texto.append(parrafo.text)
      dict_info_scraper['Cuerpo'] = articulo_texto

  except Exception as e:
    print('Error')
    print(e)
    print('\n')
  
  return dict_info_scraper # Dictionary
```
