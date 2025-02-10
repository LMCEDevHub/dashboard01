📊 Extracción y Limpieza de Datos de Ingresos de Empresas

📝 Descripción

Este proyecto utiliza Python y Pandas para extraer, limpiar y transformar los datos de ingresos de diversas empresas desde una página web. La información procesada puede ser utilizada para análisis financieros y visualizaciones.

🔧 Requisitos

Asegúrate de tener instaladas las siguientes dependencias antes de ejecutar el código:

pip install pandas beautifulsoup4 requests

🚀 Uso

El código realiza las siguientes acciones:
1️⃣ Extrae datos de una tabla HTML utilizando BeautifulSoup.
2️⃣ Limpia los datos eliminando caracteres no deseados ($ y ,).
3️⃣ Convierte la columna de ingresos a valores numéricos.
4️⃣ Filtra valores nulos y datos vacíos.

🖥️ Extracto del Código

import pandas as pd
from bs4 import BeautifulSoup
import requests

# 📂 Crear DataFrame vacío
ingresos_empresas = pd.DataFrame(columns=["Empresa", "Date", "Revenue"])

# 🌍 Obtener datos de la página web
url = "URL_DE_LA_PAGINA"
response = requests.get(url)
soup = BeautifulSoup(response.text, "html.parser")

# 📊 Extraer datos de la tabla
for row in soup.find("tbody").find_all("tr"):
    col = row.find_all("td")
    empresa = col[0].text
    date = col[1].text
    revenue = col[2].text
    ingresos_empresas = pd.concat([ingresos_empresas, pd.DataFrame({"Empresa": [empresa], "Date": [date], "Revenue": [revenue]})], ignore_index=True)

# 🧹 Limpiar datos
ingresos_empresas["Revenue"] = ingresos_empresas["Revenue"].str.replace(",|\$", "", regex=True)
ingresos_empresas.dropna(inplace=True)
ingresos_empresas = ingresos_empresas[ingresos_empresas["Revenue"] != ""]

📂 Archivo Dashboard.ipynb

Incluye un notebook de Jupyter con la implementación del código, análisis y visualización de datos.

🤝 Contribuciones

Si deseas contribuir, por favor crea un fork del repositorio y envía un pull request con tus mejoras.