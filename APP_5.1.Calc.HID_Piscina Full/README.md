# PISCINA PÚBLICA · Sistema Hidráulico Completo (Dashboard MEP v1.0)

`MEP-DSH-01` es una infografía técnica interactiva y cuadro de mando (Dashboard) desarrollado en entorno web para la visualización, auditoría visual y documentación de salas técnicas de filtración, hidráulica y climatización en piscinas de uso público.

Este módulo complementa a las herramientas de cálculo numérico proporcionando un esquema gráfico unificado de los flujos de procesos bajo normativas estatales y europeas.

---

## 🚀 Características del Cuadro de Mando

* **Interfaz de Alta Fidelidad Técnica:** Diseñado bajo una estética de modo oscuro optimizada para terminales de control en oficinas de ingeniería o salas de supervisión.
* **Esquema de Flujos Integrado:** Representación visual clara de la distribución hidráulica de la instalación: vaso principal, vaso de compensación, colectores de aspiración, etapa de filtrado, intercambiadores de calor y sistemas de dosificación química.
* **Análisis de Pérdidas Térmicas:** Gráfico interactivo (`Chart.js`) incorporado para la visualización del balance energético y pérdidas calóricas en la lámina de agua (evaporación, radiación, convección y conducción).
* **Documentación en Código:** Estructura limpia basada en componentes web puros, modular y adaptable.

---

## 📋 Marco Normativo de Referencia

La infografía indexa y organiza conceptualmente los componentes mecánicos de acuerdo con las siguientes normativas vigentes:
* **RD 742/2013:** Criterios técnico-sanitarios de la calidad del agua de piscinas.
* **UNE-EN 13451:** Equipamiento para piscinas (Requisitos generales de seguridad y métodos de ensayo).
* **RITE (RD 1027/2007 mod. RD 178/2021):** Reglamento de Instalaciones Térmicas en los Edificios.
* **CTE DB HE-4:** Contribución mínima de energía renovable para agua caliente sanitaria y climatización de piscinas.
* **RD 3/2023:** Criterios técnico-sanitarios de la calidad del agua de consumo humano.

---

## 🛠️ Tecnologías y Librerías Utilizadas

El desarrollo se ejecuta completamente en el lado del cliente (*Client-Side*) empleando:
* **HTML5 Semántico y CSS Grid / Flexbox:** Arquitectura responsiva y estructurada sin frameworks pesados comerciales.
* **Chart.js (v4.4.0):** Generación y renderizado dinámico del gráfico de distribución de pérdidas térmicas del vaso.
* **Mermaid.js (v10.6.1):** Motor de generación de diagramas de bloques y lógica de procesos a partir de texto plano.
* **Tipografías Técnicas:** Uso de las familias tipográficas *Share Tech Mono* y *Barlow* de Google Fonts para emular terminales de control industrial.

---

## 💻 Requerimientos de Despliegue

La aplicación es un archivo único autocontenido. Para su correcta visualización, se requiere una conexión a internet activa para descargar las dependencias de los CDNs en la primera carga:

1. Clone el repositorio o descargue el archivo `CalcPisc_Infografia_v1.0.html`.
2. Abra el archivo en cualquier navegador web moderno que soporte el estándar ES6 (Chrome, Edge, Firefox o Safari).
3. Para fines de demostración en red local, puede servir el directorio mediante Python:
   ```bash
   python -m http.server 8080
