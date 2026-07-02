# Calc Pozo Fecales
### Calculador de Pozo de Bombeo de Aguas Residuales Fecales
**Versión actual:** v2.6 | **Normativa:** CTE DB-HS5 (Tabla 4.1) / UNE EN 12056 (Tabla 1) | **Tecnología:** HTML5 + JS (autocontenido)
**VINCULADO A INFORME ACEPTADO:** ITR.CPF_260702-02 v2.6

---

## Descripción general

**Calc Pozo Fecales** es una herramienta de cálculo técnico para el dimensionado de pozos de bombeo de aguas residuales fecales, desarrollada para uso en Oficina Técnica MEP. Permite determinar, de forma encadenada y automática, el caudal de aporte a partir de las Unidades de Descarga (UD) de los aparatos sanitarios instalados, el volumen útil del pozo, la verificación del ciclo de bombeo y la geometría total del pozo.

La herramienta es un archivo HTML autocontenido, sin dependencias externas de servidor ni frameworks, con exportación de memoria de cálculo en PDF (vía HTML) y con un sistema dual de normativas y metodologías de cálculo.

---

## Características principales

- **Doble Normativa (NUEVO v2.6):** Tablas de aparatos sanitarios completas según **CTE DB-HS5 Tabla 4.1** (uso privado/público) y **UNE EN 12056 Tabla 1** (Sistemas I, II, III y IV).
- **Cálculo de caudal de aporte** por fórmula normativa generalizada: `Q_ap = 0,5 · √UD`
- **Dimensionado de volumen útil dinámico (NUEVO v2.6):** Selector para elegir entre el criterio clásico de fabricantes de bombas sumergidas (`Vu = Qb / (4 · n_max)`) o el cálculo volumétrico directo especificado por el usuario (`Vu = Qb / n_max`).
- **Verificación de ciclo de bombeo:** Tiempos de llenado/vaciado y arranques reales por hora interactuando con un Volumen Adoptado introducido por el usuario.
- **Módulo de geometría total del pozo** con diagrama SVG dinámico (H₁, Hn, H₂, h, Ht).
- **Encadenamiento automático** entre módulos: los resultados fluyen sin intervención manual en cascada (Top-Down Validation).
- **Persistencia de datos:** Los parámetros se guardan localmente (`localStorage`) para recuperar la sesión.
- **Exportación de memoria de cálculo** en **PDF** con diseño corporativo ELECNOR.

---

## Módulos de cálculo

### Módulo 1 — Caudal de aporte por Unidades de Descarga (UD)
- Sistema de pestañas para alternar entre **CTE DB-HS5** y **UNE EN 12056**.
- Toggle interactivo de sub-sistemas (Privado/Público para CTE; Sistemas I a IV para UNE).
- Cálculo automático de UD parciales y UD totales acumuladas.
- Fórmula de conversión compartida: `Q_ap = 0,5 · √UD_totales` (l/s).
- Al cambiar de norma, por seguridad e integridad de los datos, el recuento de aparatos se reinicia a cero.
- Resultado propagado automáticamente al Módulo 2.

### Módulo 2 — Volumen útil del pozo (Vu)
- Caudal de aporte recibido en lectura desde Módulo 1 (campo readonly).
- Caudal de bomba: `Q_b = 1,25 · Q_ap`.
- **Selector de Formulación Volumétrica:**
  - *Fórmula Fabricante (Clásica):* `Vu = Qb(m³/h) / (4 · n_max)`
  - *Fórmula Directa (Usuario):* `Vu = Qb(m³/h) / n_max`
- Toda la cadena de cálculo posterior (Hn, ciclo de bombeo, geometría) usa el Vu calculado a partir de la fórmula seleccionada.
- Altura útil: `Hn = Vu / (π · (D/2)²)`

