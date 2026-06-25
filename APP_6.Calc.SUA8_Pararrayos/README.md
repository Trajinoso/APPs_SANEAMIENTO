
# CALCULADORA PARARRAYOS CTE SUA 8 Y DIMENSIONADO PDC - MANUAL TÉCNICO

**ID_DOCUMENTO:** RE_SUA8_2026-DOC | **VERSIÓN ACUMULADA:** v1.3

**ESTADO DEL PROYECTO:** CONSOLIDADO, AMPLIADO Y COMPLETO

Este documento técnico funciona como la **Única Fuente de Verdad** y el manual de ingeniería definitivo para la aplicación interactiva de cálculo de riesgo y dimensionamiento de protección contra el rayo, estructurada estrictamente bajo los parámetros del Código Técnico de la Edificación (CTE DB-SUA 8) y la norma UNE 21186.

---

## 1. DESCRIPCIÓN GENERAL Y FUNCIONAMIENTO

La aplicación es una herramienta web interactiva autocontenida (*Single File App*) diseñada para ingenieros y proyectistas MEP. Permite realizar tanto la evaluación analítica de riesgo frente a la acción del rayo en cualquier edificación dentro del territorio español, como el posterior diseño geométrico de la instalación exterior captadora.

### Características Principales de Operación

* **Cálculo Reactivo Bidireccional:** Toda modificación en los campos geométricos de la estructura ($L, W, H$), coeficientes normativos o parámetros del mástil ($h, \Delta t, R_{max}$) recalcula de forma inmediata tanto el riesgo analítico como el dictamen de cobertura volumétrica en pantalla mediante eventos del DOM.
* **Persistencia de Datos Local:** Almacenamiento automático y transparente en el navegador (`window.localStorage`), asegurando la retención de los parámetros del último proyecto analizado al recargar o reabrir el archivo.
* **Layout de Impresión Profesional:** Incluye estilos optimizados mediante *media queries* CSS (formato DIN A4) que heran la paleta cromática corporativa (Azul Elecnor: `#004687` y Naranja: `#FF8200`), facilitando el anexo directo de la memoria técnica a los proyectos ejecutivos de edificación.

---

## 2. MARCO NORMATIVO DE REFERENCIA

El motor de cálculo unifica de manera estricta las especificaciones de dos marcos regulatorios complementarios:

1. **Código Técnico de la Edificación (CTE DB-SUA 8):** Regula la obligatoriedad de la instalación y determina el Nivel de Protección exigido mediante el balance de frecuencias de impacto.
2. **Norma UNE 21186:** Rige el diseño geométrico, el avance técnico del trazador y las inecuaciones que gobiernan el radio de protección horizontal para tecnologías dotadas de Dispositivos de Cebado (PDC).

### Coeficientes Normativos de Entorno y Estructura (CTE SUA 8)

* **Coeficiente $C_1$: Factor de Emplazamiento**

| Situación del Edificio | Valor de $C_1$ |
| --- | --- |
| Próximo a otros edificios o árboles de la misma altura o más altos | 0,50 |
| Rodeado de edificios más bajos | 0,75 |
| Aislado en terreno llano | 1,00 |
| Aislado sobre una colina o promontorio | 2,00 |

* **Coeficiente $C_2$: Función del Tipo de Construcción (Estructura / Cubierta)**

| Estructura / Cubierta | Cubierta Metálica | Cubierta de Hormigón | Cubierta de Madera |
| --- | --- | --- | --- |
| **Metálica** | 0,50 | 1,00 | 2,00 |
| **Hormigón** | 1,00 | 1,00 | 2,50 |
| **Madera** | 2,00 | 2,50 | 3,00 |

* **Coeficientes Adicionales de Operación y Uso**
* **$C_3$ (Contenido):** **3,00** para edificios con contenido inflamable, reactivo o explosivo; **1,00** para contenidos ordinarios no inflamables.
* **$C_4$ (Ocupación):** **0,50** para estructuras no ocupadas habitualmente; **3,00** para Pública Concurrencia, Sanitario, Comercial o Docente; **1,00** para uso residencial o administrativo estándar.
* **$C_5$ (Continuidad pública):** **5,00** para servicios imprescindibles (hospitales, bomberos, telecomunicaciones) o riesgo ambiental grave; **1,00** para el resto de edificios.



