# MEMORIA TÉCNICA REVISADA: BASE DE CÁLCULO DEL CAUDAL DE APORTACIÓN Y CÁMARA DE BOMBEO SEGÚN EL CTE DB-HS 1 (APÉNDICE C, APARTADO B) CON DESARROLLO ANALÍTICO DE "R"

---

## 1. Contexto Físico y Justificación Normativa (Apartado b)

Este módulo de cálculo se aplica cuando **el arranque del muro de sótano no alcanza ninguna capa impermeable**. A diferencia del caso anterior, el agua subterránea no queda bloqueada por la estructura de cimentación; existe un espacio de terreno permeable bajo la zapata o losa que permite el flujo tridimensional del agua (by-pass hidráulico).

El agua de la capa freática puede ascender por debajo de la cimentación y presionar la solera o filtrarse a través de la cámara bufa. Para mitigar esto, el sistema de drenaje rebaja el nivel freático de forma local, modelándose hidrodinámicamente mediante una fórmula que incluye un factor de corrección por penetración parcial del drenaje en el acuífero.

---

## 2. Formulación Analítica del Caudal Lineal (Fórmula C.3)

De acuerdo con el **Apéndice C, apartado 1.b) del CTE DB-HS 1**, el caudal de drenaje por metro lineal de muro ($q$), expresado en $\text{m}^3/(\text{s}\cdot\text{m})$, se calcula mediante la siguiente ecuación:

$$q = \frac{K_s \cdot \left[0,73 + 0,27 \cdot \frac{H - h_o}{H}\right] \cdot (H^2 - h_o^2)}{2R}$$

### Análisis de los Componentes de la Fórmula:

* **$K_s$**: Coeficiente de permeabilidad del terreno $\left[\text{m/s}\right]$. *(Para limos arcillosos, adoptamos tu valor $K_s = 2,5 \cdot 10^{-7} \text{ m/s}$)*.
* **$H$**: Espesor del acuífero libre antes de la intervención $\left[\text{m}\right]$. Representa la distancia vertical entre la cara superior de la capa impermeable profunda (detectada en el geotécnico) y el Nivel Freático Original (NF).
* **$h_o$**: Espesor del acuífero modificado en la zona del drenaje $\left[\text{m}\right]$. Es la distancia vertical desde la capa impermeable profunda hasta el punto donde se sitúa la canaleta de la cámara bufa o el tubo drenante.
* **$R$**: Radio de acción del drenaje o cono de depresión $\left[\text{m}\right]$.
* **Factor $\left[0,73 + 0,27 \cdot \frac{H - h_o}{H}\right]$**: Coeficiente adimensional corrector que compensa que el drenaje sea "colgado" o superficial respecto a la base del acuífero.

---

## 3. Desarrollo y Justificación Técnica del Radio de Acción ($R$)

El texto literal del CTE DB-HS 1 define a **$R$** como *"el radio de acción del drenaje, equivalente a la distancia de la zona de recarga del acuífero"*, pero no incluye una ecuación matemática explícita en su articulado, remitiendo implícitamente a los métodos reconocidos de la herencia de la mecánica de fluidos y la geotecnia.

Para la justificación formal del proyecto ante los organismos de control técnico (OCT), el desarrollo analítico de $R$ se realiza mediante la **Ecuación Empírica de Sichardt**, adaptada a las variables geométricas del **Apartado b**:

### A. Ecuación de Desarrollo

En un escenario donde el drenaje no corta el estrato impermeable, la depresión o descenso real del nivel freático ($s$) en el entorno del muro viene dada por la diferencia entre el espesor inicial del acuífero y el espesor modificado en el eje de recogida:

$$s = H - h_o$$

Sustituyendo el descenso $s$ en la formulación hidrodinámica de Sichardt, el radio de acción se desarrolla como:

$$R = 3000 \cdot (H - h_o) \cdot \sqrt{K_s}$$

Donde:

* **$R$**: Radio de acción medido en metros $\left[\text{m}\right]$.
* **$(H - h_o)$**: Depresión neta del nivel freático obtenida a pie de muro $\left[\text{m}\right]$.
* **$K_s$**: Coeficiente de permeabilidad del terreno en metros por segundo $\left[\text{m/s}\right]$.