### Módulo 3 — Ciclo de bombeo y verificación de arranques
- Q bomba propagado automáticamente desde Módulo 2.
- Input para que el usuario inserte el **Volumen Adoptado (L)** según depósitos comerciales (toma el calculado del Módulo 2 por defecto).
- Cálculo de tiempos: `t_ll = Vu_adopt / Q_ap`, `t_v = Vu_adopt / (Q_b - Q_ap)`
- Ciclo total: `T = t_ll + t_v` | Arranques reales: `n_real = 60/T`
- Verificación semáforo: ✓ CUMPLE / ✗ EXCEDE respecto a n_max admisible.

### Módulo 4 — Geometría total del pozo
- Entradas: H₁ (base bomba), H₂ (seguridad sobre nivel máximo), h (enterramiento/solera).
- Altura útil Hn propagada automáticamente desde el Módulo 3.
- Profundidad total: `Ht = H₁ + Hn + H₂ + h`
- Diagrama SVG dinámico proporcional a los valores introducidos con cotas etiquetadas.

### Memoria de cálculo
- Resumen completo de todos los módulos con trazabilidad de fórmulas (incluyendo norma y ecuación de Vu utilizadas).
- Exportación en **PDF** (Generación de documento HTML corporativo imprimible nativamente).

---

## Normativa y referencias técnicas

| Referencia | Aplicación |
|---|---|
| **CTE DB-HS5** | Evacuación de aguas. Tabla 4.1: UDs por aparato sanitario (Privado/Público). |
| **UNE EN 12056-2** | Sistemas de desagüe por gravedad en edificios. Tabla 1: UD según Sistemas I, II, III, IV. |
| **Fabricantes** (Grundfos/KSB) | Fórmula clásica `Vu = Qb/(4·n_max)` (criterio de ciclo mínimo y arranques máximos). |
| **Ingeniería MEP** | Fórmula de conversión `Q_ap = 0,5 · √UD` (K=0,5). |

---

## Historial de Requerimientos y Bitácora de Desarrollo (Changelog)

* **v1.0 (Implementado):** Tabla de aparatos CTE DB-HS5 interactiva. Cálculo automático de UD y Qap.
* **v2.0 (Implementado):** Encadenamiento total de Módulo 1 a Módulo 4. Módulo de geometría con SVG dinámico integrado.
* **v2.2 (Implementado):** Eliminación de mínimos rígidos en el volumen útil. 
* **v2.3 (Implementado):** Rediseño completo de exportación a PDF corporativo ELECNOR (vía HTML) en lugar de txt.
* **v2.4 (Implementado):** Entrada de "Volumen útil adoptado" manual por el usuario que recalcula el ciclo. Persistencia de estado en `localStorage`. 
* **v2.5 (Integrado en v2.6):** Solicitud para incluir la UNE EN 12056 y la dualidad de fórmulas en el Volumen Útil.
* **v2.6 (Actual):** - **Módulo 1:** Incorporación de pestañas para cambiar entre bases de datos de CTE DB-HS5 y UNE EN 12056 (Sistemas I a IV).
  - **Módulo 2:** Toggle para seleccionar la ecuación de Volumen Útil (`Qb / 4·nmax` vs `Qb / nmax`).
  - **Global:** Actualización del motor de persistencia y de la función de exportación de memoria para registrar qué normativa y fórmula se han empleado durante la sesión.

---

## Flujo de cálculo encadenado (Top-Down Validation)

```text
[Selección Norma: CTE o UNE] → [Tabla aparatos] → UD totales
       ↓
Q_ap = 0,5 · √UD  [l/s]
       ↓
Q_b = 1,25 · Q_ap  [m³/h]
       ↓
[Selección Ecuación Vu] → Vu_calc = Q_b / (4·n_max)  ó  Q_b / n_max  [m³]
       ↓
Vu_adoptado (Editable, por defecto = Vu_calc)
Hn_adoptado = Vu_adoptado / (π·(D/2)²)  [m]
       ↓
t_ll, t_v, T, n_real → Verificación arranques (n_real ≤ n_max admisible)
       ↓
Ht = H₁ + Hn_adoptado + H₂ + h  [m]  → Geometría total