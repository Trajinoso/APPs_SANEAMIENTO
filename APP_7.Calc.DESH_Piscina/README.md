# ENTORNO DE INSTALACIONES MEP: CALCULADORA DE DESHUMECTACIÓN Y TÉRMICA DE PISCINAS
**ID_INFORME:** ITR.CDP_260626-01 | **VERSIÓN:** 1.4  
**ESTADO:** ACEPTADO E IMPLEMENTADO

Este repositorio contiene la herramienta web autocontenida (SPA) para el dimensionado mecánico y de fluidos en piscinas cubiertas (natatorios). El aplicativo garantiza una trazabilidad completa desde los requisitos técnicos hasta las ecuaciones aplicadas de balance de masa y energía térmica.

## HISTORIAL ACUMULADO DE INFORMES TÉCNICOS (ITR)

* **Versión 1.0 - Balance de Masa Básico:** Modelado analítico de la carga latente de deshumectación considerando evaporación libre superficial, ocupación y caudal de renovación exterior (ASHRAE).
* **Versión 1.1 - Balance de Energía Térmica:** Adición del módulo de transferencia de calor para el agua del vaso (potencia de arranque inicial vs. mantenimiento).
* **Versión 1.2 - Optimización Geométrica y Psicrometría Vectorial:** Cálculo automático de volumen ($V = A \cdot h_{vaso}$) y corrección algebraica del aire exterior para evaluar su vector de secado (resta carga si es más seco, suma si es más húmedo) mediante formulación de Magnus-Tetens.
* **Versión 1.3 - Estándar VDI 2089:** Implementación de la norma alemana VDI 2089. La evaporación se calcula en base al salto de humedad absoluta en g/kg y coeficientes de agitación $\beta$ (0.5 a 4.0).
* **Versión 1.4 - Prontuario Técnico Integrado (Versión Actual):** Cancelación del sub-módulo Free-Drying. Transformación de la pestaña de auditoría en un Prontuario Técnico Interactivo. Se exponen y justifican matemáticamente (vía MathJax) todas las fórmulas de estado psicrométrico, balances latentes y sensibles.

---

## STACK TECNOLÓGICO
* **Frontend y Lógica:** HTML5, CSS3, Vanilla JS (Cálculos ejecutados en local, sin dependencias de servidor).
* **Renderizado Matemático:** MathJax v3 para visualización de ecuaciones analíticas dinámicas y estáticas en LaTeX.