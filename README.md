# TALLER_2
DIG07 Taller 2. Reformulación de un modelo entero mixto

Programa: Doctorado en Ingeniería (UV–UTA)

Asignatura: DIG07 Investigación de Operaciones

Profesor: Schulze, E.
Fecha: Septiembre 2026

👥 Integrantes
- Pasmiño, Catherinne
- Jara, Felipe
- Arriagada, Jorge A.
- Pizarro, Patricio
- Andaur, Xenia 

Control de Versiones e Historial de Commits: El trabajo fue desarrollado en colaboración continua mediante un flujo de trabajo basado en git.


## 🚀 Descripción del Proyecto

Este repositorio contiene el estudio computacional de una reformulación sobre un modelo de programación lineal entera mixta (MILP) para **seleccionar métodos de mejoramiento de arenas sueltas**, con aplicación conceptual al terreno Las Salinas (Viña del Mar).

El sitio se divide en zonas, y el modelo asigna a cada una un método de mejoramiento aplicable a arenas (Han, 2015) y un contratista. Minimiza la suma de los costos fijos de movilización y los costos de tratamiento. Se comparan dos formulaciones equivalentes:

- **F1, vínculo agregado:** $\sum_{z\in Z_j} x_{zj} \le |Z_j|\,y_j$, una restricción por oferta.
- **F2, vínculo desagregado:** $x_{zj} \le y_j$, una restricción por par zona–oferta.

Corresponde a la transformación de desagregación de restricciones de vínculo (Vielma, 2015). El modelo está implementado en Pyomo y se resuelve con HiGHS.

**Resultado principal.** F1 y F2 alcanzan el mismo óptimo en las 15 instancias. La relajación de F2 coincide con el óptimo entero, mientras F1 deja brechas de 1,9 a 7,8 %. F2 resuelve entre 2,5 y 11,7 veces más rápido (promedio por tamaño), aunque ambas usan típicamente un solo nodo, porque los cortes de HiGHS cierran la brecha de F1 en el nodo raíz.

Las figuras y tablas completas están en `informe_taller2.pdf`.

## 🛠️ Cómo ejecutar

Requiere Python 3.10 o superior y Jupyter. **No hace falta instalar nada a mano:** la celda 1 del cuaderno revisa e instala lo que falte (Pyomo 6.10.1 y HiGHS 1.15.1 en las versiones fijadas, más NumPy, pandas y matplotlib). No se requieren licencias.

**Opción 1: ejecutar el cuaderno (recomendada).** Abre `taller2_mejoramiento_suelos.ipynb` en Jupyter Notebook, JupyterLab o VS Code y ejecuta todas las celdas en orden (*Restart & Run All*). Toma unos 5 a 10 minutos y escribe sus salidas en `resultados/`.

**Opción 2: desde la consola.**
```bash
pip install jupyter
jupyter execute taller2_mejoramiento_suelos.ipynb
```

**Qué debería ver:**
- **Celda 4:** `Instancia L20_s11: 400 zonas, 15 ofertas, 4362 pares admisibles`.
- **Celda 5:** `OK: óptimo idéntico ...`.
- **Celda 8:** `OK: 15 instancias con óptimo idéntico ...`.

Los óptimos, las cotas, los nodos y las dimensiones se reproducen exactamente. Los tiempos dependen del equipo, y el número de cortes puede variar levemente entre sistemas operativos (informe, sección 8).

## 👥 Integrantes
+ Arriagada, Jorge
+ [Integrante 2]

Control de versiones: el trabajo se desarrolló con un flujo basado en git; el historial de commits documenta su evolución.

## 🧭 Problema seleccionado

Problema propio de la línea de investigación (ingeniería geotécnica), no una de las alternativas A, B o C del enunciado. **Contexto:** el proyecto de saneamiento del terreno Las Salinas, de 15,8 ha, remueve y vuelve a colocar del orden de 10⁶ m³ de arena bajo la napa (Golder Associates, 2018). La edificación posterior requiere densificar ese terreno. Las instancias son sintéticas e inspiradas en ese contexto; no son datos del proyecto.

## 📋 Correspondencia con el enunciado (sección 6, Producto de entrega)

