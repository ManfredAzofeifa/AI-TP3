# TP3 — Redes neuronales

Base del Trabajo Práctico 3 de Principios de Inteligencia Artificial, para un
equipo de tres personas. **Estado: estructura preparada; solución pendiente.**

La organización parte de
[AI-TP1](https://github.com/AleQuesada2012/AI-TP1/tree/74153d802c817c0401d39cf5a9684aad1c85c354),
adaptada al nuevo enunciado. No se copiaron implementaciones, experimentos,
resultados, informes ni documentación generada de ese proyecto.

El enunciado está en
[docs/assignment/TP_3_redes_neuronales.pdf](docs/assignment/TP_3_redes_neuronales.pdf).
Indica entrega el **domingo 29 de noviembre de 2026**; no especifica hora.

## Por dónde comenzar

1. Leer [JOURNAL.md](JOURNAL.md): reparto, secuencia, pendientes y dudas del PDF.
2. Asignar los nombres a P1, P2 y P3 y acordar el primer turno.
3. Seguir [CONTRIBUTING.md](CONTRIBUTING.md) para compartir los cambios.

[AGENTS.md](AGENTS.md) indica a los asistentes que deben revisar el journal
antes de trabajar y actualizarlo al terminar.

## Una sola solución

El archivo [notebooks/tp3_redes_neuronales.ipynb](notebooks/tp3_redes_neuronales.ipynb)
es el único notebook del proyecto y se entrega inicialmente vacío. `.ipynb`
es la extensión estándar de los notebooks de Jupyter.

Allí se escribirán todas las respuestas, implementaciones, pruebas unitarias,
gráficas, tablas, referencias y conclusiones. No habrá soluciones en módulos
Python auxiliares ni notebooks individuales por integrante.

El PDF pide también fuentes LaTeX/LyX, un PDF y un ZIP para TEC Digital. Esa
diferencia de formato queda registrada en el journal para confirmar la entrega;
por ahora se respeta el trabajo en un único notebook y no se genera otro informe.

## Estructura

```text
AI-TP3/
├── .github/pull_request_template.md  # Plantilla opcional y breve
├── AGENTS.md                        # Instrucciones para asistentes
├── CONTRIBUTING.md                  # Flujo sencillo por turnos
├── JOURNAL.md                       # Plan, responsables y pendientes
├── README.md
├── requirements.txt                 # Dependencias iniciales por validar
├── data/
│   ├── raw/.gitkeep                 # Datos originales locales
│   └── processed/.gitkeep           # Datos preparados locales
├── docs/
│   ├── assignment/TP_3_redes_neuronales.pdf
│   └── report/sections/.gitkeep      # Reserva de formato de entrega
├── notebooks/
│   └── tp3_redes_neuronales.ipynb    # Vacío, sin código ni resultados
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

Los archivos originales de UNSW-NB15 irán en `data/raw/` y los derivados en
`data/processed/`; su contenido queda fuera de Git. Todavía no se ha seleccionado
ni descargado el dataset. En T3 se documentarán su fuente, versión, archivos,
etiquetas y carga desde la raíz dentro del notebook. El generador de datos de
R² está pendiente de obtener, según D4 de `JOURNAL.md`.

Las exportaciones finales del notebook irán en `results/figures/` y
`results/tables/`, con nombres descriptivos. Los resultados transitorios pueden
guardarse en `results/raw/`, excluido de Git. Las respuestas y el análisis se
mantienen en el notebook.

`docs/report/` y `submission/` quedan como reservas para el formato de entrega.
Antes de preparar archivos finales para TEC Digital, resolver D1 del journal.

## Entorno inicial

El equipo debe acordar una versión de Python y validar las dependencias antes
de implementar. `requirements.txt` es una base sin versiones fijadas; no afirma
que ya se haya probado el entorno de los experimentos.

Desde la raíz, en Linux/macOS:

```sh
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python -m jupyter lab
```

Desde PowerShell en Windows:

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m jupyter lab
```

Abrir el notebook y usar el kernel del entorno.
