# Journal y pendientes del TP3

Estado al **23 de noviembre de 2026**: T0 (acuerdos, contratos, entorno fijado
y configuración común), T1a (clase `Multilayer_perceptron` de §1) y T1b (XOR de
§2) integradas en `main`; fase 1 en curso. En `main` están además la investigación de §3.2 b y el
ECE de §4.3. T3 (preparación de datos UNSW-NB15, P3) está integrada en `main` (2026-11-25):
los dos CSV de UNSW-NB15 están versionados en `data/raw/unsw_nb15/`. T2a y T2b (§3, P2) están
integradas en `main` (2026-11-26).
Fecha indicada por el enunciado: **domingo 29 de noviembre de 2026**, sin hora.

Este archivo es la fuente del estado de trabajo. Leerlo antes de empezar una
tarea y actualizarlo al integrarla en `main`. `[x]` significa terminado y
verificado; `[ ]` significa pendiente.

## Equipo

| Etiqueta | Nombre | Secciones del notebook a su cargo |
| --- | --- | --- |
| P1 | Alejandro Quesada | §1 red base, §2 XOR y §4.1 clasificador UNSW-NB15 con L2 |
| P2 | Jose Herrera | §3 clasificador en R² y §4.3 ECE |
| P3 | Manfred Azofeifa | Preparación de datos UNSW-NB15, §4.2 ensamble y §4.4 evaluación |

El reparto suma aproximadamente **30 puntos detallados por persona**: P1
asume §1 + §2 + §4.1; P2 asume §3 + §4.3; P3 asume §4.2 + §4.4. P3 asume
además la carga y el preprocesamiento de UNSW-NB15, que necesita para §4.2
y §4.4, para descargar a P1, que está en el camino crítico por la red base.
El encabezado de §4 anuncia 60 puntos, pero sus incisos suman 50; ver D7.

## Trabajo en curso

| Persona | Tarea | Rama | Estado |
| --- | --- | --- | --- |
| P1 | T4 (siguiente) | — | T1a y T1b integradas en `main` el 2026-11-23. T3 integrada el 2026-11-25: T4 desbloqueada. Los CSV llegan con el pull (`data/raw/unsw_nb15/`); revisar D9 |
| P2 | Revisiones (T5 y T7) | — | D10 aceptada por P1 y P3 y su revisión integrada en `main` el 2026-11-26. T2a y T2b integradas en `main` el 2026-11-26 (§3 completa; los números del análisis se revisan en T8). Entorno fijado, nbdime y PyCharm (ciclo *Clear All Outputs* incluido) comprobados en Linux x86_64. Entorno fijado y nbdime comprobados en Windows 11 el 2026-11-26: SciPy ya no está bloqueado y el notebook completo se ejecuta sin errores |
| P3 | T5 (siguiente) | — | T3 integrada en `main` el 2026-11-25 (desbloquea T4). Entorno fijado, nbdime y PyCharm configurados en Linux (Steam Deck). Sigue T5 |

- **Siguiente acción:** §3 (T2a y T2b) y la revisión de D10 ya están en `main`; D10 está aceptada. P2 ya
  comprobó el entorno fijado en Linux (con PyCharm) y en Windows, donde SciPy ya carga
  (casilla de T0). T3 ya está en `main`, así que P1 puede hacer T4: los dos CSV
  llegan con el pull, en `data/raw/unsw_nb15/`; revisar D9 (duplicados). **Ojo:** `main` se
  reescribió el 2026-11-25 (ver registro); quien haya hecho pull antes debe ejecutar
  `git fetch origin` y `git reset --hard origin/main` (sin cambios locales pendientes). Siguen abiertas T4 (P1) y
  T5 (P3); T1b, T2a y T2b ya están en `main`.
- **Integración a `main`:** libre. Solo una persona integra a la vez y lo
  avisa al equipo antes de empezar (ver `CONTRIBUTING.md`).

## Organización en paralelo

Cada persona desarrolla en su propia rama y edita **solo las celdas de sus
secciones** del notebook único. La secuencia se aplica a la integración en
`main`, no al desarrollo. Las únicas esperas son las dependencias reales del
enunciado:

- §3.2 necesita la red de §1 para **ejecutar** los experimentos; el código
  del experimento puede escribirse antes contra el contrato acordado en T0.
- §4.1 necesita la red de §1 y la preparación de datos de UNSW-NB15.
- §4.4 necesita el ensamble (§4.2), el ECE (§4.3) y la preparación de datos.
  La decisión sobre L2 de §4.1 entra como parámetro de la configuración común.
- El ensamble de §4.2 usa modelos de mínimos cuadrados, no la red de §1, y
  el ECE de §4.3 es una función de `(X, y, uncertainties)`: ambos se
  desarrollan y prueban desde el inicio.

| Fase | Tarea | Responsable | Depende de | Revisión sugerida |
| --- | --- | --- | --- | --- |
| 0 | T0: acuerdos, contratos, herramientas y esqueleto | Los tres; P1 coordina | — | Los tres |
| 1 | T1a: clase `Multilayer_perceptron` y sus pruebas (§1) | P1 | T0 | P2 |
| 1 | T1b: XOR (§2) | P1 | T1a | P2 |
| 1 | T2a: datos R² y código del experimento (§3) | P2 | T0 | P3 |
| 1 | T3: preparación de datos UNSW-NB15 | P3 | T0 | P1 |
| 1 | T5: ensamble e incertidumbre (§4.2) | P3 | T0 y material de apoyo (D4) | P2 |
| 1 | T6: ECE y sus pruebas (§4.3) | P2 | T0 y definición de ECE (D6) | P3 |
| 2 | T2b: ejecución y análisis R² (§3) | P2 | T1a y T2a | P1 |
| 2 | T4: clasificador UNSW-NB15 y L2 (§4.1) | P1 | T1a y T3 | P3 |
| 2 | T7: evaluación de ensambles (§4.4) | P3 | T3, T5 y T6; L2 de T4 | P2 |
| 3 | T8: ejecución final del notebook | P1 integra; revisan los tres | T1b, T2b, T4 y T7 | Los tres |
| 4 | T9: informe LaTeX y entrega | Los tres, cada quien sus secciones; P1 integra | T8 | Los tres |

```text
Fase 0   T0 (los tres)
Fase 1   T1a (P1) · T2a (P2) · T6 (P2) · T3 (P3) · T5 (P3)   ← en paralelo
         T1b (P1) ◄── T1a
Fase 2   T2b (P2) ◄── T1a + T2a
         T4  (P1) ◄── T1a + T3
         T7  (P3) ◄── T3 + T5 + T6 (y decisión L2 de T4)
Fase 3   T8 (los tres) ◄── T1b + T2b + T4 + T7
Fase 4   T9 (los tres) ◄── T8
```

T1 se dividió en T1a y T1b para que la clase de la red llegue antes a `main`:
T2b y T4 solo necesitan T1a.

**Calendario objetivo** (propuesto por P1 en T0; cada persona lo confirma al
revisar T0):

| Fecha | Hito |
| --- | --- |
| 2026-11-23 | T0 revisado e integrado |
| 2026-11-24 | T1a, T3, T2a y T5 integrados |
| 2026-11-26 | T1b, T2b, T4 y T7 integrados |
| 2026-11-27 | T8: ejecución final del notebook |
| 2026-11-27 a 2026-11-29 | T9: informe, revisión y entrega por TEC Digital |

Quien esté esperando una dependencia puede avanzar sus otras tareas de la
fase 1, revisar la rama de otra persona o investigar referencias.

## Secciones del notebook y responsables

El esqueleto de `notebooks/tp3_redes_neuronales.ipynb` tiene un encabezado
por sección. Cada persona agrega celdas solo debajo de los encabezados a su
cargo y no mueve ni edita celdas ajenas sin acordarlo.

| Sección del notebook | Responsable |
| --- | --- |
| 0. Configuración común | Definida en T0; los cambios posteriores se registran aquí y se avisan al equipo |
| 1. Perceptrón de tres capas | P1 |
| 2. Clasificación de XOR | P1 |
| 3. Clasificador de datos en R² | P2 |
| 4. Preparación de datos UNSW-NB15 | P3 |
| 4.1 Clasificador UNSW-NB15 y normalización L2 | P1 |
| 4.2 Ensamble e incertidumbre | P3 |
| 4.3 Expected calibration error | P2 |
| 4.4 Evaluación de ensambles | P3 |

