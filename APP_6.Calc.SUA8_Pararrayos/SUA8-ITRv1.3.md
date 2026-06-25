He comprendido el protocolo de ingeniería MEP y el sistema de ITR incremental. Estoy listo para indexar la información. Por favor, proporcione el nombre del proyecto y los detalles de la app a desarrollar.

Información indexada correctamente para el contexto del proyecto. A continuación, presento el **Informe Técnico de Requisitos (ITR)** inicial para expandir la aplicación actual e integrar el módulo de dimensionamiento geométrico de mástiles y radios de protección de pararrayos según la normativa UNE 21186 y el CTE DB-SUA 8.

---

# CALCULADORA AVANZADA CTE SUA 8 Y DIMENSIONADO DE PARARRAYOS PDC

**ID_INFORME:** ITR.PARARRAYOS_260625-01 | **VERSIÓN:** v1.0

**ESTADO:** ESPERANDO ACEPTACIÓN TÉCNICA

### 1. ESPECIFICACIONES TÉCNICAS

* **Orden del Usuario:** Ampliar la herramienta existente de evaluación de necesidad de pararrayos (CTE DB-SUA 8) para incluir el cálculo iterativo del mástil de un pararrayos con dispositivo de cebado (PDC) conforme a la norma UNE 21186. Se requiere verificar si el radio de protección ($R_p$) cubre la diagonal máxima de la edificación ($R_{max}$) y rediseñar la interfaz manteniendo tres pestañas (Panel de Cálculo, Informe Técnico Regulado, Explicación Técnica y Normativa).
* **Normativa:** * Código Técnico de la Edificación: Documento Básico SUA 8 (Seguridad frente al riesgo causado por la acción del rayo).
* Norma UNE 21186: Protección contra el rayo: Pararrayos con dispositivo de cebado.


* **Parámetros Validados:**
* Nivel de Protección Obligatorio (I, II, III, IV) obtenido automáticamente del cálculo de riesgo o forzado por el usuario.
* Tiempo de cebado del cabezal PDC ($\Delta t$) en microsegundos ($\mu\text{s}$), limitado normativamente a un máximo de 60 $\mu\text{s}$.
* Altura del mástil ($h$) en metros (m), evaluando de forma diferenciada tramos de $2\text{ m} \le h < 5\text{ m}$ y $h \ge 5\text{ m}$.
* Radio máximo o diagonal de la cubierta a proteger ($R_{max}$) en metros (m).


* **Hipótesis y Simplificaciones:**
* El pararrayos se ubica en el centro de gravedad o punto crítico de la instalación desde donde se mide la distancia radial máxima a proteger ($R_{max}$).
* La velocidad de propagación del trazador ascendente se fija por norma en $v = 1\text{ m}/\mu\text{s}$.



### 2. LÓGICA DE INGENIERÍA Y CÁLCULOS

* **Check de Indexación:** Se han analizado los datos del archivo HTML base adjunto. El módulo reactivo existente calcula con éxito $A_e$, $N_e$, $N_a$ y define si la instalación es obligatoria y su nivel de protección correspondiente.
* **Determinación de Variables Críticas según el Nivel de Protección:**
El radio de la esfera rodante teórica ($r$) se asocia directamente al nivel de protección determinado por el CTE:
* Nivel I: $r = 20\text{ m}$ (Eficiencia: 98%)
* Nivel II: $r = 30\text{ m}$ (Eficiencia: 95%)
* Nivel III: $r = 45\text{ m}$ (Eficiencia: 91%)
* Nivel IV: $r = 60\text{ m}$ (Eficiencia: 84%)


* **Cálculo del Avance de Cebado ($\Delta L$):**

$$\Delta L = v \cdot \Delta t$$



Donde $v = 1\text{ m}/\mu\text{s}$ y $\Delta t \le 60\ \mu\text{s}$.
* **Ecuación de Cobertura para Alturas $h \ge 5\text{ m}$:**

$$R_p(h) = \sqrt{2rh - h^2 + \Delta L(2r + \Delta L)}$$


