<h1>Instalación y Configuración de Streamlit con UV en un Contenedor Docker</h1>

<h2>Descripción</h2>
<p>
Esta práctica consiste en la instalación y configuración de una aplicación web desarrollada con Streamlit
dentro de un entorno Linux basado en Ubuntu ejecutado en un contenedor Docker. Durante el desarrollo de la actividad
se realizaron tareas de actualización del sistema, instalación de dependencias necesarias para Python,
instalación del gestor de paquetes UV, clonación de un repositorio de ejemplo desde GitHub y ejecución
de una aplicación Streamlit.
</p>

<p>
El objetivo principal fue comprender el proceso completo de preparación de un entorno de desarrollo para
aplicaciones Python, así como la ejecución de una aplicación web interactiva mediante Streamlit dentro
de un contenedor.
</p>

<hr>

<h2>Entorno de Trabajo</h2>
<p>El entorno utilizado para esta práctica fue el siguiente:</p>

<ul>
<li>Docker Desktop</li>
<li>Contenedor basado en Ubuntu</li>
<li>Python 3</li>
<li>Streamlit</li>
<li>UV (gestor rápido de paquetes y entornos virtuales)</li>
<li>Git para clonación de repositorios</li>
<li>Puerto utilizado para la aplicación: 8501</li>
</ul>

<hr>

<h2>Procedimiento Realizado</h2>

<h3>1. Actualización del sistema</h3>
<p>Se ejecutaron los siguientes comandos para actualizar el sistema:</p>

<ul>
<li>apt update</li>
<li>apt upgrade -y</li>
</ul>

<p>
El comando <code>apt update</code> permite actualizar la lista de paquetes disponibles
en los repositorios configurados del sistema operativo Ubuntu. Esto asegura que el sistema
tenga información actualizada sobre las versiones de software disponibles.
</p>

<p>
El comando <code>apt upgrade -y</code> actualiza los paquetes instalados en el sistema
a sus versiones más recientes. La opción <code>-y</code> permite aceptar automáticamente
las confirmaciones necesarias durante el proceso de actualización.
</p>

<p>
Como resultado de esta operación, el sistema actualizó varios paquetes importantes,
incluyendo librerías y herramientas del sistema.
</p>

<hr>

<h3>2. Instalación de herramientas y dependencias</h3>
<p>
Una vez actualizado el sistema, se procedió a instalar las herramientas necesarias
para ejecutar aplicaciones de Python y trabajar con repositorios de código.
</p>

<p>El comando utilizado fue:</p>

<p>
<code>
apt install -y git curl python3 python3-venv python3-pip
</code>
</p>

<p>
Este comando instala múltiples herramientas esenciales para el desarrollo.
Git permite gestionar versiones de código y clonar repositorios desde GitHub.
Curl se utiliza para descargar archivos desde internet. Python3 es el intérprete
principal para ejecutar programas en Python. Python3-venv permite crear entornos
virtuales aislados y python3-pip es el gestor de paquetes para instalar librerías
de Python.
</p>

<p>
Después de la instalación se verificó la versión de Python instalada utilizando
el siguiente comando:
</p>

<p><code>python3 --version</code></p>

<p>
El resultado mostró que la versión instalada fue Python 3.13.3.
</p>

<hr>

<h3>3. Instalación del gestor de paquetes UV</h3>
<p>
Posteriormente se instaló UV, una herramienta moderna diseñada para gestionar
dependencias de Python y crear entornos virtuales de manera más rápida que
las herramientas tradicionales como pip y venv.
</p>

<p>El comando utilizado fue:</p>

<p>
<code>
curl -Ls https://astral.sh/uv/install.sh | sh
</code>
</p>

<p>
Este comando descarga el script de instalación desde el sitio oficial de UV
y lo ejecuta automáticamente en el sistema. La herramienta se instaló en el
directorio <code>/root/.local/bin</code>.
</p>

<p>
Después de la instalación fue necesario recargar la configuración de la terminal
para que el sistema reconociera la nueva herramienta.
</p>

<p><code>source $HOME/.bashrc</code></p>

<p>
Finalmente se verificó que UV estuviera correctamente instalado utilizando:
</p>

<p><code>uv --version</code></p>

<p>
El resultado indicó que la versión instalada fue UV 0.10.9.
</p>

<hr>

<h3>4. Clonación del proyecto de Streamlit</h3>
<p>
Una vez preparado el entorno de desarrollo, se procedió a descargar un proyecto
de demostración de Streamlit desde GitHub.
</p>

<p>El comando utilizado fue:</p>

<p>
<code>
git clone https://github.com/streamlit/demo-seattle-weather.git
</code>
</p>

<p>
Este comando creó una copia local del repositorio dentro del contenedor,
generando una carpeta llamada <strong>demo-seattle-weather</strong>
que contiene todos los archivos del proyecto.
</p>

<p>
Posteriormente se ingresó al directorio del proyecto utilizando:
</p>