## Contratos entre secciones (acordados en T0)

Acordados el 2026-11-23 y vigentes desde la integración de T0. Cambiarlos exige
registrar el nuevo acuerdo aquí y avisar a quien dependa de ellos.

### Red (§1 → §3 y §4.1)

- **Constructor:** `Multilayer_perceptron(neurons_per_layer, alpha,
  max_weights, gamma=0.0, seed=None)`. Conserva el orden de la firma impresa
  y agrega `gamma`, que la lista de argumentos sí pide (D2), con un valor por
  omisión para que la llamada de tres argumentos siga funcionando. `seed`
  inicializa el generador propio de la instancia.
- **Formas:** `X` es n × D (una observación por fila, como en `sklearn`).
  `T` es n × K con valores 0/1: one-hot si K ≥ 2 y una columna con 1 = clase
  positiva si K = 1.
- **Pesos:** representación matricial del curso, `W_o` de (D+1) × M y `W_s`
  de (M+1) × K, con el sesgo en la fila 0 (x₀ = 1 y y₀ᵒ = 1).
- **`max_weights`:** inicialización uniforme en [−max_weights, max_weights] y
  recorte a ese intervalo después de cada actualización.
- **Activaciones:** tangente hiperbólica en la capa oculta y softmax en la de
  salida. Con K = 1 la salida es la primera componente de softmax([p, 0]),
  que equivale a sigmoide(p) (D3).
- **`forward(X)`:** devuelve la salida n × K y guarda como atributos los pesos
  netos y las salidas de cada capa.
- **Optimización (D5): AdaGrad con momentum, en lote completo.** Para cada
  matriz de pesos, con gradiente g: G ← G + g ⊙ g; paso = α · g / (√G + ε);
  v ← γ · v + paso; W ← W − v; luego el recorte por `max_weights`. Con γ = 0
  queda AdaGrad puro. G y v se conservan entre llamadas a `train_mlp`; una
  instancia nueva los reinicia. ε = 10⁻⁸ (acordado en T1a).
- **Deltas (T1a):** `backpropagate_deltas` calcula el gradiente exacto de
  `get_error` (factor 2/(n·K), sin ½) con el jacobiano de la softmax; con K = 1
  se reduce al delta de la sigmoide. La derivación está en `s1-derivacion`.
  Deja en la instancia `delta_o`, `delta_s`, `grad_W_o` y `grad_W_s`.
- **`train_mlp(num_epochs, X, T, alpha, gamma, X_val=None, T_val=None)`:**
  `alpha` y `gamma` reemplazan los valores guardados. Devuelve
  `{"train_error": [...], "val_error": [...]}`, con un valor por época medido
  después de la actualización de esa época; `val_error` queda vacía si no se
  pasan datos de validación. Así §3 obtiene la curva de validación que pide.
- **`get_error(X, T)`:** MSE promediado sobre n · K, es decir, la media de
  (y − t)² sobre todas las observaciones y salidas.
- **`predict(X)`:** etiquetas enteras de forma (n,): argmax si K ≥ 2 y umbral
  0.5 si K = 1 (y ≥ 0.5 → 1).
- **Validación (T1a):** `T` debe tener exactamente la forma n × K; con K = 1 se
  pasa `y.reshape(-1, 1)`, no un vector (n,). Una forma distinta, valores que no
  son 0/1 o filas que no son one-hot (K ≥ 2) dan `ValueError`.

### Datos UNSW-NB15 (preparación → §4.1, §4.2 y §4.4)

- **Fuente:** los dos CSV particionados oficiales,
  `UNSW_NB15_training-set.csv` y `UNSW_NB15_testing-set.csv` (unas 257 000
  filas en total), unidos y vueltos a particionar como pide el enunciado. No
  se usan los cuatro CSV crudos de unos 2.5 millones de filas. Van en
  `data/raw/unsw_nb15/`. T3 registra la URL, los conteos reales y una suma de
  verificación de cada archivo.
- **Etiqueta y atributos:** `label` (1 = ataque) es la clase. Se excluyen de
  los atributos `id`, `label` y `attack_cat`, que revelan la etiqueta. El
  resto son los atributos; T3 confirma la lista con los datos.
- **Preprocesamiento (orden fijo):** partición → one-hot de `proto`, `service`
  y `state` → log1p de las columnas numéricas no negativas → z-score de las
  numéricas → normalización L2 opcional. El one-hot y el z-score se ajustan
  solo con entrenamiento; las categorías que solo aparecen en prueba se
  ignoran. Las columnas one-hot quedan en 0/1, sin log1p ni z-score. Una
  desviación estándar 0 se reemplaza por 1. Si una columna numérica tiene
  valores negativos, T3 lo documenta y no le aplica log1p.
- **Normalización L2 (D8):** por fila. Cada observación completa (numéricas y
  one-hot) se divide entre su norma euclídea. Es el último paso y no aprende
  nada de los datos, por lo que no filtra información de prueba.
- **Funciones:** `load_unsw_nb15(data_dir)` devuelve un `DataFrame`;
  `split_unsw(df, test_size, seed)` devuelve entrenamiento y prueba;
  `preprocess_unsw(train_df, test_df, l2)` devuelve `X_train`, `X_test`
  (float64, n × D) y `y_train`, `y_test` (enteros 0/1, forma (n,)). Las 30
  particiones 80/20 de §4.1 y las 10 particiones 70/30 de §4.4 usan semillas
  derivadas de `SEEDS["s4_datos"]` que T3 registra. T3 documenta si estratifica
  por `label`.
- **Resuelto en T3 (2026-11-25):**
  - Archivos: `UNSW_NB15_training-set.csv`, con 175 341 filas y SHA-256
    `bec7dd5ec88dc2a0ccc7a07879d338395ed7421750f675fd0339e07dfe0648fa`, y
    `UNSW_NB15_testing-set.csv`, con 82 332 filas y SHA-256
    `734fe6642edf758f7c94d7d9149426b49d202fe8e7bf0bef47392489c3c0a559`; en total, 257 673 filas.
    Están versionados en `data/raw/unsw_nb15/` (acuerdo del 2026-11-25). Se obtuvieron a mano desde
    la carpeta de SharePoint que enlaza <https://research.unsw.edu.au/projects/unsw-nb15-dataset>
    (no se pueden bajar con `curl`); los pasos para volver a obtenerlos están en «Origen de los datos»
    (§4 del notebook). `s4-datos-carga` comprueba las sumas.
  - Atributos: 42, de los cuales 39 son numéricos y 3 categóricos (`proto` 133, `service` 13 y
    `state` 11 valores). Ninguna numérica tiene negativos, así que log1p se aplica a las 39. No hay
    faltantes. Clase: 164 673 ataques (63.9 %) y 93 000 normales. `X` lleva primero las numéricas
    en el orden del CSV y luego el one-hot por orden alfabético de categoría; D = 195 en la
    partición 80/20 de semilla 4000 (depende de las categorías presentes en entrenamiento).
  - Particiones **estratificadas por `label`** (`train_test_split`). Semillas:
    `S4_SEMILLAS_80_20` = 4000–4029 (`SEEDS["s4_datos"] + i`) y `S4_SEMILLAS_70_30` = 4500–4509
    (`SEEDS["s4_datos"] + 500 + i`).
  - One-hot y z-score implementados con pandas/NumPy, sin transformadores de scikit-learn.
  - `load_unsw_nb15` agrega el parámetro opcional `drop_duplicates=False` (D9), compatible con la
    firma acordada. El `DataFrame` cargado queda en `s4_unsw` y las demás secciones lo reutilizan
    sin modificarlo.
  - Para la red de §1 con K = 1, se pasa `T = y_train.reshape(-1, 1)`.

### Comparación con y sin L2 (§4.1, T4)

- Ambos tratamientos usan el mismo preprocesamiento base; la única diferencia
  es el paso L2.
- **Corridas emparejadas:** la corrida i de los dos tratamientos usa la misma
  partición 80/20 y los mismos pesos iniciales.
- **Calibración por tratamiento:** cada tratamiento calibra sus
  hiperparámetros con el mismo presupuesto de búsqueda, sobre una validación
  separada del entrenamiento. El 20 % de prueba no se usa para calibrar.
- **Métricas:** F1 de la clase ataque como métrica principal y tasa de
  aciertos como complemento, en las 30 corridas.
