<h1>📝 Write-up de Pentesting: Vulnerabilidad en WordPress</h1>

<p>Este write-up cubre los pasos básicos para realizar un análisis de seguridad en un sitio WordPress utilizando herramientas comunes. Se cubren los pasos desde el descubrimiento de subdominios hasta el escaneo profundo utilizando WPScan con un API Token.</p>

<h2>📌 Paso 1: Encontrar subdominios mediante fuzzing con <code>Gobuster</code></h2>

<p>Ejecutamos el siguiente comando para encontrar subdominios de <code>10.10.151.30</code> y buscamos directorios comunes:</p>
<pre><code>gobuster dir -u http://10.10.151.30/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt</code></pre>

<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>gobuster dir</code>: Inicia Gobuster para hacer fuzzing de directorios (buscar directorios y archivos comunes).</li>
    <li><code>-u http://10.10.151.30/</code>: Especifica la URL del objetivo, en este caso el sitio web.</li>
    <li><code>-w /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt</code>: Utiliza un diccionario de directorios comunes para el fuzzing.</li>
</ul>
<img src="https://github.com/luiszero303/guia-practica-wpscan/blob/main/paso1-wpscan.png" alt="Ejecución de Gobuster" width="450" height="200">

<h2>📌 Paso 2: Identificar tecnologías utilizando <code>WhatWeb</code> y <code>Wappalyzer</code></h2>

<p>Ahora usamos <code>WhatWeb</code> y <code>Wappalyzer</code> para analizar las tecnologías utilizadas en el sitio web.</p>
<pre><code>whatweb http://10.10.151.30</code></pre>
<pre><code>wappalyzer https://10.10.151.30</code></pre>

<h3>🔍 Explicación de los comandos:</h3>
<ul>
    <li><code>WhatWeb</code>: Herramienta que detecta tecnologías como CMS, frameworks y servidores.</li>
    <li><code>Wappalyzer</code>: Extensión de navegador que detecta tecnologías y es útil para análisis visual.</li>
</ul>
<div style="display: flex; gap: 10px;">
    <img src="https://github.com/luiszero303/guia-practica-wpscan/blob/main/paso2-1wpscan.png" alt="Ejecución de WPScan 1" width="450" height="200">
    <img src="https://github.com/luiszero303/guia-practica-wpscan/blob/main/paso2-2wpscan.png" alt="Ejecución de WPScan 2" width="450" height="200">
</div>

<h2>📌 Paso 3: Enumerar usuarios con <code>WPScan</code></h2>

<p>Para enumerar los usuarios de WordPress, ejecutamos el siguiente comando con <code>WPScan</code>:</p>
<pre><code>wpscan --url http://10.10.151.30 --enumerate u</code></pre>

<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>wpscan</code>: Herramienta especializada en la detección de vulnerabilidades en WordPress.</li>
    <li><code>--url http://10.10.151.30</code>: Especifica la URL del sitio objetivo.</li>
    <li><code>--enumerate u</code>: Enumera los usuarios de WordPress encontrados en el sitio.</li>
</ul>
<img src="https://github.com/luiszero303/guia-practica-wpscan/blob/main/paso3wpscan.png" alt="Ejecución de Gobuster" width="450" height="200">
<h2>📌 Paso 4: Escaneo más profundo con <code>WPScan</code> utilizando el API Token</h2>

<p>Para un análisis más profundo, podemos usar el API Token con <code>WPScan</code> para obtener detalles adicionales:</p>
<pre><code>wpscan --url http://10.10.151.30 --enumerate p --api-token YOUR_API_TOKEN</code></pre>

<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>--enumerate p</code>: Enumera los plugins instalados en el sitio WordPress.</li>
    <li><code>--api-token YOUR_API_TOKEN</code>: Usamos un token de API para acceder a información más detallada sobre vulnerabilidades conocidas.</li>
</ul>
<img src="https://github.com/luiszero303/guia-practica-wpscan/blob/main/paso4wpscan.png" alt="Ejecución de Gobuster" width="450" height="200">
<h2>🎯 Conclusión</h2>
<ul>
    <li>🔹 Realizamos fuzzing con <code>Gobuster</code> para encontrar directorios ocultos.</li>
    <li>🔹 Identificamos las tecnologías del sitio con <code>WhatWeb</code> y <code>Wappalyzer</code>.</li>
    <li>🔹 Enumeramos usuarios de WordPress con <code>WPScan</code> para posibles ataques de fuerza bruta.</li>
    <li>🔹 Realizamos un análisis detallado de los plugins con el API Token de <code>WPScan</code>.</li>
</ul>

<p>Con estas herramientas y técnicas, podemos identificar vulnerabilidades en un sitio WordPress mal configurado o inseguro. 🚀</p>
