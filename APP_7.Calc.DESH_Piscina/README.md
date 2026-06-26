# CALCULADORA AVANZADA MEP: DESHUMECTACIÓN Y POTENCIA TÉRMICA EN PISCINAS
**ID_INFORME:** ITR.CDP_260626-01 | **VERSIÓN:** 1.1  
**ESTADO:** ACEPTADO E IMPLEMENTADO

### 1. ESPECIFICACIONES TÉCNICAS
* **Orden del Usuario:** Desarrollar una herramienta web SPA para el cálculo integral de recintos de piscinas cubiertas. El alcance incluye:
    1. Cálculo de la carga latente (kg/h de agua a deshumectar) por evaporación, ocupación y ventilación.
    2. Cálculo de la potencia térmica requerida para el vaso de la piscina (kW), tanto para el calentamiento inicial como para el mantenimiento operativo.
* **Normativa:** RITE, ASHRAE Handbook (Natatoriums), VDI 2089.
* **Parámetros Validados:**
    * Superficie de agua (A): [m²] | Volumen del vaso (V): [m³]
    * Temperatura del agua (Tw): [ºC] | Temperatura del aire interior (Tint): [ºC]
    * Humedad Relativa interior (HRint): [%]
    * Temperatura inicial/red (Tred): [ºC] | Tiempo de calentamiento (t_cal): [h]
    * Caudal de ventilación (Qv): [m³/h] | Condiciones exteriores (Text, HRext).
    * Ocupantes (N) y Factor de Actividad (F).
* **Hipótesis y simplificaciones:**
    * Capacidad calorífica específica del agua ($c_p$) = 1.16 Wh/(kg·K).
    * Densidad del aire estándar = 1.2 kg/m³. Calor latente de vaporización ($h_{fg}$) = 0.68 kWh/kg.
    * *Nota técnica:* Se ha implementado un motor psicrométrico real. Si la humedad exterior absoluta es menor que la interior, la ventilación seca el local. Para diseño de capacidad máxima, se evalúa el aporte latente solo si el exterior es más húmedo.

### 2. LÓGICA DE INGENIERÍA Y CÁLCULOS
* **Módulo 1: Carga Latente y Deshumectación**
    1.  Cálculo de Presión de Saturación (Magnus-Tetens): $P_{sat} = 0.6112 \cdot \exp\left(\frac{17.67 \cdot T}{T + 243.5}\right)$
    2.  Humedad Absoluta: $x = 0.622 \cdot \frac{P_a}{101.325 - P_a}$
    3.  Evaporación ($\dot{m}_e$): $\dot{m}_e = A \cdot (P_w - P_{a,int}) \cdot F$
    4.  Ocupación ($\dot{m}_p$): $\dot{m}_p = N \cdot 0.15$
    5.  Ventilación ($\dot{m}_v$): $\dot{m}_v = Q_v \cdot \rho \cdot \max(0, x_{ext} - x_{int})$
* **Módulo 2: Potencia Térmica del Vaso**
    1.  Energía de Calentamiento ($Q_{ini}$): $Q_{ini} = V \cdot 1.16 \cdot (T_w - T_{red})$
    2.  Potencia de Arranque ($P_{arranque}$): $P_{arranque} = \frac{Q_{ini}}{t_{cal}}$
    3.  Pérdidas Térmicas por Evaporación ($P_{evap}$): $P_{evap} = \dot{m}_e \cdot 0.68$
    4.  Potencia de Mantenimiento ($P_{maint}$): $P_{maint} = P_{evap} + P_{otras}$

### 3. HISTORIAL DE REQUERIMIENTOS ACUMULADOS
* [Implementado] Interfaz con 3 pestañas (Panel de Cálculo, Informe, Documentación).
* [Implementado] Input de datos de geometría, condiciones psicrométricas y térmicas.
* [Implementado] Motor de cálculo psicrométrico y termodinámico en JS.
* [Implementado] Generación de informe justificativo imprimible detallando fórmulas MEP.
* [Implementado] Renderizado de ecuaciones con MathJax.

### 6. BITÁCORA DE CAMBIOS (Changelog)
* **v1.0:** Creación del ITR inicial centrado en el balance de masa de agua (deshumectación).
* **v1.1:** Incorporación de ecuaciones de balance de energía térmica para el vaso (calentamiento y mantenimiento).

### 7. STACK TECNOLÓGICO Y LIBRERÍAS
* HTML5 / CSS3 (impresión optimizada). JavaScript ES6 Vanilla.
* MathJax v3 vía CDN.