- **Prueba:** Wilcoxon de rangos con signo sobre las 30 diferencias
  emparejadas, como prueba principal, con α = 0.05. Se reporta además la
  prueba t pareada como complemento.
- **Regla de decisión, fijada antes de ver resultados:** se usa L2 solo si es
  significativamente mejor en F1. Si no hay diferencia significativa, se usa
  la opción más simple, sin L2.
- **Alcance:** la decisión se guarda en `USE_L2` y se aplica también a los
  ensambles de §4.2 y §4.4.

### Ensamble → ECE (§4.2 → §4.3 y §4.4)

Propuesta de P2 (D6), aceptada por P3 el 2026-11-23: el ECE recibe `X`, `y`,
`uncertainties` (varianza por observación, forma (n,)) y `predictions`
(etiquetas predichas con los puntajes previos a la activación, forma (n,)).
`run_ensemble_uq` y `quantify_uncertainty_ensemble` devuelven esa varianza por
observación; T5 documenta las formas exactas.

### Configuración común (sección 0)

La celda `s0-config` define `PROJECT_ROOT` (se busca hacia arriba desde el
directorio de trabajo, por lo que el kernel puede arrancar en la raíz o en
`notebooks/`), las rutas `DATA_RAW_DIR`, `DATA_PROCESSED_DIR`, `UNSW_DIR`,
`RESULTS_FIGURES_DIR` y `RESULTS_TABLES_DIR`, una semilla por sección en
`SEEDS`, el modo reducido `QUICK` (variable de entorno `TP3_QUICK=1`) con
`quick_or_full(reducido, completo)` y `USE_L2 = None` hasta T4. También imprime
las versiones del entorno. Cada sección ejecuta solo sus propias pruebas con un
`unittest.TestSuite` explícito, como §4.3, con nombres de clases que no se
repiten entre secciones.

## Reglas de congruencia de las salidas

- Durante el desarrollo, el notebook se versiona **sin salidas**: antes de
  cada commit, *Clear All Outputs* en PyCharm, guardar y revisar `git diff`
  (ver `CONTRIBUTING.md`). Cada quien ejecuta localmente para verificar.
- Cada sección crea su propio generador aleatorio a partir de su semilla de la
  configuración común, para que sus resultados no dependan de lo que se
  ejecutó antes en el notebook.
- No reutilizar variables globales genéricas entre secciones (`X`, `T`,
  `model`): usar nombres con prefijo de sección o encapsular en funciones.
- Las salidas que se entregan salen de **una única ejecución completa** desde
  un kernel limpio en T8. El análisis que cite números se escribe o revisa
  después de esa ejecución.

## Pendientes por tarea

### T0 — Acuerdos iniciales (los tres; P1 coordina)

- [x] Registrar los nombres del equipo (tabla «Equipo»).
- [x] Acordar Python y fijar `requirements.txt`: Python 3.15.0
  (`.python-version`) y versiones exactas del entorno de P1, con PyYAML 6.0.4.
  Comprobado: el entorno de P1 coincide con el archivo y las dependencias se
  resuelven con ruedas para Python 3.15 en Linux x64, Windows x64 y macOS
  arm64.
- [x] Después de integrar T0, P2 (Linux y Windows) y P3 (Linux): instalar
  Python 3.15.0 y `requirements.txt` en un entorno nuevo, y ejecutar
  `s0-config` y §4.3. En
  Windows, comprobar si el Control de aplicaciones sigue bloqueando SciPy; si
  ocurre, ejecutar en Linux las secciones que usan SciPy o `sklearn`.
  Hecho en Linux por P3 (2026-11-25) y por P2 (2026-11-26, también en
  PyCharm), y en Windows 11 por P2 (2026-11-26): SciPy y scikit-learn cargan
  y el notebook completo se ejecuta sin errores; en Windows no se probó PyCharm.
- [x] Retirar nbstripout: renumeraba los identificadores de celda y
  reformateaba todo el archivo. Las salidas se limpian con *Clear All Outputs*
  de PyCharm. Se versionan en `.gitattributes` las líneas de nbdime.
- [ ] Configurar nbdime en cada clon (`nbdime config-git --enable`). Hecho
  por P3 (Linux) y por P2 (Linux y Windows); falta registrar el de P1.
- [x] Comprobar el ciclo en PyCharm (macOS): ejecutar, *Clear All Outputs* y
  guardar quita salidas, contadores y `ExecuteTime`, y no cambia `kernelspec`.
  Lo único distinto era el orden de claves de las celdas de código; se guardó
  el notebook en el formato de PyCharm y el ciclo repetido deja el diff vacío.
  Instrucciones del kernel del `.venv` en `CONTRIBUTING.md`.
- [x] Resolver D2, D3 y D5, que afectan el contrato de la red.
- [x] Resolver D4: los datos de R² se generan con scikit-learn, con
  autorización del docente. El material de apoyo ya está en `docs/assignment/`.
- [x] Acordar y registrar los contratos entre secciones. P3 aceptó el
  contrato ensamble → ECE, incluido `predictions`.
- [x] Crear la configuración común (celda `s0-config`).
- [x] Integrar T0 en `main` antes de abrir las ramas de la fase 1
  (2026-11-23).

### T1a — P1: clase `Multilayer_perceptron` y sus pruebas (fase 1)

- [x] Implementar `Multilayer_perceptron` y su constructor según el
  contrato, con la representación matricial de pesos (D2).
- [x] Implementar `forward(X)` con tangente hiperbólica y softmax; con K = 1,
  softmax([p, 0]) (D3).
- [x] Implementar `backpropagate_deltas(X, T)` y `update_weights(X, T)`. El
  material deriva los deltas con sigmoide; con softmax y MSE, el delta de
  salida usa el jacobiano de la softmax. Documentar la derivación
  (`s1-derivacion`).
- [x] Implementar `train_mlp` con AdaGrad y momentum según el contrato (D5),
  y explicar qué cambia respecto de la retropropagación vista en clase.
- [x] Implementar `get_error(X, T)` con MSE y registrar el error por época.
- [x] Documentar qué hace cada función y ejecutar al menos dos pruebas por
  función para cubrir la regla general del PDF: 20 pruebas, de dos a cuatro
  por función, incluida una comprobación del gradiente con diferencias
  centrales para K = 3 y K = 1 (`s1-pruebas`).
- [ ] Captura de la prueba de entrenamiento como adjunto de la celda Markdown
  `s1-captura-entrenamiento`: se toma en T8, con el código entregado
  (acordado en T1a).
- [x] Integrar en `main` (2026-11-23): desbloquea T2b y T4.
- [ ] Avisar a P2 y P3 de que T1a está en `main`.
- [x] Revisión de P2 (2026-11-26): sin errores; ver el registro de trabajo.
- [ ] P1: decidir sobre el recorte con momentum (revisión de P2): un peso recortado
  sigue acumulando `v` y puede quedar varias épocas en el límite. Documentarlo en
  `s1-derivacion` o, con acuerdo registrado (cambia §2 y §3), anular `v` en los pesos recortados.

### T1b — P1: XOR (fase 1, requiere T1a)

- [x] Revisión de P2 (2026-11-26): sin errores; resultados idénticos en Linux x86_64.
- [ ] P1: respaldar en el notebook o quitar la frase de `s2-planteamiento` según la cual
  K = 2 converge con más semillas que K = 1 (revisión de P2).
- [x] Resolver XOR: cuatro entradas booleanas y etiquetas, arquitectura y
  diagrama, calibración y curvas para los hiperparámetros probados
  (`s2-calibracion`, `s2-curvas`, `s2-diagrama`): 36 configuraciones × 20
  semillas × 2000 épocas.
- [x] Reportar predicciones de las cuatro entradas, criterio de error cero y
  número de iteraciones de convergencia; distinguir clasificación y MSE (D5)
  (`s2-convergencia`).
- [ ] Redactar en T8 el análisis con números (`s2-analisis`), con la
  ejecución final.
- [x] Integrar en `main`.

### T2a — P2: datos R² y código del experimento (fase 1)

- [x] Generar los datos con `sklearn.datasets` (D4); documentar las funciones,
  sus parámetros y la semilla de la sección: `make_blobs` (separable) y
  `make_moons` (no separable), 300 muestras, `SEEDS["s3_r2"]` (`s3-planteamiento`).
- [x] Generar y graficar un conjunto linealmente separable y otro no separable;
  la separabilidad se comprueba con un programa lineal (`s3-datos`).
