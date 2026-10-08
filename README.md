# TALLER_2
DIG07 Taller 2. Reformulación de un modelo entero mixto

Programa: Doctorado en Ingeniería (UV–UTA)
Asignatura: DIG07 Investigación de Operaciones Profesor: Schulze, E. Fecha: Septiembre 2026

👥 Integrantes
Pasmiño, Catherinne
Jara, Felipe
Arriagada, Jorge
??
??
Control de Versiones e Historial de Commits: El trabajo fue desarrollado en colaboración continua mediante un flujo de trabajo basado en git.

# 🚀 Descripción del Proyecto
## Objetivo
Establecer, mediante evidencia computacional controlada, el efecto de una reformulación sobre el desempeño de un modelo de programación lineal entera mixta, manteniendo invariante el conjunto de soluciones enteras factibles.
Criterio de evaluación. No se evalúa la magnitud de la mejora obtenida.
Se evalúa la validez del diseño experimental y la consistencia entre la evidencia producida y las conclusiones enunciadas. Una reformulación cuyo efecto resulte nulo, correctamente medida y discutida, recibe la misma calificación que una cuyo efecto sea sustantivo.

# 🛠️ Cómo ejecutar

# Producto de entrega
Un repositorio de acceso público o compartido con ambos académicos, que contenga los siguientes elementos.
Informe de entre cuatro y seis páginas, en formato de artículo científico: planteamiento del problema y su vinculación con la línea de investigación; las dos formulaciones en notación
matemática completa; la hipótesis sobre cuál debiera resultar superior y su fundamento; los resultados en forma tabular; y la discusión. 
Con referencias bibliográficas.
Código, en Pyomo o en el lenguaje de modelado algebraico que el equipo prefiera, estructurado de modo que ambas formulaciones compartan los datos y se seleccionen
mediante un parámetro.
Instancias, o bien el generador que las produce, con la semilla declarada.
Cuaderno de resultados ejecutable de principio a fin, que reproduzca la tabla del informe.
Declaración de entorno: versiones de las bibliotecas y del solver empleados

# 📁 Estructura del Repositorio
Taller_2/
├── README.md           # Cómo ejecutar, integrantes e instancia asignada
├── cuaderno.ipynb      # Desarrollo, verificación y respuestas
├── modelo.py           # Formulación en Pyomo, sin datos incrustados
├── datos/              # Los CSV entregados, sin modificar
│   ├── nodos.csv
│   └── arcos.csv
└── resultados/
    ├── solucion.csv    # Flujos óptimos arco por arco
    └── duales.csv      # Valores duales de los nodos
