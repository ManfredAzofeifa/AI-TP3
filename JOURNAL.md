# Journal y pendientes del TP3

Estado al **23 de noviembre de 2026**: T0 (acuerdos, contratos, entorno y
configuración común) en la rama `p1/t0-acuerdos`, pendiente de revisión de P2 y
P3. En `main` están la investigación de §3.2 b y el ECE de §4.3; no hay código
de la red, datos descargados ni experimentos ejecutados.
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
| P1 | T0 | `p1/t0-acuerdos` | Acuerdos, contratos, entorno y §0 listos; falta la comprobación en PyCharm antes de integrar |
| P2 | T2a (resto de §3) | — | En espera de la integración de T0 para instalar el entorno fijado. La investigación de §3.2 b y el ECE de T6 ya están integrados en `main` |
| P3 | — | — | En espera de la integración de T0 para instalar el entorno fijado; luego T3 y T5 |

- **Siguiente acción:** P1 comprueba el guardado en PyCharm e integra T0 en
  `main`. Después, P2 y P3 instalan el entorno fijado y se abren las ramas de
  la fase 1.
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
  instancia nueva los reinicia. T1a documenta el valor de ε.
- **`train_mlp(num_epochs, X, T, alpha, gamma, X_val=None, T_val=None)`:**
  `alpha` y `gamma` reemplazan los valores guardados. Devuelve
  `{"train_error": [...], "val_error": [...]}`, con un valor por época medido
  después de la actualización de esa época; `val_error` queda vacía si no se
  pasan datos de validación. Así §3 obtiene la curva de validación que pide.
- **`get_error(X, T)`:** MSE promediado sobre n · K, es decir, la media de
  (y − t)² sobre todas las observaciones y salidas.
- **`predict(X)`:** etiquetas enteras de forma (n,): argmax si K ≥ 2 y umbral
  0.5 si K = 1.

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
- [ ] Después de integrar T0, P2 (Linux y Windows) y P3 (Linux): instalar
  Python 3.15.0 y `requirements.txt` en un entorno nuevo, y ejecutar
  `s0-config` y §4.3. En
  Windows, comprobar si el Control de aplicaciones sigue bloqueando SciPy; si
  ocurre, ejecutar en Linux las secciones que usan SciPy o `sklearn`.
- [x] Retirar nbstripout: renumeraba los identificadores de celda y
  reformateaba todo el archivo. Las salidas se limpian con *Clear All Outputs*
  de PyCharm. Se versionan en `.gitattributes` las líneas de nbdime.
- [ ] Configurar nbdime en cada clon (`nbdime config-git --enable`).
- [ ] Comprobar en PyCharm, con el notebook de esta rama: abrir, *Clear All
  Outputs*, guardar y confirmar que `git diff` queda vacío o solo cambia lo
  esperado (contadores de ejecución, metadatos de PyCharm, nombre del kernel).
  Registrar lo que haya que hacer a mano.
- [x] Resolver D2, D3 y D5, que afectan el contrato de la red.
- [x] Resolver D4: los datos de R² se generan con scikit-learn, con
  autorización del docente. El material de apoyo ya está en `docs/assignment/`.
- [x] Acordar y registrar los contratos entre secciones. P3 aceptó el
  contrato ensamble → ECE, incluido `predictions`.
- [x] Crear la configuración común (celda `s0-config`).
- [ ] Integrar T0 en `main` antes de abrir las ramas de la fase 1.

### T1a — P1: clase `Multilayer_perceptron` y sus pruebas (fase 1)

- [ ] Implementar `Multilayer_perceptron` y su constructor según el
  contrato, con la representación matricial de pesos (D2).
- [ ] Implementar `forward(X)` con tangente hiperbólica y softmax; con K = 1,
  softmax([p, 0]) (D3).
- [ ] Implementar `backpropagate_deltas(X, T)` y `update_weights(X, T)`. El
  material deriva los deltas con sigmoide; con softmax y MSE, el delta de
  salida usa el jacobiano de la softmax. Documentar la derivación.
- [ ] Implementar `train_mlp` con AdaGrad y momentum según el contrato (D5),
  y explicar qué cambia respecto de la retropropagación vista en clase.
- [ ] Implementar `get_error(X, T)` con MSE y registrar el error por época.
- [ ] Documentar qué hace cada función y ejecutar al menos dos pruebas por
  función para cubrir la regla general del PDF. Como mínimos particulares,
  `forward` exige dos; constructor, entrenamiento, deltas, actualización y
  error exigen al menos una. Conservar también la captura de la prueba de
  entrenamiento, como adjunto de una celda Markdown.
- [ ] Integrar en `main` y avisar a P2 y P3: desbloquea T2b y T4.

### T1b — P1: XOR (fase 1, requiere T1a)

- [ ] Resolver XOR: cuatro entradas booleanas y etiquetas, arquitectura y
  diagrama, calibración y curvas para los hiperparámetros probados.