- [x] Preparar la partición 80 % entrenamiento / 20 % validación de `sklearn`
  (estratificada, `random_state=SEEDS["s3_r2"]`).
- [x] Escribir, contra el contrato de la red, el código de las cuatro
  configuraciones (D = 2, K según D3, α = 0.01, M ∈ {20, 2}, γ ∈ {0, un valor
  no nulo documentado}) en ambos escenarios con P = 50 iteraciones, y el de
  las curvas, la tabla de gráficas y la tabla de errores finales (D10; siete
  funciones `s3_*` con 15 pruebas en `s3-pruebas`).
- [x] Investigar la relación entre neuronas ocultas y de entrada, y reunir
  los artículos científicos que se citarán. Redactado en la celda
  `s3-investigacion-neuronas` con seis referencias cuyos datos se verificaron
  en línea; las preguntas que dependen de resultados quedan para T2b.
- [x] Integrar en `main` (2026-11-26, junto con T2b).

### T2b — P2: ejecución y análisis R² (fase 2, requiere T1a)

- [x] Ejecutar las ocho combinaciones con particiones comparables: misma partición
  por escenario y las mismas 20 semillas de pesos iniciales (D10) (`s3-experimento`).
- [x] Mostrar curvas de entrenamiento y validación, la tabla de gráficas y
  la tabla de errores finales por configuración y escenario (`s3-curvas`,
  `s3-errores-finales`).
- [x] Analizar α, tamaño de capa oculta y error, citando los artículos dentro del notebook
  (`s3-analisis`). Se agregó un experimento complementario de α con M ∈ {2, 20}
  (`s3-alpha`) y dos referencias verificadas: LeCun et al. 1998 (§4.7, en el PDF y en
  Crossref) y Duchi et al. 2011 (JMLR).
- [x] Ejecutar desde cero e integrar en `main` (2026-11-26).
- [x] Revisar D10 (rama `p2/t2-d10`): sensibilidad de la elección de `max_weights`, inicialización y
  recorte documentados en `s3-experimento-descripcion`, `s3-max-weights`, `s3-max-weights-sensibilidad`
  y `s3-analisis`.
- [x] Integrar la revisión de D10 en `main` (2026-11-26); P1 y P3 aceptaron D10.
- [ ] Revisar en T8 que los números citados en `s3-analisis` coincidan con la ejecución final.

### T3 — P3: preparación de datos UNSW-NB15 (fase 1)

- [x] Descargar los dos CSV particionados oficiales en `data/raw/unsw_nb15/`
  y registrar la URL, los conteos y una suma de verificación de cada archivo
  (contrato de datos, «Resuelto en T3»).
- [x] Confirmar la clase ataque, los atributos y las columnas excluidas
  (`id`, `label`, `attack_cat`) según el contrato de datos. Se encontraron
  duplicados masivos: se registró D9.
- [x] Implementar `load_unsw_nb15`, `split_unsw` y `preprocess_unsw` con el
  orden acordado: one-hot, log1p, z-score ajustado con entrenamiento y L2 por
  fila opcional (`l2`).
- [x] Definir las 30 particiones 80 % / 20 % (§4.1) y las 10 particiones
  70 % / 30 % (§4.4), con semillas derivadas de `SEEDS["s4_datos"]`.
- [x] Documentar y probar las funciones (21 pruebas en `s4-datos-pruebas`).
- [x] Integrar en `main` (2026-11-25): desbloquea T4.
- [ ] Avisar a P1 de que T3 está en `main` (los CSV llegan con el pull; revisar D9).

### T4 — P1: UNSW-NB15 y comparación de normalización L2 (fase 2, requiere T1a y T3)

- [ ] Calibrar los hiperparámetros de cada tratamiento con el mismo
  presupuesto, sobre una validación separada del entrenamiento, y documentar
  el proceso.
- [ ] Comparar con L2 y sin L2 en 30 corridas emparejadas (misma partición y
  mismos pesos iniciales). Reportar F1 de la clase ataque y tasa de aciertos.
- [ ] Aplicar Wilcoxon de rangos con signo (y la prueba t pareada como
  complemento), documentar supuestos y resultados, y decidir con la regla
  acordada si usar L2 en el resto del proyecto.
- [ ] Registrar la decisión en la configuración común, ejecutar desde cero,
  integrar en `main` y avisar a P3.

### T5 — P3: ensamble y cuantificación de incertidumbre (fase 1)

- [ ] Revisar el material de apoyo. El contrato ensamble → ECE ya está
  acordado con P2 (D6).
- [ ] Implementar `train_ensemble` con modelos de mínimos cuadrados de
  clasificación según el enunciado, documentando cómo se construyen sus miembros.
- [ ] Implementar `run_ensemble_uq` para evaluar la varianza de las salidas.
- [ ] Implementar `quantify_uncertainty_ensemble(x, model, N=10)` reutilizando
  el ensamble entrenado; usar puntajes del producto punto antes de la activación.
- [ ] Documentar y ejecutar al menos dos pruebas unitarias de la
  cuantificación, con datos sintéticos si T3 no está integrada; cubrir
  también las funciones auxiliares según la regla general.
- [ ] Ejecutar desde cero e integrar en `main`.

### T6 — P2: expected calibration error (fase 1)

- [x] Resolver con el material de apoyo la definición, entradas, intervalos y
  procedencia de predicciones/puntajes de ECE; registrar el acuerdo D6.
- [x] Implementar `calculate_expected_calibration_error(X, y, uncertainties)`
  según la definición y el contrato acordados, y documentar la relación con
  la última capa. Se agregó el parámetro `predictions` (D6) y las funciones
  auxiliares `uncertainty_to_confidence`, `calibration_bins` y
  `uncertainty_accuracy_correlation`.
- [x] Diseñar, ejecutar y explicar al menos dos pruebas unitarias de ECE con
  datos sintéticos de resultado conocido: 13 pruebas que cubren las cuatro funciones.
- [x] Revisión de P3 del contrato ensamble → ECE: aceptó `predictions` el
  2026-11-23.
- [x] Integrar en `main` y avisar a P3. Integrado el 2026-11-20 antes de la
  revisión de P3; si P3 cambia el contrato, se ajusta en una rama nueva.

### T7 — P3: ECE, costo de ejecución y comparación de ensambles (fase 2)

- [ ] Usar las 10 particiones reproducibles de 70 % / 30 % de T3.
- [ ] Evaluar N ∈ {10, 100, 1000} sobre las mismas particiones comparables:
  30 combinaciones de tamaño y partición. Registrar semillas y protocolo.
- [ ] Medir ECE y tiempo; especificar qué incluye cada tiempo y registrar el entorno.
- [ ] Reportar media y desviación estándar del ECE por N y los tiempos medidos.
- [ ] Aplicar una prueba estadística adecuada para comparar configuraciones,
  documentando la interpretación adoptada ante la frase incompleta de D7.
- [ ] Preparar las gráficas y el comentario; el código puede avanzar antes de
  T4 usando la bandera de L2, pero los resultados finales usan su decisión.
- [ ] Ejecutar desde cero e integrar en `main`.

### T8 — Ejecución final del notebook (P1 integra; revisan los tres)

- [ ] Comprobar que los cuatro apartados del enunciado tienen respuestas,
  pruebas, referencias, tablas y gráficas dentro del notebook único.
- [ ] Confirmar que el entorno coincide con `requirements.txt` y ejecutar
  todo desde un kernel limpio, sin `TP3_QUICK`, con los valores del
  enunciado; registrar máquina, duración, datos, semillas y resultados de
  las pruebas.
- [ ] Hacer commit del notebook **con** las salidas de esa ejecución en
  `main` (es la única vez que se versionan), incluida la evidencia de la
  prueba de entrenamiento, y exportar a `results/` solo las figuras y tablas
  necesarias.
- [ ] Antes de limpiar el kernel para ese commit, tomar en PyCharm el
  pantallazo de la salida de `s1-pruebas` (líneas de `TestMLPTrain`) y
  adjuntarlo a la celda Markdown `s1-captura-entrenamiento` (§1 d.1).
- [ ] Revisar en conjunto que el análisis cite los números de esa ejecución.

### T9 — Informe LaTeX y entrega (los tres; P1 integra)