* **Modelo de Comprobación para Alturas $2\text{ m} \le h < 5\text{ m}$:**
Para el rango crítico inferior ($2\text{ m} \le h < 5\text{ m}$), dado que la geometría del trazador no está completamente estabilizada, se implementará la matriz de coeficientes y valores normalizados indexados de la norma UNE 21186, calculados mediante interpolación o aplicando el factor de reducción proporcional sobre el valor base de 5 metros:

$$R_p(h) = h \cdot \frac{R_p(5)}{5}$$



*(Nota: Se incluirá también la tabla explícita normalizada de la norma para los valores comerciales exactos de $h = 2\text{ m}$, $h = 3\text{ m}$ y $h = 4\text{ m}$ según el $\Delta t$ seleccionado para asegurar la máxima fidelidad regulatoria).*
* **Criterio de Validación de Ingeniería (Dictamen Geométrico):**
* Si $R_p(h) \ge R_{max}$: **CUMPLE**. El volumen proyectado envuelve la estructura.
* Si $R_p(h) < R_{max}$: **NO CUMPLE**. Se requiere alertar al usuario para que aumente la altura del mástil ($h$) o elija un cabezal con mayor tiempo de cebado ($\Delta t$).



### 3. HISTORIAL DE REQUERIMIENTOS ACUMULADOS

* **v1.0 (Fase Actual):** * Módulo de cálculo analítico de necesidad de pararrayos según CTE DB-SUA 8 (Implementado en HTML base).
* Integración del módulo de cálculo iterativo de altura de mástil ($h$) y radio de protección ($R_p$) según UNE 21186 (Pendiente de codificación).
* Rediseño de la tercera pestaña para mostrar la "Explicación Técnica y Normativa" del algoritmo iterativo en lugar del código Markdown crudo (Pendiente de codificación).



### 4. ESPECIFICACIONES DE LA VERSIÓN ACTUAL (v1.0)

* **Nuevos Componentes de Interfaz:**
* Campos de entrada en el Panel de Cálculo: Altura del Mástil ($h$), Tiempo de cebado del PDC ($\Delta t$), Radio máximo de cobertura requerido ($R_{max}$).
* Sección de resultados gráficos y analíticos que compare $R_p$ frente a $R_{max}$ con badges dinámicos (Cumple / No Cumple).


* **Estrategia de Manejo de Errores:**
* Limitación por JavaScript del valor máximo de $\Delta t$ a 60 $\mu\text{s}$ (si el usuario introduce un valor mayor, el cálculo se forzará a 60 $\mu\text{s}$ con un mensaje de advertencia normativa).
* Validación de rangos para impedir alturas de mástil inferiores a 2 metros.



### 5. STACK TECNOLÓGICO

* **Definición Técnica:** HTML5, CSS3 corporativo (Elecnor Blue & Orange), JavaScript Nativo (ES6) sin dependencias de servidor, y renderizado matemático mediante MathJax v3.

### 6. BITÁCORA DE CAMBIOS (CHANGELOG)

* **v1.0 (Diseño Inicial):** Unificación del cálculo de riesgo CTE DB-SUA 8 y el dimensionamiento geométrico de pararrayos de cebado UNE 21186.

### 7. FUNDAMENTOS DE INGENIERÍA Y NORMATIVA

* **Sistema Internacional (SI):** Todas las variables se expresarán en metros (m), microsegundos ($\mu\text{s}$) e impactos por kilómetro cuadrado año ($\text{imp/km}^2\cdot\text{año}$).
* **Ecuaciones en Plantilla:** Visualización dinámica de la fórmula de la raíz cuadrada en el panel de resultados y en la memoria técnica descargable.

### 8. LIBRERÍAS TÉCNICAS

* `MathJax.js` (para renderizado de ecuaciones fluidas en pantalla).

### 9. IMPLEMENTACIÓN

*(Sección vacía a la espera de aprobación formal del ITR).*

---

⚠️ **ESPERANDO ACEPTACIÓN TÉCNICA.** Por favor, revisa los puntos anteriores y escribe 'ACEPTO INFORME' para proceder con el código, o indica los cambios necesarios. En caso de aceptar el informe, solicita también el lenguaje en cual se hará el código.