### B. Sensibilidad del Parámetro con $K_s = 2,5 \cdot 10^{-7} \text{ m/s}$

Sustituyendo el valor de permeabilidad proporcionado para tu terreno permeable de limos arcillosos, la ecuación operativa de diseño queda definida como:

$$R = 3000 \cdot (H - h_o) \cdot \sqrt{2,5 \cdot 10^{-7}}$$

$$R = 3000 \cdot (H - h_o) \cdot 0,0005$$

$$R = 1,5 \cdot (H - h_o)$$

> **Implicación Teórica Crítica:** Este desarrollo demuestra que en terrenos limoso-arcillosos el radio de acción es extremadamente contraído ($R$ es apenas 1,5 veces el descenso del agua). El cono de depresión será muy vertical y localizado. Esto significa que la mayor parte del esfuerzo hidráulico que recibe la cámara bufa se debe a la presión hidrostática vertical inmediata, reduciendo el riesgo de afectar a edificaciones colindantes situadas más allá de esta distancia $R$.

---

## 4. Desarrollo Operativo del Caudal Total del Edificio ($Q_{inf}$)

Una vez calculado $R$ con la fórmula de Sichardt, se sustituye su valor en el denominador de la ecuación principal (C.3) para obtener el caudal lineal $q$. Posteriormente, se integra todo el perímetro del sótano para obtener el caudal total de aportación que ingresa al pozo de bombeo:

$$Q_{inf} = q \cdot L_{muro}$$

Donde $L_{muro}$ es la longitud total en metros de los muros de contención que están en contacto con el terreno inundado.

### Conversión Hidráulica Obligatoria:

Para la posterior selección de los equipos mecánicos de bombeo en catálogos comerciales, el caudal de aportación se transforma de $\text{m}^3/\text{s}$ a unidades de explotación práctica:

$$Q_{inf} \left[\text{m}^3/\text{h}\right] = Q_{inf} \left[\text{m}^3/\text{s}\right] \cdot 3600$$

---

## 5. Dimensionamiento de la Cámara de Bombeo Asociada

El pozo de bombeo debe actuar como un vaso receptor capaz de gestionar el caudal calculado por el Apéndice C sin comprometer la mecánica de los motores ni la estabilidad del suelo.

### A. Caudal de Diseño de las Bombas ($Q_b$)

De acuerdo con los márgenes de seguridad para filtraciones subterráneas estipulados de forma combinada entre el DB-HS 1 y el DB-HS 5, el caudal nominal de la bomba debe sobredimensionarse para absorber puntas de infiltración por lluvias estacionales:


$$Q_b \ge 1,25 \cdot Q_{inf}$$

### B. Geometría Prescriptiva del Vaso (Exigencia Literal del DB-HS 1)

Aunque el caudal calculado mediante la fórmula C.3 para un terreno limoso ($K_s = 2,5 \cdot 10^{-7} \text{ m/s}$) sea volumétricamente bajo, el diseño físico de la cámara no es libre:

* **Sección Mínima:** El diámetro interior neto del pozo circular (o lado menor si es rectangular) tiene que ser **igual o mayor a 0,7 metros** ($\varnothing \ge 0,7 \text{ m}$).
* **Equipos Mínimos:** Se exige la instalación de **dos (2) bombas sumergibles idénticas** montadas sobre pie de acoplamiento rápido. Funcionarán en régimen de **alternancia automática** para asegurar un desgaste homogéneo.

### C. Volumen Útil de Regulación ($V_u$)

Para evitar que los motores eléctricos sufran sobrecalentamiento por arranques continuos, el volumen geométrico útil (espacio entre el nivel de arranque y el nivel de parada de la bomba) se calcula bajo la siguiente restricción termomecánica:

$$V_u = \frac{Q_b}{4 \cdot z}$$

Donde:

* $V_u$: Volumen útil requerido $\left[\text{m}^3\right]$.
* $Q_b$: Caudal de la bomba seleccionada $\left[\text{m}^3/\text{h}\right]$.
* $z$: Frecuencia máxima de arranques del motor permitida por el fabricante. En estaciones de drenaje soterradas se fija por seguridad en **$z = 10 \text{ h}^{-1}$** (10 arranques por hora).