- [ ] Redactar el informe en LaTeX en `docs/report/` cuando el notebook esté
  terminado (D1). Es un documento escrito, no una exportación del notebook.
  Cada persona redacta las secciones de sus tareas, con los números,
  figuras y tablas de la ejecución de T8.
- [ ] Reunir las referencias en BibTeX, incluidas las de §3.2 b.
- [ ] Compilar el PDF y revisarlo entre los tres.
- [ ] Preparar en `submission/` el ZIP con las fuentes LaTeX, el PDF y el
  notebook, con instrucciones de reproducción y sin datos innecesarios.
- [ ] Verificar el paquete final antes de entregarlo por TEC Digital.

## Dudas del enunciado y materiales faltantes

Interpretaciones del enunciado y materiales faltantes. Consultar las páginas
indicadas del PDF; cada fila indica si ya hay acuerdo.

| ID | Página | Afecta | Pendiente o acuerdo |
| --- | --- | --- | --- |
| D1 | 1 | T8, T9 | **Acordado en T0 (2026-11-23).** El PDF pide un ZIP con fuentes LaTeX/LyX, PDF y Jupyter. Toda la solución sigue en el notebook único; cuando esté terminado (T8), se redacta un informe en LaTeX (T9) que no es una exportación del notebook. No se empieza antes. |
| D2 | 1 | T0, T1a, T2a | **Acordado en T0.** La firma impresa `__init__(neurons_per_layer, alpha, max_weights)` omite `gamma`, que la lista de argumentos sí pide. Se usa `__init__(neurons_per_layer, alpha, max_weights, gamma=0.0, seed=None)`, que admite ambas lecturas. |
| D3 | 2–4 | T0, T1a, T2a, T2b | **Acordado en T0.** Se exige softmax de salida y en R² K = 1; una softmax de un componente siempre vale 1, su derivada es 0 y la red no aprende. El docente indicó que una salida igual a 1 con K = 1 es aceptable. Se usa softmax([p, 0]), cuya primera componente es sigmoide(p): sigue siendo una softmax y permite comparar las configuraciones de §3. El notebook explica la elección y menciona la indicación del docente. |
| D4 | 3 y 5 | T2a | **Acordado (2026-11-23).** El docente autorizó generar los datos de R² con scikit-learn en lugar de la función `generar_datos_R2`. T2a elige las funciones de `sklearn.datasets` para el conjunto linealmente separable y el no separable, documenta sus parámetros y usa `SEEDS["s3_r2"]`. El material de apoyo de ensambles y ECE está en `docs/assignment/EstimacionIncertidumbre.pdf` (sección 2: ensamble entrenado sobre N particiones del entrenamiento e incertidumbre como varianza de las predicciones; sección 4: ECE). |
| D5 | 2–3 | T1a, T1b | **Acordado en T0, salvo XOR.** El docente se refiere a AdaGrad con «descenso del gradiente adaptativo». Se implementa AdaGrad con momentum γ (contrato de la red); γ = 0 es AdaGrad puro. Se usan los nombres `get_error` y `train_mlp`, aunque el PDF también dice `evaluar_error` y `entrenar_red`. En T1a (2026-11-23) se acordó ε = 10⁻⁸ y que los deltas sean el gradiente exacto del MSE de `get_error`. En T1b (2026-11-23) se acordó para XOR: K = 2 con softmax y etiquetas one-hot; «error cero» = ninguna de las cuatro entradas mal clasificada, con MSE ≤ 0.01 (el MSE exacto 0 es inalcanzable con softmax y recorte); época de convergencia = primera a partir de la cual eso se cumple hasta la última época; calibración en rejilla con 20 semillas por configuración. |
| D6 | 5 | T5, T6 | **Acordado por P2 el 2026-11-20; aceptado por P3 el 2026-11-23.** Definición del material (§4): ECE = Σ \|B_m\|/N · \|acc(B_m) − s̄(B_m)\|, ignorando cubetas vacías, con puntajes en [0, 1]. El material no fija la conversión de la varianza ni el número de cubetas, y la firma no recibe predicciones. Acuerdos: (1) puntaje s = 1 − varianza normalizada min-max, porque la varianza no está acotada y crece con la falta de confianza; (2) reportar además la correlación de Pearson entre incertidumbre y acierto, alternativa del material; (3) 10 cubetas de igual ancho, configurables; (4) agregar el parámetro `predictions`, con etiquetas obtenidas de la salida de la última capa antes de la activación. |
| D7 | 4–5 | T7 | §4 anuncia 60 puntos pero sus incisos suman 50. La última instrucción estadística termina en “verifique si existe” sin completar la hipótesis. Confirmar alcance; el plan conserva todos los incisos visibles. |
| D8 | 4–5 | T3, T4, T5, T7 | **Acordado en T0.** «Normalización L2» no está definida y los atributos crudos de UNSW-NB15 van de 0/1 hasta unos 10⁹: sin escalar, la tangente hiperbólica se satura, y una L2 sobre datos crudos borraría casi todos los atributos. Se interpreta como L2 por fila sobre un preprocesamiento base común (one-hot, log1p y z-score); ver el contrato de datos y el protocolo de comparación. |
| D9 | 4–5 | T3, T4, T5, T7 | **Acordado por P3 en T3 (2026-11-25); P1 y P2 pueden revisarlo.** En los dos CSV unidos, 103 575 filas (40.2 %) repiten exactamente los atributos y la etiqueta de otra (96 297 son ataques, sobre todo *Generic*), y 414 grupos de atributos idénticos tienen etiquetas distintas. Con las particiones de T3, el 45.2 % de las filas de prueba (media de las 30 particiones 80/20; 44.5 % en las 10 de 70/30) tienen una copia exacta de sus atributos en entrenamiento, así que la tasa de aciertos, el F1 y el ECE resultan optimistas. Se **conservan todas las filas**, como fija el contrato y como pide el enunciado («datos provistos»). La superposición se mide y documenta en el notebook (`s4-datos-carga`), y T4 y T7 la mencionan como limitación al analizar. `load_unsw_nb15(..., drop_duplicates=True)` permite repetir el análisis sin duplicados (154 098 filas, 44.4 % ataques). |
| D10 | 3–4 | T2a, T2b | **Propuesto por P2 en T2a (2026-11-26); aceptado por P1 y P3 (2026-11-26).** Para §3.2: (1) γ ≠ 0 «a conveniencia» = 0.9, el mismo valor probado en §2; (2) P = 50 iteraciones = 50 épocas en lote completo sobre el 80 % de entrenamiento («todo el conjunto de muestras» se lee como lote completo), con el MSE de validación (20 %) registrado en cada época; (3) «error final de convergencia» = MSE de la época 50, aunque la red no haya convergido; (4) `max_weights`, que el enunciado no fija, se elige entre {0.5, 1, 2, 5} con el MSE final de **entrenamiento** (menor media de las medianas de las 8 combinaciones), sin usar validación; (5) cada combinación se repite con 20 semillas de pesos iniciales derivadas de `SEEDS["s3_r2"]`, las mismas en las 8 combinaciones y con la misma partición, y se reportan mediana, rango intercuartílico, media y desviación estándar. **Revisión de P2 (2026-11-26, rama `p2/t2-d10`):** el criterio de (4) se mantiene, pero elige 1 por poco (media 0.102 frente a 0.115 con 0.5 y 0.116 con 2) y otros criterios razonables no coinciden: la media de los log₁₀ elige 2 y el rango medio, 1. Con los cuatro valores, M = 20 termina con menos error que M = 2 y γ = 0.9 con menos que γ = 0 en los cuatro pares; solo cambia el orden entre b) y c). Se documentan en §3 esa sensibilidad (celda `s3-max-weights-sensibilidad`, sin entrenamientos nuevos), que `max_weights` también fija la escala de la inicialización, que la variabilidad entre semillas refleja solo los pesos iniciales y que el recorte acota la salida (|aˢ| ≤ (M + 1)·`max_weights`; con M = 2 y `max_weights` = 1, el MSE no baja de 2.2·10⁻³, un piso que no se alcanza en la época 50). |

## Acuerdos vigentes

- La solución se escribe solo en `notebooks/tp3_redes_neuronales.ipynb`.
- Desarrollo en paralelo: una rama por tarea, cada persona edita solo sus
  secciones del notebook y la integración en `main` es de una en una.
- El notebook se versiona sin salidas (*Clear All Outputs* en PyCharm antes de
  cada commit) hasta la ejecución final de T8. No se usa nbstripout.
