# ARCHIVO 3: PM.CPF_260702-03_v2.7.md

### REGISTRO DE AUDITORÍA Y TRAZABILIDAD MEP
**Herramienta:** Calculador Pozo Fecales v2.7
**ID Informe Vinculado:** ITR.CPF_260702-03 v2.7
**Objetivo:** Replicar la aplicación completa v2.7 desde cero en una nueva sesión o IA.

---

**Copia y pega el siguiente texto en una nueva sesión de IA para generar el código de la aplicación:**

> **Rol:** Actúa como un Ingeniero Senior MEP y Desarrollador Full-Stack experto en herramientas de cálculo técnico.
> 
> **Objetivo:** Desarrollar una aplicación web autocontenida en un único archivo HTML (HTML5 + CSS3 Dark Industrial + JavaScript Vanilla) para el cálculo de un Pozo de Bombeo de Aguas Fecales. No utilices frameworks externos (ni React, ni Vue, ni librerías de componentes).
> 
> **Estructura de la Interfaz:**
> La aplicación debe tener un sistema de navegación por pestañas en la parte superior:
> 1. **Pestaña "Calculador MEP":** Contendrá los 4 módulos de cálculo.
> 2. **Pestaña "Prontuario Técnico":** Contendrá la justificación teórica y fórmulas en texto, renderizando ecuaciones con MathJax (vía CDN).
> 
> **Módulo 1: Caudal de Aporte (UD)**
> - Debe permitir seleccionar entre dos normativas mediante botones toggle: "CTE DB-HS5" y "UNE EN 12056".
> - Si se selecciona CTE DB-HS5: Mostrar un sub-toggle para "Uso Privado" o "Uso Público". Cargar los 17 aparatos de la tabla 4.1 del CTE.
> - Si se selecciona UNE EN 12056: Mostrar un sub-toggle para los Sistemas "I", "II", "III" y "IV". Cargar los 18 aparatos de la Tabla 1 de la norma europea.
> - Al cambiar de normativa, resetear las cantidades a 0 por seguridad.
> - Mostrar una tabla donde el usuario pueda introducir la cantidad de cada aparato. Calcular las UD parciales y las UD totales.
> - Calcular el caudal de aporte: $Q_{ap} = 0.5 \cdot \sqrt{UD_{totales}}$ (resultado en l/s y m3/h).
> 
> **Módulo 2: Volumen Útil del Pozo (Vu)**
> - Calcular el caudal de la bomba: $Q_b = 1.25 \cdot Q_{ap}$
> - Inputs de usuario: N.º máx. de arranques/hora ($n_{max}$) por defecto 10, y Diámetro interior del pozo (m) por defecto 1.2.
> - Selector de fórmula (Toggle):
>   - Opción A (Fabricante): $V_u = Q_b / (4 \cdot n_{max})$ (con Qb en m3/h).
>   - Opción B (Directa): $V_u = Q_b / n_{max}$.
> - Calcular el volumen útil calculado ($V_u$) y la altura útil calculada ($H_n$).
> 
> **Módulo 3: Ciclo de Bombeo y Verificación**
> - Input de usuario: N.º máx. arranques admisible (por defecto 10).
> - Input de usuario: "Volumen útil adoptado (litros)". Por defecto debe coger el valor de $V_u$ calculado en el Módulo 2. Si el usuario lo edita, mantener el valor del usuario.
> - Recalcular $H_n$ adoptada con este volumen.
> - Calcular tiempo de llenado: $t_{ll} = V_u / Q_{ap}$ (en minutos).
> - Calcular tiempo de vaciado: $t_v = V_u / (Q_b - Q_{ap})$ (en minutos).
> - Calcular arranques reales: $n_{real} = 60 / (t_{ll} + t_v)$.
> - Mostrar etiqueta CUMPLE (verde) si $n_{real} \le n_{max}$ admisible, o EXCEDE (rojo) si no.
> 
> **Módulo 4: Geometría Total del Pozo**
> - Inputs: $H_1$ (base bomba, def: 0.3), $H_2$ (seguridad, def: 0.3), $h$ (enterramiento, def: 0.2).
> - El valor $H_n$ viene arrastrado del Módulo 3.
> - Calcular $H_t = H_1 + H_n + H_2 + h$.
> - Generar un gráfico SVG dinámico usando `<rect>` y `<line>` que varíe las alturas proporcionalmente a los valores calculados, mostrando un esquema visual del pozo acotado.
> 
> **Generación de Informe Corporativo (PDF/HTML):**
> - Un botón que ejecute una función JS para exportar un HTML autónomo (que el usuario imprimirá a PDF).
> - Este HTML exportado debe tener un diseño limpio y corporativo: colores Azul (#003087) y Naranja (#F5A800).
> - Debe incluir: Cabecera con título, fecha, bases de cálculo y normativa elegida. Listado de aparatos introducidos y sus UDs. Cajas de resumen semafóricas para Qap, Qb, Vu adoptado, verificación de ciclo y alturas.
> - Debe inyectar el código SVG generado en el Módulo 4 directamente dentro del informe exportado para que se vea el gráfico.
> 
> **Requisitos técnicos y persistencia:**
> - El flujo debe ser en cascada (Top-Down Validation): Cambiar un aparato en M1 debe actualizar automáticamente hasta M4.
> - Usa `localStorage` para guardar en todo momento el estado (cantidades, toggles, inputs) y recuperarlo al recargar la página.
> - Las variables matemáticas en el DOM deben formatearse a 2 o 3 decimales para legibilidad.