---

## 3. FORMULACIÓN Y DESARROLLO ANALÍTICO

Las ecuaciones operan bajo el Sistema Internacional de Unidades (SI) y se despliegan en la interfaz desglosando cada variable con el punto centrado ($\cdot$) como operador explícito de multiplicación.

### 3.1. Superficie de Captura Equivalente ($A_e$)

Representa el área crítica de la estructura delimitada por una línea trazada a una distancia de **3H** de su perímetro. Para bases rectangulares ortogonales se define como:

$$A_e = (L \cdot W) + 6H \cdot (L+W) + 9\pi \cdot H^2$$

### 3.2. Frecuencia Anual Esperada de Impactos ($N_e$)

Representa el número previsible de impactos directos de rayos anuales calculados sobre la superficie del inmueble:

$$N_e = N_g \cdot A_e \cdot C_1 \cdot 10^{-6}$$

### 3.3. Frecuencia de Riesgo Admisible ($N_a$)

Constituye el umbral de seguridad normativo máximo tolerado para la configuración arquitectónica y operativa propuesta:

$$N_a = \frac{5,5 \cdot 10^{-3}}{C_2 \cdot C_3 \cdot C_4 \cdot C_5}$$

### 3.4. Eficiencia Requerida del Sistema ($E$)

Determina la tasa de efectividad mínima que debe garantizar la instalación externa captadora si se supera el umbral tolerable:

$$E = 1 - \frac{N_a}{N_e}$$

### 3.5. Avance del Trazador Ascendente ($\Delta L$) - UNE 21186

Parámetro físico que evalúa la distancia de anticipación de descarga conseguida por el dispositivo de cebado (PDC) en función de su tiempo de cebado certificado ($\Delta t$):

$$\Delta L = v \cdot \Delta t$$

> **Nota de Auditoría MEP:** La velocidad de propagación está fijada por norma en $v = 1\text{ m}/\mu\text{s}$. El valor máximo admisible de $\Delta t$ para el cálculo se encuentra acotado estrictamente a **60 µs**, ignorando valores superiores de catálogo por coeficientes de seguridad de laboratorio.

### 3.6. Radio de Protección Geométrico ($R_p$) - UNE 21186

El cálculo del radio de amparo horizontal a una distancia vertical $h$ (altura del mástil desde la punta hasta el plano superior a proteger) se divide en dos regímenes debido a la estabilización del trazador:

* **Para Alturas de Mástil $h \ge 5\text{ m}$:**

$$R_p(h) = \sqrt{2rh - h^2 + \Delta L(2r + \Delta L)}$$

* **Para Alturas Críticas Intermedias $2\text{ m} \le h < 5\text{ m}$:**

$$R_p(h) = h \cdot \frac{R_p(5)}{5}$$

---

## 4. CONDICIONES DE OBLIGATORIEDAD Y EXCEPCIONES ESPECIALES

El dictamen definitivo de instalación obligatoria se activa bajo tres supuestos independientes controlados por lógica booleana:

1. **Evaluación de Frecuencias:** Condición estándar si la tasa anual esperada sobrepasa el umbral admisible ($N_e > N_a$).
2. **Excepción por Altura Crítica:** Si la altura máxima perimetral es estrictamente superior a **43 m** ($H > 43\text{ m}$), la instalación se declara obligatoria con un requerimiento mínimo de Eficiencia Máxima ($E \ge 0,98$, Nivel I), ignorando el balance de frecuencias.
3. **Excepción por Sustancias Peligrosas:** Estructuras destinadas a la manipulación de sustancias tóxicas, explosivas o altamente inflamables activan automáticamente la obligatoriedad con eficiencia máxima ($E \ge 0,98$, Nivel I).

### Determinación del Nivel de Protección Exigido (Tabla 2.1 del CTE)

