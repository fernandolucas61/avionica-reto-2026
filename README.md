# Reto de Ingreso – División de Aviónica (AAIAQ) | Ruta 2

**Autor:** Fernando Lucas Hernández  
**Programa:** Licenciatura en Tecnología – ENES Juriquilla, UNAM  
**Versión:** `v1.0`  
**Fecha:** 21 de noviembre de 2026  

---

## Descripción del Proyecto

Este repositorio contiene el diseño esquemático, las simulaciones SPICE y la documentación técnica de dos etapas de acondicionamiento analógico para un sistema de adquisición de datos (ADC de 12 bits, $V_{\text{ref}} = 3.3\text{ V}$):

1. **Parte A – Filtro Anti-Aliasing Sallen-Key:** Filtro pasa-bajas activo de 2.º orden con respuesta Butterworth ($f_c \approx 150\text{ Hz}$) basado en el amplificador operacional *rail-to-rail* **MCP6002**, diseñado para preservar una señal útil de $10\text{ Hz}$ y atenuar ruido de alta frecuencia ($\ge 1\text{ kHz}$).
2. **Parte B – Monitor de Batería LiPo 2S:** Divisor resistivo de bajo consumo ($R_3 = 62\text{ k}\Omega$, $R_4 = 33\text{ k}\Omega$, $I_{\max} = 88.42\ \mu\text{A}$) para escalar el rango de $6.0\text{ V}$ a $8.4\text{ V}$ dentro del margen seguro de entrada del ADC ($\le 3.0\text{ V}$).

---

## Herramientas Utilizadas

* **Diseño Esquemático y Simulación SPICE:** KiCad E.D.A. `10.0.8`
* **Documentación Técnica:** LaTeX (`pdflatex` / Overleaf)
* **Control de Versiones:** Git `2.56.1` y GitHub

---

## Estructura del Repositorio

```text
avionica-reto-2026/
├── src/          # Archivos de proyecto (.kicad_pro) y esquemáticos (.kicad_sch)
├── docs/         # Reporte técnico compilado en PDF (3 páginas) y código fuente (.tex)
├── media/        # Exportaciones del esquemático formal y gráficas de simulación (Bode AC y Transitorio)
└── README.md     # Documentación general del proyecto