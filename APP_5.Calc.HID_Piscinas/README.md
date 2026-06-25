Aquí tienes un archivo `README.md` completo, riguroso y estructurado a nivel profesional para el repositorio del proyecto. Está diseñado integrando las especificaciones de la aplicación HTML/JS, la lógica de ingeniería detallada en el Informe de Requerimientos Técnicos (ITR) y las directrices del Master Prompt (PM), incluyendo la bitácora de cambios oficial.

---

# CalcPisc — Calculadora Hidráulica de Piscinas (v1.3)

`CalcPisc` es una aplicación de ingeniería web interactiva de código abierto diseñada para el **cálculo, dimensionado preliminar y verificación hidráulica de piscinas** de uso público y colectivo. La herramienta automatiza la evaluación geométrica, los caudales de renovación normativos, el área de filtración requerida, la velocidad de paso por tuberías por tramos y la caracterización de los grupos de bombeo, emitiendo un informe técnico dinámico y estructurado listo para su exportación a PDF.

Este desarrollo se rige de forma estricta bajo el principio de **Documentation-Driven Development (DDD)**, asegurando que toda línea de código ejecute exactamente los algoritmos convalidados en el Informe de Requisitos Técnicos adjunto.

---

## 🚀 Características y Módulos Principales

La aplicación se estructura en una arquitectura limpia dividida en tres pestañas operativas:

### 1. Pestaña: Calculadora Hidráulica

* **M1 · Geometría:** Deducción automática del volumen total ($m^3$), superficie de lámina de agua ($m^2$) y profundidad media a partir de datos de longitud, anchura y profundidades extremas.
* **M2 · Filtración:** Cálculo de caudales de diseño según tiempos de renovación normativos (con factor de compensación por vaso). Selección de filtros comerciales normalizados basados en la velocidad de filtración real y máxima admisible ($m/h$).
* **M3 · Tuberías:** Pre-dimensionado y cálculo de diámetros comerciales e internos en PVC PN10 para los colectores críticos del sistema: Aspiración, Impulsión, Recogida/Rebosadero y Lavado.
* **M4 · Bomba:** Estimación paramétrica de la potencia teórica del motor ($kW$ y $CV$) requerida en el punto de diseño a partir del número de bombas en paralelo, la Altura Manométrica Total ($HMT$) introducida y la eficiencia termomecánica del conjunto.

### 2. Pestaña: Tablas de Referencia

Centraliza las bases de datos técnicas estáticas utilizadas para las restricciones de cálculo:

* Velocidades máximas normativas por tramo de tubería.
* Catálogo de diámetros comerciales de filtros normalizados con sus respectivas superficies de filtración ($m^2$).
* Catálogo de tuberías de PVC PN10 con sus diámetros interiores netos y caudales máximos límite recomendados por velocidad.

### 3. Pestaña: Informe Resumen

* Generación en tiempo real de una memoria de cálculo dividida en 6 secciones formalizadas.
* Maquetación CSS nativa con directivas `@media print` para generar un reporte PDF limpio y profesional a través de la función de impresión del sistema (`window.print()`), ocultando la interfaz interactiva.

---

## 🧮 Fundamentos de Ingeniería y Algoritmos

Toda la lógica de computación utiliza de forma estricta el **Sistema Internacional de Unidades (SI)**.

### A. Volumen y Superficie

$$S_{vaso} = L \times A$$

$$V_{vaso} = S_{vaso} \times \left(\frac{h_{min} + h_{max}}{2}\right)$$

$$V_{total} = V_{vaso} \times \left(1 + \frac{\%_{comp}}{100}\right)$$

### B. Caudales y Filtración

El caudal mínimo de recirculación exigido por diseño:


$$Q_{dise\tilde{n}o} = \frac{V_{total}}{t_{renovacion}}$$

Para la validación de filtros de área comercial ($S_{com}$):


$$Q_{real} = S_{com} \times v_{filtracion} \times N_{filtros}$$

$$Q_{max} = S_{com} \times v_{filtracion\_max} \times N_{filtros}$$

### C. Dimensionado de Tuberías (PVC PN10)

A partir de la velocidad máxima paramétrica ($v_{tramo}$), se obtiene el diámetro interior mínimo teórico ($D_{int\_teorico}$):


$$D_{int\_teorico} = \sqrt{\frac{4 \times Q_{tramo}}{\pi \times v_{tramo}}}$$


El script realiza un barrido matricial sobre la serie normalizada de PVC PN10 para seleccionar el diámetro comercial cuyo diámetro interior neto ($D_{interior}$) sea inmediatamente superior al teórico, recalculando la velocidad real de paso para comprobar que no supere los límites físicos del material.

### D. Potencia Hidráulica de Bombeo

$$Q_{bomba} = \frac{Q_{real}}{N_{bombas}}$$