- El equipo trabaja con PyCharm y con el kernel del `.venv` del proyecto.
- Entorno: Python 3.15.0 y las versiones exactas de `requirements.txt`. P1
  trabaja en macOS y en WSL (Ubuntu, dentro del sistema de archivos de WSL);
  P2 en Linux y a veces en Windows; P3 en Linux.
- Mantener un único `README.md` general en la raíz, sin README por carpeta.
- Los nombres están en la tabla «Equipo»; las etiquetas P1, P2 y P3 se usan
  en las tareas y en los nombres de las ramas.
- Los contratos entre secciones y la configuración común son los acordados en
  T0 (ver arriba). Este journal describe trabajo y acuerdos, no soluciones.
- ECE de §4.3 según D6: confianza 1 − varianza normalizada, Pearson como
  complemento, 10 cubetas configurables y parámetro adicional `predictions`.
- Los datos de R² de §3 se generan con scikit-learn (D4).
- El informe LaTeX se redacta en T9, con el notebook terminado (D1).
- Red de §1 (T1a): AdaGrad con ε = 10⁻⁸; deltas con el gradiente exacto del
  MSE de `get_error`; la captura de la prueba de entrenamiento se toma en T8.
- Datos y resultados en Git (2026-11-25, P3): se versionan `data/` y `results/` para que nadie tenga
  que volver a descargar ni generar lo que otra persona ya tiene; `data/` se trata como binario en
  `.gitattributes` (los CSV de UNSW-NB15 usan CRLF y sus sumas SHA-256 deben conservarse). Se
  retiraron del `.gitignore` las exclusiones de `data/`, `results/raw/` y de artefactos (`*.pkl`, etc.).
- Commits sin líneas de coautoría automáticas (2026-11-25, P3).
- Datos UNSW-NB15 (T3): particiones estratificadas por `label`, semillas 4000–4029 (80/20) y
  4500–4509 (70/30), se conservan los duplicados (D9) y `s4_unsw` se comparte entre secciones.
- XOR de §2 (T1b): K = 2 one-hot; error cero = 0 errores de clasificación y
  MSE ≤ 0.01 sostenidos hasta el final; 36 configuraciones × 20 semillas.
- R² de §3 (T2a y T2b): `make_blobs` y `make_moons` con 300 muestras y separabilidad comprobada
  con un programa lineal; partición 80/20 estratificada; γ ≠ 0 = 0.9; `max_weights` elegido con el
  error de entrenamiento (sensibilidad al criterio documentada en §3); 20 semillas emparejadas (D10, aceptada).

## Registro de trabajo