Asociado directamente al valor de la esfera rodante teórica ($r$) empleado en las fórmulas volumétricas de la norma UNE 21186:

* **Nivel I:** $E \ge 0,98 \implies r = 20\text{ m}$ (Máxima exigencia de diseño).
* **Nivel II:** $0,95 \le E < 0,98 \implies r = 30\text{ m}$.
* **Nivel III:** $0,80 \le E < 0,95 \implies r = 45\text{ m}$.
* **Nivel IV:** $0 \le E < 0,80 \implies r = 60\text{ m}$.

---

## 5. ARQUITECTURA GRÁFICA DE LA INTERFAZ (BOXES EXCLUSIVOS)

Para una lectura scannable, la aplicación organiza visualmente el análisis mediante componentes modulares de control:

* **Boxes de Desarrollo Analítico Detallado:** Bloques con fondo `#ffffff`, sombra sutil y borde izquierdo de realce de 5 px en azul corporativo (`--elecnor-blue`). Muestran en tiempo real la sustitución numérica de los inputs del formulario dentro de las expresiones formales de LaTeX.
* **Box de Demostración Visual de Riesgo ($N_e > N_a$):** Un contenedor interactivo centralizado que contrasta los impactos esperados frente a los tolerables. Conmuta dinámicamente el operador lógico ($>$ o $\le$) y altera su color de fondo y texto: rojo de advertencia (`--danger-color`) si se requiere protección, o verde de seguridad (`--success-color`) si el riesgo se mantiene bajo control.
* **Box de Verificación de Cobertura Geométrica ($R_p \ge R_{max}$):** Evalúa el cruce de datos entre el radio real del pararrayos ($R_p$) y el radio crítico real de la edificación ($R_{max}$). Si la inecuación falla, emite un badge dinámico de alerta indicando la presencia de "Zonas Vulnerables" no cubiertas por el cono de protección.
* **Box Exclusivo del Informe (Nivel de Protección):** Destaca en la memoria imprimible el nivel normativo final obtenido (Nivel 1 al 4) y el radio de la esfera rodante asignada, facilitando la rápida auditoría por parte de los organismos de control técnico (OCT).

---

## 6. BITÁCORA DE CAMBIOS ACUMULATIVA (CHANGELOG)

* **v1.0 (24/06/2026) - Entrega Inicial Basada en CTE SUA 8**
* Consolidación del motor matemático para $A_e$, $N_e$, $N_a$ y eficiencia $E$.
* Desarrollo de la interfaz con selectores interactivos para coeficientes $C_1$ a $C_5$.
* Implementación de persistencia de datos mediante la API `window.localStorage`.


* **v1.1 (24/06/2026) - Refinamiento Semántico e Indicadores de Riesgo**
* Supresión de textos no funcionales y etiquetas de depuración del entorno visual.
* Adición del Box interactivo biestable para contrastar en caliente la inecuación de riesgo $N_e > N_a$.
* Inclusión del bloque independiente de nivel de protección en el informe técnico DIN A4.


* **v1.2 (24/06/2026) - Integración de Bloques Analíticos de Referencia**
* Programación de contenedores de desarrollo analítico en el panel derecho.
* Ajuste sintáctico en ecuaciones matemáticas para la sustitución explícita de valores numéricos reales con puntos centrados ($\cdot$).


* **v1.3 (25/06/2026) - Módulo de Dimensionado Geométrico y Cobertura (Versión Actual)**
* Integración de la lógica de diseño para terminales PDC conforme a la norma **UNE 21186**.
* Programación de las variables de mástil: Altura efectiva ($h$), tiempo de cebado ($\Delta t$), avance de trazador ($\Delta L$) y radio de control de la edificación ($R_{max}$).
* Implementación del modelo matemático dual por tramos ($h \ge 5\text{ m}$ y $h < 5\text{ m}$) para determinar con precisión el radio de amparo ($R_p$).
* Rediseño y estructuración total de la tercera pestaña, sustituyendo el código Markdown crudo por una sección interactiva de **Explicación Técnica y Normativa** orientada al ingeniero MEP.
