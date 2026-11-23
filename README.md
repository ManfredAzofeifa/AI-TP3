# TP3 — Redes neuronales

Base del Trabajo Práctico 3 de Principios de Inteligencia Artificial, para un
equipo de tres personas. **Estado: acuerdos de T0 en revisión; solución en
desarrollo** (ver [JOURNAL.md](JOURNAL.md)).

La organización parte de
[AI-TP1](https://github.com/AleQuesada2012/AI-TP1/tree/74153d802c817c0401d39cf5a9684aad1c85c354),
adaptada al nuevo enunciado. No se copiaron implementaciones, experimentos,
resultados, informes ni documentación generada de ese proyecto.

El enunciado está en
[docs/assignment/TP_3_redes_neuronales.pdf](docs/assignment/TP_3_redes_neuronales.pdf).
Indica entrega el **domingo 29 de noviembre de 2026**; no especifica hora.

## Por dónde comenzar

1. Leer [JOURNAL.md](JOURNAL.md): reparto, dependencias, pendientes y dudas del PDF.
2. Preparar el entorno (abajo) y el clon según [CONTRIBUTING.md](CONTRIBUTING.md).
3. Seguir [CONTRIBUTING.md](CONTRIBUTING.md): cada persona trabaja en su rama
   y en sus secciones del notebook, e integra en `main` de una en una.

[AGENTS.md](AGENTS.md) indica a los asistentes que deben revisar el journal
antes de trabajar y actualizarlo al terminar.

## Una sola solución

El archivo [notebooks/tp3_redes_neuronales.ipynb](notebooks/tp3_redes_neuronales.ipynb)
es el único notebook del proyecto. Tiene un encabezado por sección, con su
responsable, y la configuración común en la sección 0. `.ipynb` es la
extensión estándar de los notebooks de Jupyter.

Allí se escriben todas las respuestas, implementaciones, pruebas unitarias,
gráficas, tablas, referencias y conclusiones. No habrá soluciones en módulos
Python auxiliares ni notebooks individuales por integrante.

El PDF pide también fuentes LaTeX/LyX, un PDF y un ZIP para TEC Digital. Cuando
el notebook esté terminado (T8), el equipo redacta un informe en LaTeX en
`docs/report/` (T9); no es una exportación del notebook.

## Estructura

```text
AI-TP3/
├── .github/pull_request_template.md  # Plantilla opcional y breve
├── AGENTS.md                        # Instrucciones para asistentes
├── CONTRIBUTING.md                  # Flujo en paralelo por ramas
├── JOURNAL.md                       # Plan, responsables y pendientes
├── .python-version                  # Python 3.15.0
├── README.md
├── requirements.txt                 # Versiones exactas acordadas en T0
├── data/
│   ├── raw/.gitkeep                 # Datos originales locales
│   └── processed/.gitkeep           # Datos preparados locales
├── docs/
│   ├── assignment/
│   │   ├── TP_3_redes_neuronales.pdf      # Enunciado
│   │   └── EstimacionIncertidumbre.pdf    # Material de apoyo: ensambles y ECE
│   └── report/sections/.gitkeep      # Informe LaTeX de T9
├── notebooks/
│   └── tp3_redes_neuronales.ipynb    # Solución única, versionada sin salidas hasta T8
├── results/
│   ├── figures/.gitkeep
│   └── tables/.gitkeep
└── submission/
    └── .gitkeep                     # Reserva de entrega; sin PDF ni ZIP final
```

Se conservan las carpetas principales del TP1 y se agrega `data/` para
UNSW-NB15. Los `.gitkeep` son archivos vacíos para versionar carpetas vacías.
No se arrastran `utils.py`, la configuración Doxygen ni los scripts del informe
anterior, porque no son necesarios para iniciar este trabajo.

## Datos, resultados y entrega

Los CSV de UNSW-NB15 van en `data/raw/unsw_nb15/` y los derivados en
`data/processed/`; su contenido queda fuera de Git. Se usan los dos CSV
particionados oficiales (unas 257 000 filas), según el contrato de datos de
`JOURNAL.md`. En T3 (P3) se descargan y se documentan su fuente, conteos y
carga dentro del notebook. Los datos de R² se generan con scikit-learn, como
autorizó el docente (D4 de `JOURNAL.md`).

Las exportaciones finales del notebook irán en `results/figures/` y
`results/tables/`, con nombres descriptivos. Los resultados transitorios pueden
guardarse en `results/raw/`, excluido de Git. Las respuestas y el análisis se
mantienen en el notebook.

`docs/report/` recibe el informe LaTeX de T9 y `submission/` el ZIP de entrega
(fuentes LaTeX, PDF y notebook).

## Entorno

Python **3.15.0** (`.python-version`) con las versiones exactas de
`requirements.txt`. Si ya existe un `.venv` con otra versión de Python,
borrarlo y crearlo de nuevo.

Desde la raíz, en Linux, macOS o WSL:

```sh
python3.15 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
```

Desde PowerShell en Windows (con el administrador de instalaciones de Python,
`py install 3.15`, o el instalador de python.org):

```powershell
py -3.15 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Abrir el proyecto en PyCharm, elegir el intérprete del `.venv` y ejecutar la
celda `s0-config`: imprime las versiones del entorno. Antes del primer commit,
configurar nbdime según [CONTRIBUTING.md](CONTRIBUTING.md).

El informe (T9) necesita una distribución de LaTeX con `latexmk` y el soporte
de español de `babel`: MacTeX en macOS, TeX Live en Linux.