$$P_{motor} = \frac{\rho \times g \times Q_{bomba} \times HMT}{3600 \times \eta_{bomba} \times \eta_{motor}}$$


*Donde $\rho \approx 1000 \text{ kg/m}^3$, $g \approx 9.81 \text{ m/s}^2$, con eficiencias ($\eta$) expresadas en base 1.*

---

## 🛠️ Tecnologías e Implementación

* **Core Lógico:** JavaScript Vanilla (ES6). Cálculos deterministas directos y mapeo matricial de arrays para la selección de componentes. No requiere librerías ni frameworks pesados de terceros.
* **Interfaz de Usuario:** HTML5 semántico y CSS3 avanzado utilizando propiedades personalizadas (`--variables`), transiciones suaves y arquitectura adaptativa mediante Flexbox y CSS Grid (Mobile-First de alta fidelidad).
* **Fuentes:** Integración de la familia tipográfica *IBM Plex Sans* e *IBM Plex Mono* para garantizar legibilidad técnica.
* **Dependencias:** 0% dependencias externas. No requiere conexión a CDNs para operar los motores de cálculo principales.

---

## 💻 Despliegue y Uso

Al tratarse de una aplicación basada estrictamente en **Client-Side Rendering (CSR)**, su ejecución es local e instantánea:

1. Clonar el repositorio:
```bash
git clone https://github.com/tu-usuario/calcpisc.git

```


2. Abrir el entorno:
* Haga doble clic en el archivo `CalcPisc_CPSC_260410-01_v1.3.html` desde cualquier navegador web moderno (Chrome, Edge, Firefox, Safari).
* Alternativamente, si desea servirlo en una red local de la oficina técnica:
```bash
python -m http.server 8000

```


E ingrese a `http://localhost:8000`.



---

## 📋 Cumplimiento Normativo (Marco de Referencia)

Los algoritmos y rangos recomendados en la interfaz están parametrizados en conformidad con los siguientes textos legales y normas técnicas vigentes en territorio español y europeo:

* **RD 742/2013:** Criterios técnico-sanitarios de las piscinas.
* **CTE DB-HS4:** Código Técnico de la Edificación - Salubridad (Suministro de agua).
* **UNE-EN 13451 / UNE-EN 16713-1:** Equipamiento para piscinas y sistemas de distribución hidráulica.
* **Especificación de Materiales:** Dimensiones e interiores normativos para tuberías de PVC Presión PN10.

---

## 📜 Bitácora de Cambios (Versionado Oficial)

* **v1.3 (2026-04-10) — Estado: ACEPTADO [Versión Actual]**
* *M4:* Eliminación completa del campo de texto de modelo comercial de bomba y sus referencias en el árbol del DOM y JavaScript para evitar duplicidades con las curvas de selección de fabricantes.
* *M3:* Adición de bloques de texto descriptivos inline (`.vel-desc`) bajo cada input de velocidad, indicando el rango normativo y el criterio técnico de diseño.
* *Tablas:* Implementación de la pestaña "Tablas de Referencia" poblada dinámicamente mediante funciones JS (`poblarTablasFiltros`, `poblarTablasPVC`) al inicializar la aplicación.
* *Informe:* Rediseño del módulo de informe dinámico (`generarInforme`), estructurado en 6 secciones completas con soporte optimizado para exportación PDF mediante `window.print()` y reglas `@media print`.


* **v1.2 (2026-04-10) — Estado: ACEPTADO**
* Corrección y ajuste fino en las ecuaciones de cálculo y acoplamiento hidráulico de bombas en configuración paralelo.


* **v1.1 (2026-04-10) — Estado: ACEPTADO**
* Eliminación del cálculo automático preliminar de pérdidas de carga singulares en favor de un campo de entrada manual para la Altura Manométrica Total ($HMT$) requerida en el proyecto.


* **v1.0 (2026-04-10) — Estado: ACEPTADO**
* Lanzamiento del informe inicial y estructura base del motor de cálculo geométrico y de filtración.



---

## ⚠️ Limitaciones del Modelo

> [!IMPORTANT]
> * **Curvas de Bomba:** La aplicación estima la potencia del motor requerida basándose en un punto de diseño estático de caudal y presión ($HMT$). No sustituye la simulación sobre la curva característica del fabricante ni valida el punto de operación real (BEP).
> * **NPSH (Cavitación):** No se realiza la comprobación del NPSH disponible frente al requerido. Dicha validación debe ser ejecutada por el ingeniero responsable considerando la geometría específica de la tubería de aspiración y la temperatura del fluido.
> * **Pérdidas de Carga:** La $HMT$ es un valor de entrada parametrizado manualmente; las pérdidas lineales y singulares del circuito hidráulico exterior deben calcularse previamente mediante métodos tradicionales (Darcy-Weisbach o Hazen-Williams).
> 
>