<p><code>cd demo-seattle-weather</code></p>

<hr>

<h3>5. Creación del entorno virtual con UV</h3>
<p>
Para aislar las dependencias del proyecto se creó un entorno virtual
utilizando la herramienta UV.
</p>

<p>El comando utilizado fue:</p>

<p><code>uv venv</code></p>

<p>
Este comando generó un entorno virtual dentro de la carpeta
<code>.venv</code> del proyecto.
</p>

<p>
Posteriormente se activó el entorno virtual utilizando el comando:
</p>

<p><code>source .venv/bin/activate</code></p>

<p>
Cuando el entorno virtual se activa, la terminal muestra el nombre
del proyecto al inicio del prompt, lo que indica que todas las
dependencias que se instalen estarán aisladas dentro de este entorno.
</p>

<p>
Después se ejecutó el siguiente comando para instalar automáticamente
las dependencias del proyecto:
</p>

<p><code>uv sync</code></p>

<p>
Este comando analizó los archivos de configuración del proyecto y
descargó todas las librerías necesarias, incluyendo Streamlit,
pandas, numpy y otras dependencias utilizadas por la aplicación.
</p>

<hr>

<h3>6. Ejecución de la aplicación Streamlit</h3>
<p>
Finalmente se ejecutó la aplicación web utilizando el siguiente comando:
</p>

<p>
<code>
streamlit run streamlit_app.py --server.address 0.0.0.0 --server.port 8501
</code>
</p>

<p>
El comando <code>streamlit run</code> inicia el servidor de Streamlit
y ejecuta la aplicación definida en el archivo <strong>streamlit_app.py</strong>.
La opción <code>server.address 0.0.0.0</code> permite que el servidor
escuche en todas las interfaces de red del contenedor, lo cual es
necesario para acceder a la aplicación desde fuera del contenedor.
</p>

<p>
La opción <code>server.port 8501</code> define el puerto donde se ejecutará
la aplicación.
</p>

<p>
Una vez iniciado el servidor, la aplicación puede accederse mediante
la siguiente dirección:
</p>

<p><strong>http://localhost:8501</strong></p>

<hr>

<h2>Problema detectado</h2>
<p>
Durante la ejecución de la aplicación se identificó un problema
relacionado con el mapeo de puertos del contenedor Docker.
El contenedor fue creado a partir de la imagen <strong>ubuntu/nginx</strong>,
la cual está diseñada principalmente para ejecutar el servidor web Nginx.
</p>

<p>
El problema ocurrió debido a una configuración incorrecta del mapeo
de puertos utilizando la sintaxis <strong>8501:80</strong>.
Esta configuración genera un conflicto porque la aplicación Streamlit
se ejecuta en el puerto 8501 dentro del contenedor.
</p>

<hr>

<h2>Solución aplicada</h2>
<p>
Para solucionar el problema fue necesario eliminar el contenedor
actual y crear uno nuevo con el mapeo de puertos correcto.
</p>

<p>
El formato correcto para el mapeo de puertos en Docker es:
</p>

<p><code>puerto_host:puerto_contenedor</code></p>

<p>
En este caso la configuración correcta es:
</p>

<p><code>-p 8501:8501</code></p>

<p>
Esta configuración permite enlazar el puerto 8501 del contenedor,
donde se ejecuta Streamlit, con el puerto 8501 de la máquina host.
De esta manera la aplicación puede accederse correctamente desde
el navegador utilizando la dirección <strong>http://localhost:8501</strong>.
</p>

<hr>

<h2>Aprendizajes obtenidos</h2>

<ul>
<li>Administración básica de paquetes en Linux</li>
<li>Instalación de herramientas de desarrollo en Python</li>
<li>Uso del gestor de dependencias UV</li>
<li>Creación de entornos virtuales</li>
<li>Clonación de proyectos desde GitHub</li>
<li>Ejecución de aplicaciones web con Streamlit</li>
<li>Configuración de puertos en contenedores Docker</li>
<li>Resolución de problemas relacionados con mapeo de puertos</li>
</ul>

<hr>

<h2>Conclusión</h2>
<p>
Esta práctica permitió comprender el proceso completo de preparación
de un entorno de desarrollo para aplicaciones Python utilizando
Streamlit dentro de un contenedor Docker. Asimismo, se reforzaron
conocimientos relacionados con Linux, gestión de dependencias,
entornos virtuales y despliegue de aplicaciones web interactivas.
</p>

<p>
El uso de herramientas modernas como UV facilita la instalación
y gestión de dependencias en proyectos Python, mejorando la
velocidad y eficiencia en el desarrollo de aplicaciones.
</p>

<hr>

<p>
Autor: Edgar Eduardo Lopez Orozco<br>
Autor: Keyna vianney Villa Vera<br>
Materia: Computación en la Nube (361)<br>
Institución: Universidad Autónoma de Baja California
</p>
