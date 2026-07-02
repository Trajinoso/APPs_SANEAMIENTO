# ARCHIVO 1: README.md (Actualizado v2.7)

# Calc Pozo Fecales
### Calculador de Pozo de Bombeo de Aguas Residuales Fecales
**Versión actual:** v2.7 | **Normativa:** CTE DB-HS5 / UNE EN 12056 | **Tecnología:** HTML5 + JS (autocontenido)
**VINCULADO A INFORME ACEPTADO:** ITR.CPF_260702-03 v2.7

---

## Descripción general

**Calc Pozo Fecales** es una herramienta de cálculo técnico para el dimensionado de pozos de bombeo de aguas residuales fecales, desarrollada para uso en Oficina Técnica MEP. Permite determinar, de forma encadenada y automática, el caudal de aporte a partir de las Unidades de Descarga (UD), el volumen útil del pozo, la verificación del ciclo de bombeo y la geometría total.

La herramienta es un archivo HTML autocontenido, sin dependencias externas de servidor, que incorpora un sistema dual de normativas, una interfaz de usuario por pestañas y generación nativa de informes corporativos.

---

## Módulos de cálculo y Estructura

### Pestaña 1: Calculador MEP
* **Módulo 1 — Caudal de aporte:** Selección dual interactiva entre **CTE DB-HS5** (uso privado/público) o **UNE EN 12056** (Sistemas I a IV). Cálculo por fórmula: Qap = 0,5 · √UD.
* **Módulo 2 — Volumen útil:** Selector de ecuación paramétrica. Opción 1: Fórmula de Fabricante (Vu = Qb / 4·nmax). Opción 2: Fórmula Directa (Vu = Qb / nmax).
* **Módulo 3 — Ciclo de bombeo:** Verificación de arranques reales mediante tiempos de retención e iteración con un Volumen Adoptado comercial introducido por el usuario.
* **Módulo 4 — Geometría paramétrica:** Cálculo de cotas de resguardo (H1, H2), altura útil (Hn) y solera (h) para obtener la profundidad total. Generación dinámica de un esquema SVG proporcional.

### Pestaña 2: Prontuario Técnico
* Justificación teórica MEP de todos los parámetros utilizados.
* Desarrollo del cálculo diferencial para la comprobación del caudal crítico (Qap = Qb/2) y validación del divisor "4" en la fórmula volumétrica de los fabricantes.
* Criterios normativos sobre prevención de septicidad y requerimientos NPSHr para inmersión de volutas.

---

## Historial de Requerimientos y Bitácora (Changelog)

* **v1.0 a v2.4 (Implementado):** Base del cálculo estocástico de UDs, geometría, encadenamiento en cascada (Top-Down Validation) y variables de persistencia en navegador (localStorage).
* **v2.6 (Implementado):** Integración paralela de la norma UNE EN 12056 y selector de la ecuación volumétrica en el Módulo 2.
* **v2.7 (Actual):**
    * Implementación de Pestañas de Navegación UI (Calculador / Prontuario).
    * Integración del "Prontuario Técnico" con renderizado de matemática avanzada (MathJax/LaTeX).
    * Reescritura de la función de exportación HTML para inyectar dinámicamente las variables y el SVG generado directamente sobre la plantilla corporativa ELECNOR estricta.

---

## Flujo de cálculo encadenado (Top-Down Validation)

1. Selección Norma (CTE / UNE) → Tabla aparatos → UD totales
2. Q_ap = 0,5 · √UD  [l/s]
3. Q_b = 1,25 · Q_ap  [m³/h]
4. Selección Ecuación Vu → Vu_calc
5. Vu_adoptado → Hn_adoptado
6. t_ll, t_v, T, n_real → Verificación arranques (n_real ≤ n_max admisible)
7. Ht = H₁ + Hn_adoptado + H₂ + h  [m] → Diagrama SVG y Reporte PDF

---

## Tecnología

- **HTML5 + CSS3 + JavaScript vanilla** — Single-Page App sin dependencias estructurales.
- **MathJax (CDN)** — Renderizado del prontuario matemático.
- **Generador HTML a PDF** — Replicación nativa de estilos para impresión corporativa.