| Fecha | Responsable | Trabajo y verificación | Siguiente paso |
| --- | --- | --- | --- |
| 2026-11-18 | Preparación del repositorio | Revisados la estructura del TP1 y las cinco páginas del enunciado. Creada la base sin avances. Verificados el formato del notebook único y vacío, la identidad del PDF, los enlaces locales y las exclusiones de Git. Las dependencias de los experimentos siguen pendientes de validar. | T0: asignar nombres, materiales e interpretaciones. |
| 2026-11-18 | Simplificación de documentación | Centralizadas las indicaciones en el README general y retirados los cinco README de subcarpetas. Se conserva la estructura con archivos vacíos. | T0 sigue pendiente. |
| 2026-11-20 | P2 (reorganización) | Reemplazada la secuencia en cascada por un plan en paralelo según las dependencias reales del enunciado. Asignada a P3 la preparación de datos UNSW-NB15. Agregados contratos entre secciones, reglas de congruencia de salidas, flujo por ramas con nbstripout y nbdime, y esqueleto de encabezados en el notebook. No se ejecutó código ni se instalaron las herramientas. | T0: aprobar el reparto entre los tres, instalar herramientas y acordar contratos. |
| 2026-11-20 | P2 (T2a, rama `p2/t2a-r2`) | Redactada la investigación de §3.2 b (neuronas ocultas frente a entradas) con referencias a Hornik et al. 1989, Sartori y Antsaklis 1991, Huang 2003, Barron 1994, Sheela y Deepa 2013 y Stathakis 2009; autores, revista, volumen, páginas y DOI comprobados en fuentes en línea. Solo Markdown; no se ejecutó código. El resto de T2a espera `generar_datos_R2` (D4) y el contrato de la red (T0). | Conseguir el generador y el material de apoyo de ECE; acordar contratos en T0. |
| 2026-11-20 | P2 (T6, rama `p2/t6-ece`) | Agregado el material de apoyo `docs/assignment/EstimacionIncertidumbre.pdf` y registrados los acuerdos de D6. Implementado el ECE de §4.3 con tres funciones auxiliares y 13 pruebas unitarias. Notebook ejecutado desde un kernel limpio con `jupyter nbconvert --execute` (copia fuera del repositorio): 13/13 pruebas correctas. Entorno: Python 3.14.7 y NumPy 2.5.5 en `.venv` local. **Bloqueo:** en esta máquina, el Control de aplicaciones de Windows impide cargar la DLL `_fblas` de SciPy, por lo que no se pueden importar SciPy ni scikit-learn. §4.3 no los usa, pero §3 (partición con `sklearn`) y las pruebas estadísticas de §4.1 y §4.4 sí. | P3 revisa el contrato ensamble → ECE; en T0, comprobar SciPy y scikit-learn en las otras máquinas y buscar una solución para esta. |
| 2026-11-20 | P2 (integración) | Integradas en `main` las ramas `p2/t2a-r2` y `p2/t6-ece`. El único conflicto fue el de las dos filas agregadas al registro; se conservaron ambas. Notebook integrado ejecutado desde un kernel limpio con `jupyter nbconvert --execute` (copia fuera del repositorio): 13/13 pruebas de §4.3 correctas. | P3 revisa el contrato ensamble → ECE; T0 sigue pendiente. |
| 2026-11-23 | P1 (T0, rama `p1/t0-acuerdos`) | Acordados los contratos de la red, los datos UNSW-NB15, la comparación L2 y la configuración común; resueltos D1, D2, D3, D5 (salvo XOR) y D8. Fijados Python 3.15.0 y las versiones exactas de `requirements.txt` (PyYAML 6.0.4, porque 6.0.3 no tiene ruedas para 3.15 en Linux ni Windows); el entorno de P1 coincide y `pip install --dry-run --only-binary=:all:` resuelve las dependencias para Linux x64, Windows x64 y macOS arm64 (no es una instalación real en esas máquinas). Retirado nbstripout; versionadas las líneas de nbdime. Agregada la celda `s0-config` y guardado el notebook en el formato de nbformat (indentación de 1 espacio); el resto de las celdas no cambió. Notebook completo ejecutado desde un kernel limpio en macOS arm64 con `jupyter nbconvert --execute` (salida fuera del repositorio): `s0-config` imprime Python 3.15.0 y las versiones fijadas, y 13/13 pruebas de §4.3 correctas. `s0-config` también se comprobó desde la raíz con `TP3_QUICK=1`. Nota: sin activar el `.venv`, `python -m jupyter nbconvert` puede tomar otro `jupyter-nbconvert` del PATH. No se probó todavía en PyCharm, Linux, Windows ni WSL. | P2 y P3 revisan T0, instalan el entorno y comprueban PyCharm; P1 integra. |
| 2026-11-23 | P1 (T0, rama `p1/t0-acuerdos`) | Registrados los nombres del equipo, D4 (datos de R² con scikit-learn, autorizado por el docente) y la aceptación de P3 del parámetro `predictions` (D6). Comprobado en PyCharm (macOS, intérprete `.venv` 3.15.0, *IDE-Managed Server*): el notebook se ejecuta completo (13/13 pruebas de §4.3) y el ciclo ejecutar, *Clear All Outputs* y guardar deja `git diff` vacío después de guardar el notebook con el orden de claves de PyCharm. Agregadas a `CONTRIBUTING.md` las instrucciones para usar el `.venv` como kernel sin registrar kernels nuevos. No probado en Linux, Windows ni WSL. | P1 integra T0; luego P2 y P3 instalan el entorno fijado. |
| 2026-11-23 | P1 (integración) | Integrada en `main` la rama `p1/t0-acuerdos` (sin conflictos; `main` no había cambiado desde la creación de la rama). Las verificaciones son las de las filas anteriores de T0. | P2 y P3 instalan el entorno fijado; fase 1: T1a, T2a, T3 y T5. |
| 2026-11-23 | P1 (T1a, rama `p1/t1a-mlp`) | Implementada `Multilayer_perceptron` en §1 según el contrato, solo con NumPy: celdas `s1-descripcion`, `s1-derivacion` (propagación, delta con jacobiano de la softmax y MSE, caso K = 1, AdaGrad con momentum y cambios respecto de la retropropagación del curso), `s1-mlp-clase`, `s1-pruebas-descripcion`, `s1-pruebas` y `s1-captura-entrenamiento` (pendiente de T8). Acordados ε = 10⁻⁸, los deltas como gradiente exacto de `get_error` y la captura en T8. 20 pruebas, incluida la comprobación del gradiente con diferencias centrales para K = 3 y K = 1. Para confirmar que las pruebas detectan errores, se introdujeron a propósito ocho errores en el código (jacobiano, derivada de tanh, escala del error, momentum, acumulación de G, recorte, fila del sesgo y umbral): cada uno hizo fallar al menos una prueba. Notebook completo ejecutado desde un kernel limpio en macOS arm64 con `jupyter nbconvert --execute`, sin `TP3_QUICK` (salida fuera del repositorio): 20/20 pruebas de §1 y 13/13 de §4.3 correctas. El diff del notebook solo agrega celdas de §1, sin salidas. No probado en PyCharm, Linux, Windows ni WSL. | P1 integra T1a; P2 (T2b) y P1 (T4) ya pueden usar la red. |
| 2026-11-23 | P1 (integración) | Integrada en `main` la rama `p1/t1a-mlp` (sin conflictos). Las verificaciones son las de la fila anterior. | P1 sigue con T1b. |
| 2026-11-23 | P1 (T1b, rama `p1/t1b-xor`) | Resuelto XOR en §2 con la red de §1: celdas `s2-planteamiento`, `s2-funciones-descripcion`, `s2-funciones` (`s2_entrenar_xor`, `s2_epoca_convergencia`, `s2_dibujar_red`), `s2-pruebas` (8 pruebas), `s2-calibracion` (rejilla de M, `max_weights`, α y γ: 36 configuraciones × 20 semillas derivadas de `SEEDS["s2_xor"]` × 2000 épocas; 5 semillas y 500 épocas con `TP3_QUICK`), `s2-curvas` (mediana y rango intercuartílico del MSE de cada configuración), `s2-arquitectura` y `s2-diagrama`, `s2-convergencia` (corrida representativa, curvas de MSE y de errores de clasificación, predicciones) y `s2-analisis` (pendiente de T8). Acordados con P1 la salida K = 2, el criterio de error cero y la calibración con varias semillas (D5). Notebook completo ejecutado dos veces desde un kernel limpio en macOS arm64 con `jupyter nbconvert --execute`, sin `TP3_QUICK` (unos 100 s; salida fuera del repositorio): 20/20 pruebas de §1, 8/8 de §2 y 13/13 de §4.3; las dos ejecuciones eligieron la misma configuración (M = 4, `max_weights` = 2, α = 0.5, γ = 0; 20/20 semillas convergen, época mediana 38) y clasificaron bien las cuatro entradas. Con `TP3_QUICK=1` también se ejecuta completo. El diff del notebook solo agrega celdas de §2, sin salidas. No probado en PyCharm, Linux, Windows ni WSL. | P1 integra T1b; T4 espera T3. |
| 2026-11-25 | P3 (entorno y T3, rama `p3/t3-datos`) | **Entorno:** Python 3.15.0 instalado con `uv` en Linux (Steam Deck) y `requirements.txt` instalado en un `.venv` nuevo; las versiones coinciden con el archivo y `pip check` sale limpio (solo faltan `appnope` y `pywinpty`, que son de macOS y Windows). `nbdime config-git --enable` hecho y probado con `git diff` del notebook. PyCharm con el intérprete del `.venv` e *IDE-Managed Server*: `s0-config` imprime Python 3.15.0 y las versiones fijadas, y el diff solo mostró la salida de `s0-config` y sus tiempos, con el orden de claves intacto. **T3:** descargados los dos CSV oficiales (conteos y SHA-256 en el contrato de datos) y revisadas columnas, clases, faltantes, negativos, categorías y duplicados (D9). Implementadas en §4 las celdas `s4-datos-fuente`, `s4-datos-funciones-descripcion`, `s4-datos-funciones` (`load_unsw_nb15`, `split_unsw`, `preprocess_unsw` y siete auxiliares), `s4-datos-pruebas-descripcion`, `s4-datos-pruebas` (21 pruebas con datos sintéticos), `s4-datos-carga-descripcion` y `s4-datos-carga` (verificación de archivos, resumen, duplicados, superposición en las 40 particiones y preprocesamiento con y sin L2). Referencia de Moustafa y Slay (2015) comprobada en Crossref. Para confirmar que las pruebas detectan errores, se introdujeron a propósito siete errores (partición sin estratificar, z-score ajustado con prueba, σ = 0 sin reemplazar, log1p con negativos, categorías tomadas de prueba, L2 solo en las numéricas y duplicados comparados con `id`): cada uno hizo fallar al menos una prueba. Leer sin `utf-8-sig` no es un error, porque pandas ya descarta el BOM. Notebook completo ejecutado desde un kernel limpio en Linux x86_64 con `jupyter nbconvert --execute`, sin `TP3_QUICK` (unos 3 min 15 s; salida fuera del repositorio): 20/20 pruebas de §1, 8/8 de §2, 21/21 de §4 (datos) y 13/13 de §4.3. `s4-datos-carga` se ejecutó sin errores: superposición media de 45.2 % (80/20) y 44.5 % (70/30); X de 195 columnas, sin `NaN`, en 0.7 s sin L2 y 1.3 s con L2. El diff del notebook solo agrega celdas de §4 (preparación de datos), sin salidas. | P3 integra T3; P1 hace T4. P3 sigue con T5. |
| 2026-11-25 | P3 (integración) | Integrada en `main` la rama `p3/t3-datos`, sin conflictos: `main` no había cambiado desde la reserva (`4f36e5f`). Las verificaciones son las de la fila anterior; las celdas integradas son idénticas a las ejecutadas. | P1 hace T4; P3 sigue con T5. |
| 2026-11-25 | P3 (datos en Git e historia de `main`) | **Historia reescrita:** los cuatro commits de T3 en `main` (`4f36e5f`, `d48a9b2`, `11b81e0` y `868f572`) se recrearon sin la línea `Co-Authored-By` que había agregado el asistente (`6210172`, `04308e9`, `9179837` y `d2c4c69`): los árboles de archivos, los autores y las fechas son idénticos, y `git diff 868f572 d2c4c69` sale vacío. Se publicó con force push en `main`, por decisión de P3, como excepción a `CONTRIBUTING.md`. Quien haya hecho pull antes: `git fetch origin` y `git reset --hard origin/main`. **Datos en Git:** se retiraron del `.gitignore` las exclusiones de `data/`, `results/raw/` y artefactos, y en `.gitattributes` se marcó `data/**` como binario. Comprobado: `git hash-object` con y sin filtros coincide para los dos CSV (bytes intactos, CRLF incluido). Actualizados `AGENTS.md`, `CONTRIBUTING.md`, `README.md`, este journal y `s4-datos-fuente`. El repositorio es público: subir los CSV redistribuye UNSW-NB15 (sus autores lo ofrecen para investigación académica, citando la fuente). | P3 sube los CSV y estos cambios; P1 y P2 hacen pull. |
| 2026-11-26 | P2 (entorno, T2a y T2b, rama `p2/t2-r2`) | **Entorno:** Python 3.15.0 instalado con `uv` (actualizado a 0.13.10: la 0.12.21 solo ofrecía 3.15.0rc2) en Linux x86_64 y `requirements.txt` en un `.venv` nuevo; las versiones coinciden con el archivo (solo faltan `appnope` y `pywinpty`) y `pip check` sale limpio. `nbdime config-git --enable` hecho; `git diff` del notebook requiere el `.venv` activado. PyCharm y Windows siguen sin comprobar. **T2a:** en §3, celdas `s3-planteamiento`, `s3-funciones-descripcion`, `s3-funciones` (siete funciones `s3_*`), `s3-pruebas` (15 pruebas), `s3-datos-descripcion`, `s3-datos`, `s3-experimento-descripcion`, `s3-max-weights`, `s3-experimento`, `s3-curvas-descripcion`, `s3-curvas`, `s3-errores-descripcion` y `s3-errores-finales`; decisiones en D10. **T2b:** `s3-alpha-descripcion`, `s3-alpha` (experimento complementario de α) y `s3-analisis` (comparación, ajuste de α según M y relación entre M y error, con LeCun et al. 1998 y Duchi et al. 2011); en `s3-investigacion-neuronas` se reemplazó la nota de pendiente. Para confirmar que las pruebas detectan errores, se introdujeron a propósito ocho errores (partición sin estratificar, programa lineal sin margen, desviación con ddof = 0, γ ignorado, error de la primera época, media en vez de mediana, semilla fija y T como vector): cada uno hizo fallar al menos una prueba. Notebook completo ejecutado cuatro veces (dos con T2a y dos con T2b, la última con las celdas integradas) desde un kernel limpio en Linux x86_64 con `jupyter nbconvert --execute`, sin `TP3_QUICK` (unos 2 min 10 s; salida fuera del repositorio): 20/20 pruebas de §1, 8/8 de §2, 15/15 de §3, 21/21 de §4 (datos) y 13/13 de §4.3; los resultados de §3 fueron idénticos en todas las ejecuciones (`max_weights` elegido = 1). El diff del notebook solo agrega celdas de §3 y modifica `s3-investigacion-neuronas`, sin salidas. | P2 integra T2a y T2b. |
| 2026-11-26 | P2 (integración) | Integrada en `main` la rama `p2/t2-r2`, sin conflictos: `main` no había cambiado desde la reserva (`9254913`). Las verificaciones son las de la fila anterior; las celdas integradas son idénticas a las ejecutadas. | P1 y P3 revisan D10; T8 revisa los números de `s3-analisis`. |
| 2026-11-26 | P2 (revisión de T1a y T1b) | Revisadas en `main` las celdas de §1 y §2 frente al enunciado y al contrato de la red. **T1a:** cumple el contrato. Una comprobación independiente del gradiente con diferencias centrales en cuatro arquitecturas que las pruebas no usan ([4,6,2], [3,1,1], [5,2,4] y [1,8,1]) da un error relativo máximo ≤ 10⁻⁸. La salida con K = 1 coincide con una red K = 2 cuya segunda columna de `W_s` es 0 (D3). La derivación y las referencias son correctas, y cada función tiene al menos dos pruebas. **T1b:** cubre los incisos a) a c) de §2. En Linux x86_64 los resultados son idénticos a los registrados en macOS (M = 4, `max_weights` = 2, α = 0.5, γ = 0; 20/20 semillas, época mediana 38; las cuatro entradas bien clasificadas). **Observaciones:** (1) con momentum, un peso recortado sigue acumulando `v`: en una prueba con γ = 0.9 y α = 0.1, `v` llegó a unos 2.5 α y el peso quedó 4 épocas en el límite después de invertirse el gradiente. No contradice el contrato, pero no está documentado. (2) La frase de `s2-planteamiento` sobre K = 2 frente a K = 1 no tiene respaldo en el notebook. (3) Fuera de T1: `s0-configuracion` todavía dice que los CSV de UNSW-NB15 quedan fuera de Git. No se modificó código. | P1 atiende (1) y (2); el equipo decide quién corrige (3). |
| 2026-11-26 | P2 (PyCharm en Linux) | PyCharm configurado en Linux x86_64: intérprete del proyecto `.venv` (Python 3.15.0, versiones de `requirements.txt`) y notebook en *IDE-Managed Server*. Ejecutadas en ese kernel, sin `TP3_QUICK`, las celdas `s0-config`, `s1-mlp-clase`, `s1-pruebas`, todas las celdas de código de §3 y `s4-3-funciones` y `s4-3-pruebas`: `s0-config` imprime Python 3.15.0 y las versiones fijadas; 20/20 pruebas de §1, 15/15 de §3 y 13/13 de §4.3 correctas; las celdas del experimento de §3 terminan sin errores (`max_weights` elegido = 1, como en T2b). No se ejecutaron §2 ni la preparación de datos de §4, que §3 y §4.3 no necesitan. PyCharm guardó solo las salidas en disco: frente a `HEAD` cambiaron únicamente `outputs`, `execution_count` y los metadatos de esas 13 celdas; `source`, los identificadores, el orden de las celdas y los metadatos del notebook (`kernelspec`) no cambiaron. Después, *Clear All Outputs* y guardar dejaron vacío el `git diff` del notebook. | P2 comprueba Windows (SciPy). |
| 2026-11-26 | P2 (revisión de D10, rama `p2/t2-d10`) | Revisada D10 frente al enunciado y al código de §3 en `main`. Los puntos (1), (2), (3) y (5) se sostienen. El punto (4) se mantiene, pero la elección es sensible al criterio: la media de las medianas elige `max_weights` = 1 por poco (0.102 frente a 0.115 y 0.116), la media de los log₁₀ elegiría 2 y el rango medio, 1 (2 frente a 2.125). En §3: `s3-max-weights` conserva los resultados de cada valor; la celda nueva `s3-max-weights-sensibilidad` muestra los tres criterios y las comparaciones de 3.2 b con cada valor, sin entrenar redes nuevas; `s3-experimento-descripcion` agrega que `max_weights` también fija la escala de la inicialización y que la variabilidad entre semillas refleja solo los pesos iniciales; `s3-analisis` agrega la sensibilidad y el piso del MSE que impone el recorte con M = 2. Con los cuatro valores, M = 20 termina con menos error que M = 2 y γ = 0.9 con menos que γ = 0 en los cuatro pares; el orden entre b) y c) se invierte con `max_weights` ≥ 2. Notebook completo ejecutado dos veces desde un kernel limpio en Linux x86_64 con `jupyter nbconvert --execute`, sin `TP3_QUICK` (unos 3 min; salida fuera del repositorio): 20/20 pruebas de §1, 8/8 de §2, 15/15 de §3, 21/21 de §4 (datos) y 13/13 de §4.3, sin errores; los resultados de §3 son los mismos que en `main` (`max_weights` elegido = 1). No se agregaron funciones ni pruebas. El diff del notebook solo toca celdas de §3, sin salidas. | P1 y P3 aceptan o comentan D10; P2 integra `p2/t2-d10`. |
| 2026-11-26 | P2 (integración) | Integrada en `main` la rama `p2/t2-d10`, sin conflictos: `main` no había cambiado desde la creación de la rama (`8667828`). P1 y P3 aceptaron D10. Las verificaciones son las de la fila anterior; las celdas integradas son idénticas a las ejecutadas. | T8 revisa los números de `s3-analisis`, incluida la sensibilidad a `max_weights`. |
| 2026-11-26 | P2 (entorno en Windows) | Python 3.15.0 de 64 bits instalado en Windows 11 (AMD64) con el administrador de instalaciones de Python (`py install 3.15.0-64`); se borró el `.venv` anterior (Python 3.14.7) y se creó uno nuevo con `requirements.txt`. `pip check` sale limpio y `nbdime config-git --enable` está hecho. **SciPy ya no está bloqueado:** SciPy 1.18.1 y scikit-learn 1.9.1 se importan, incluido `scipy.stats.wilcoxon`; el bloqueo de la DLL `_fblas` registrado el 2026-11-20 (con Python 3.14.7) no se repite; no se averiguó qué lo eliminó. Notebook completo ejecutado desde un kernel limpio con `jupyter nbconvert --execute`, sin `TP3_QUICK` (unos 2 min 16 s; salida fuera del repositorio), sin errores en ninguna celda: `s0-config` imprime Python 3.15.0 y las versiones fijadas; 20/20 pruebas de §1, 8/8 de §2, 15/15 de §3, 21/21 de §4 (datos) y 13/13 de §4.3. Resultados iguales a los de Linux y macOS: §2 elige M = 4, `max_weights` = 2, α = 0.5, γ = 0 (20/20 semillas, época 38); §3 elige `max_weights` = 1 con la misma sensibilidad al criterio; §4 cuenta 103 575 filas duplicadas (40.2 %). No se probó PyCharm en Windows. | Ninguno para T0 por parte de P2; P2 revisa T5 y T7 cuando lleguen. |

Al integrar cada tarea, agregar una fila y actualizar las casillas, el trabajo
en curso y los acuerdos. Registrar las verificaciones realmente ejecutadas y
cualquier bloqueo; no copiar resultados sin reproducirlos.