- [ ] Reportar predicciones de las cuatro entradas, criterio de error cero y
  número de iteraciones de convergencia; distinguir clasificación y MSE (D5).
- [ ] Integrar en `main`.

### T2a — P2: datos R² y código del experimento (fase 1)

- [ ] Generar los datos con `sklearn.datasets` (D4); documentar las funciones,
  sus parámetros y la semilla de la sección.
- [ ] Generar y graficar un conjunto linealmente separable y otro no separable.
- [ ] Preparar la partición 80 % entrenamiento / 20 % validación de `sklearn`.
- [ ] Escribir, contra el contrato de la red, el código de las cuatro
  configuraciones (D = 2, K según D3, α = 0.01, M ∈ {20, 2}, γ ∈ {0, un valor
  no nulo documentado}) en ambos escenarios con P = 50 iteraciones, y el de
  las curvas, la tabla de gráficas y la tabla de errores finales.
- [x] Investigar la relación entre neuronas ocultas y de entrada, y reunir
  los artículos científicos que se citarán. Redactado en la celda
  `s3-investigacion-neuronas` con seis referencias cuyos datos se verificaron
  en línea; las preguntas que dependen de resultados quedan para T2b.
- [ ] Integrar en `main` lo que no depende de resultados.

### T2b — P2: ejecución y análisis R² (fase 2, requiere T1a)

- [ ] Ejecutar las ocho combinaciones con particiones comparables.
- [ ] Mostrar curvas de entrenamiento y validación, la tabla de gráficas y
  la tabla de errores finales por configuración y escenario.
- [ ] Analizar α, tamaño de capa oculta y error, citando los artículos dentro del notebook.
- [ ] Ejecutar desde cero e integrar en `main`.

### T3 — P3: preparación de datos UNSW-NB15 (fase 1)

- [ ] Descargar los dos CSV particionados oficiales en `data/raw/unsw_nb15/`
  y registrar la URL, los conteos y una suma de verificación de cada archivo.
- [ ] Confirmar la clase ataque, los atributos y las columnas excluidas
  (`id`, `label`, `attack_cat`) según el contrato de datos.
- [ ] Implementar `load_unsw_nb15`, `split_unsw` y `preprocess_unsw` con el
  orden acordado: one-hot, log1p, z-score ajustado con entrenamiento y L2 por
  fila opcional (`l2`).
- [ ] Definir las 30 particiones 80 % / 20 % (§4.1) y las 10 particiones
  70 % / 30 % (§4.4), con semillas derivadas de `SEEDS["s4_datos"]`.
- [ ] Documentar y probar las funciones; integrar en `main` y avisar a P1.

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
| D5 | 2–3 | T1a, T1b | **Acordado en T0, salvo XOR.** El docente se refiere a AdaGrad con «descenso del gradiente adaptativo». Se implementa AdaGrad con momentum γ (contrato de la red); γ = 0 es AdaGrad puro. Se usan los nombres `get_error` y `train_mlp`, aunque el PDF también dice `evaluar_error` y `entrenar_red`. Falta acordar en T1b cómo reportar el «error cero» de XOR frente al MSE. |
| D6 | 5 | T5, T6 | **Acordado por P2 el 2026-11-20; aceptado por P3 el 2026-11-23.** Definición del material (§4): ECE = Σ \|B_m\|/N · \|acc(B_m) − s̄(B_m)\|, ignorando cubetas vacías, con puntajes en [0, 1]. El material no fija la conversión de la varianza ni el número de cubetas, y la firma no recibe predicciones. Acuerdos: (1) puntaje s = 1 − varianza normalizada min-max, porque la varianza no está acotada y crece con la falta de confianza; (2) reportar además la correlación de Pearson entre incertidumbre y acierto, alternativa del material; (3) 10 cubetas de igual ancho, configurables; (4) agregar el parámetro `predictions`, con etiquetas obtenidas de la salida de la última capa antes de la activación. |
| D7 | 4–5 | T7 | §4 anuncia 60 puntos pero sus incisos suman 50. La última instrucción estadística termina en “verifique si existe” sin completar la hipótesis. Confirmar alcance; el plan conserva todos los incisos visibles. |
| D8 | 4–5 | T3, T4, T5, T7 | **Acordado en T0.** «Normalización L2» no está definida y los atributos crudos de UNSW-NB15 van de 0/1 hasta unos 10⁹: sin escalar, la tangente hiperbólica se satura, y una L2 sobre datos crudos borraría casi todos los atributos. Se interpreta como L2 por fila sobre un preprocesamiento base común (one-hot, log1p y z-score); ver el contrato de datos y el protocolo de comparación. |

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

Al integrar cada tarea, agregar una fila y actualizar las casillas, el trabajo
en curso y los acuerdos. Registrar las verificaciones realmente ejecutadas y
cualquier bloqueo; no copiar resultados sin reproducirlos.