| Exigencia | Dónde está |
|---|---|
| Informe de 4 a 6 páginas | `informe_taller2.pdf` (6 páginas carta) |
| Código con ambas formulaciones sobre los mismos datos, seleccionadas por parámetro | Celda 5: `construir_modelo(inst, formulacion="F1" \| "F2")` |
| Instancias o generador con semilla declarada | Celda 4: `generar_instancia(L, semilla)`, con semillas 11, 22 y 33 (celda 3) |
| Cuaderno ejecutable que reproduce la tabla del informe | `taller2_mejoramiento_suelos.ipynb` (celdas 7 a 9) |
| Declaración de entorno | Celda 2 y `resultados/entorno.txt` |
| Verificación de equivalencia | Algebraica (informe, sección 3) y numérica (celda 8) |
| Respaldo de la discusión de H2 | Celda 10, `resultados/movilizacion.csv` |

# 📁 Estructura del Repositorio
```text
TALLER_2/
├── README.md                          # Cómo ejecutar, integrantes y correspondencia con el enunciado
├── informe_taller2.pdf                # Informe en formato de artículo (6 páginas)
├── taller2_mejoramiento_suelos.ipynb  # Cuaderno ejecutable de principio a fin (10 celdas):
│                                      #   1 instalación · 2 entorno · 3 parámetros · 4 generador
│                                      #   5 modelo F1/F2 · 6 medición · 7 experimento
│                                      #   8 equivalencia · 9 tablas y figuras
│                                      #   10 análisis complementario (movilización)
└── resultados/                        # Ejecución reportada en el informe
    ├── entorno.txt                    # Declaración de entorno
    ├── resultados.csv                 # Siete indicadores, 15 instancias × 2 formulaciones
    └── movilizacion.csv               # Participación de la movilización y brecha de F1 (celda 10)
```

Al ejecutar el cuaderno, `resultados/` se regenera completo: además de `resultados.csv`, se agregan la verificación de equivalencia, las tablas 1 y 2 del informe en CSV y las figuras.

## 🔬 Diseño experimental

- **Tamaños:** 5, en grillas de 10×10 a 50×50 zonas (100 a 2 500 zonas).
- **Sitios:** 3 por tamaño, con semillas 11, 22 y 33.
- **Corridas:** 2 formulaciones, con 3 repeticiones de cada resolución entera.
- **Solver:** HiGHS con un hilo, `random_seed = 0`, `mip_rel_gap = 1e-6` y límite de 120 s.
- **Indicadores:** cota de la relajación, óptimo entero, brecha de la relajación, nodos, cortes generados y activos, tiempo (media y desviación) y dimensión del modelo.

## 💲 Trazabilidad de los costos unitarios

Los precios unitarios base $u$ [USD/m³ de suelo tratado] se derivan de la tabla 1-6 de FHWA-NHI-16-027 (Schaefer et al., 2017; precios de noviembre de 2016). Conversión: 1 pie lineal = 0,3048 m; malla triangular con área tributaria 0,866·s²; para jet grouting, razón de reemplazo $a_s$.

| Método | FHWA (unidad original) | Supuesto de conversión | Rango [USD/m³] | $u$ usado | $f$ base [USD] |
|---|---|---|---|---|---|
| Compactación dinámica profunda (CDP) | 10–30 USD/yd² | 8 m tratados | 1,5–4,5 | 3,0 | 80 000 |
| Compactación por impacto rápido (CIR) | 1–2 USD/ft² y movilización 20 000–40 000 USD (Geo-Institute, 2018)* | 4–6 m tratados | 1,8–5,4 | 2,5 | 40 000 |
| Vibrocompactación (VCP) | 5–9 USD/pie lineal | s = 2,5–3,0 m | 2,1–5,5 | 4,0 | 120 000 |
| Columnas de grava (CGR) | 15–60 USD/pie lineal | s = 2,0 m | 14–57 | 25 | 150 000 |
| Jet grouting (JGR) | 250–750 USD/yd³ de columna | a_s = 0,25–0,35 | 82–343 | 180 | 220 000 |

\* La CIR no figura en la tabla de la FHWA; su costo proviene de la ficha *Rapid Impact Compaction Cost Information* del Geo-Institute de la ASCE (GeoTechTools, 2018), https://www.geoinstitute.org/node/8288.

**Costos fijos $f$:** la FHWA indica solo que la movilización va "desde unos cientos de dólares hasta más de 100 000 USD" según la tecnología; los valores usados son supuestos que respetan ese orden.

**Factores por contratista** (sobre $f$ y $u$, respectivamente):
- local: 0,6 y 1,10;
- nacional: 1,0 y 1,00;
- internacional: 1,8 y 0,90.

Cada oferta varía además ±10 % al azar, con la semilla de la instancia.


