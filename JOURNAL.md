# Journal y pendientes del TP3

Estado inicial al **18 de noviembre de 2026**: estructura preparada; no hay
soluciones, código de la red, datos descargados ni experimentos ejecutados.
Fecha indicada por el enunciado: **domingo 29 de noviembre de 2026**, sin hora.

Este archivo es la fuente del estado de trabajo. Leerlo antes de empezar una
tarea y actualizarlo al integrarla en `main`. `[x]` significa terminado y
verificado; `[ ]` significa pendiente.

## Equipo

| Etiqueta | Nombre | Secciones del notebook a su cargo |
| --- | --- | --- |
| P1 | Por asignar | §1 red base, §2 XOR y §4.1 clasificador UNSW-NB15 con L2 |
| P2 | Por asignar | §3 clasificador en R² y §4.3 ECE |
| P3 | Por asignar | Preparación de datos UNSW-NB15, §4.2 ensamble y §4.4 evaluación |

El reparto suma aproximadamente **30 puntos detallados por persona**: P1
asume §1 + §2 + §4.1; P2 asume §3 + §4.3; P3 asume §4.2 + §4.4. P3 asume
además la carga y el preprocesamiento de UNSW-NB15, que necesita para §4.2
y §4.4, para descargar a P1, que está en el camino crítico por la red base.
El encabezado de §4 anuncia 60 puntos, pero sus incisos suman 50; ver D7.

## Trabajo en curso

| Persona | Tarea | Rama | Estado |
| --- | --- | --- | --- |
| P1 | — | — | Sin iniciar |
| P2 | T2a (resto de §3) | — | En espera del generador (D4) y del contrato de la red (T0). La investigación de §3.2 b y el ECE de T6 ya están integrados en `main` |
| P3 | — | — | Sin iniciar |

- **Siguiente acción:** T0 con los tres: nombres, herramientas, contratos y
  dudas que bloquean las tareas de la fase 1.
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
| 1 | T1: perceptrón y XOR (§1 y §2) | P1 | T0 | P2 |
| 1 | T2a: datos R² y código del experimento (§3) | P2 | T0 y generador (D4) | P3 |
| 1 | T3: preparación de datos UNSW-NB15 | P3 | T0 | P1 |
| 1 | T5: ensamble e incertidumbre (§4.2) | P3 | T0 y material de apoyo (D4) | P2 |
| 1 | T6: ECE y sus pruebas (§4.3) | P2 | T0 y definición de ECE (D6) | P3 |
| 2 | T2b: ejecución y análisis R² (§3) | P2 | T1 y T2a | P1 |
| 2 | T4: clasificador UNSW-NB15 y L2 (§4.1) | P1 | T1 y T3 | P3 |
| 2 | T7: evaluación de ensambles (§4.4) | P3 | T3, T5 y T6; L2 de T4 | P2 |
| 3 | T8: ejecución final y entrega | P1 integra; revisan los tres | T2b, T4 y T7 | Los tres |

```text
Fase 0   T0 (los tres)
Fase 1   T1 (P1) · T2a (P2) · T6 (P2) · T3 (P3) · T5 (P3)   ← en paralelo
Fase 2   T2b (P2) ◄── T1 + T2a
         T4  (P1) ◄── T1 + T3
         T7  (P3) ◄── T3 + T5 + T6 (y decisión L2 de T4)
Fase 3   T8 (los tres) ◄── T2b + T4 + T7
```

Quien esté esperando una dependencia puede avanzar sus otras tareas de la
fase 1, revisar la rama de otra persona o investigar referencias.

## Secciones del notebook y responsables

El esqueleto de `notebooks/tp3_redes_neuronales.ipynb` tiene un encabezado
por sección. Cada persona agrega celdas solo debajo de los encabezados a su
cargo y no mueve ni edita celdas ajenas sin acordarlo.

| Sección del notebook | Responsable |
| --- | --- |
| 0. Configuración común | Se define en T0; los cambios posteriores se avisan al equipo |
| 1. Perceptrón de tres capas | P1 |
| 2. Clasificación de XOR | P1 |
| 3. Clasificador de datos en R² | P2 |
| 4. Preparación de datos UNSW-NB15 | P3 |
| 4.1 Clasificador UNSW-NB15 y normalización L2 | P1 |
| 4.2 Ensamble e incertidumbre | P3 |
| 4.3 Expected calibration error | P2 |
| 4.4 Evaluación de ensambles | P3 |

## Contratos entre secciones (acordar en T0)

Para trabajar en paralelo, estas interfaces deben quedar acordadas y
registradas en «Acuerdos vigentes» antes de la fase 1. Son pendientes, no
decisiones tomadas:

- **Red (§1 → §3 y §4.1):** firma del constructor con `gamma` (D2); formas de
  `X` (n × D) y `T` (n × K); representación de etiquetas y salida para
  K = 1 (D3); qué devuelve `train_mlp`; y cómo se obtiene el **error de
  validación por época** que pide §3.2, ya que `train_mlp(num_epochs, X, T,
  alpha, gamma)` no recibe datos de validación (por ejemplo, argumentos
  opcionales de validación, o garantizar que llamarla época a época conserva
  el estado del momentum).
- **Datos UNSW-NB15 (preparación → §4.1, §4.2 y §4.4):** funciones de carga,
  preprocesamiento con L2 opcional y particiones 80/20 y 70/30
  reproducibles; formato de `X` y de las etiquetas de la clase ataque.
- **Ensamble → ECE (§4.2 → §4.3 y §4.4):** qué devuelven `run_ensemble_uq`
  y `quantify_uncertainty_ensemble` (puntajes previos a la activación,
  varianza por muestra, formas) y qué recibe
  `calculate_expected_calibration_error` (D6). Propuesta de P2, pendiente de
  revisión de P3: el ECE recibe `X`, `y`, `uncertainties` (varianza por
  observación, forma (n,)) y `predictions` (etiquetas predichas con los
  puntajes previos a la activación, forma (n,)).
- **Configuración común (sección 0):** una semilla por sección, rutas de
  datos, bandera de L2 y, si se acuerda, un modo de ejecución reducida para
  el desarrollo; la ejecución final usa los valores del enunciado.

## Reglas de congruencia de las salidas

- Durante el desarrollo, el notebook se versiona **sin salidas** (nbstripout,
  ver `CONTRIBUTING.md`). Cada quien ejecuta localmente para verificar.
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

- [ ] Reemplazar P1/P2/P3 por los nombres del equipo.
- [ ] Acordar Python, validar `requirements.txt` y registrar versiones probadas.
- [ ] Instalar y configurar nbstripout y nbdime en cada clon (`CONTRIBUTING.md`).
- [ ] Resolver o dejar documentados D2, D3 y D5, que afectan el contrato de la red.
- [ ] Conseguir el material de apoyo y la función `generar_datos_R2` (D4).
- [ ] Acordar y registrar los contratos entre secciones.
- [ ] Crear la configuración común (sección 0) e integrar T0 en `main` antes
  de abrir las ramas de la fase 1.

### T1 — P1: perceptrón de tres capas y XOR (fase 1)

- [ ] Implementar `Multilayer_perceptron` y su constructor, incluyendo la
  representación matricial de pesos y el acuerdo sobre `gamma` (D2).
- [ ] Implementar `forward(X)` con tangente hiperbólica y la salida acordada (D3).
- [ ] Implementar `backpropagate_deltas(X, T)` y `update_weights(X, T)`.
- [ ] Implementar `train_mlp(num_epochs, X, T, alpha, gamma)` según el
  contrato y explicar la adaptación del descenso del gradiente con base en
  el material del curso (D5).
- [ ] Implementar `get_error(X, T)` con MSE y registrar el error por época.
- [ ] Documentar qué hace cada función y ejecutar al menos dos pruebas por
  función para cubrir la regla general del PDF. Como mínimos particulares,
  `forward` exige dos; constructor, entrenamiento, deltas, actualización y
  error exigen al menos una. Conservar también la captura de la prueba de entrenamiento.
- [ ] Resolver XOR: cuatro entradas booleanas y etiquetas, arquitectura y
  diagrama, calibración y curvas para los hiperparámetros probados.
- [ ] Reportar predicciones de las cuatro entradas, criterio de error cero y
  número de iteraciones de convergencia; distinguir clasificación y MSE (D5).
- [ ] Integrar en `main` y avisar a P2 y P3: desbloquea T2b y T4.

### T2a — P2: datos R² y código del experimento (fase 1)

- [ ] Incorporar el generador provisto; documentar sus parámetros y la semilla de la sección.
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

### T2b — P2: ejecución y análisis R² (fase 2, requiere T1)

- [ ] Ejecutar las ocho combinaciones con particiones comparables.
- [ ] Mostrar curvas de entrenamiento y validación, la tabla de gráficas y
  la tabla de errores finales por configuración y escenario.
- [ ] Analizar α, tamaño de capa oculta y error, citando los artículos dentro del notebook.
- [ ] Ejecutar desde cero e integrar en `main`.

### T3 — P3: preparación de datos UNSW-NB15 (fase 1)

- [ ] Elegir y registrar la fuente, versión, archivos y forma de obtener los
  datos; identificar clase ataque, atributos y columnas que puedan revelar la etiqueta.
- [ ] Preparar las categorías con one-hot usando los atributos exigidos;
  documentar el tratamiento de columnas y ajustar el preprocesamiento solo
  con entrenamiento, evitando filtrar información de prueba.
- [ ] Hacer la normalización L2 opcional mediante un parámetro.
- [ ] Definir particiones reproducibles 80 % / 20 % (§4.1) y 10 particiones
  70 % / 30 % (§4.4), con semillas registradas.
- [ ] Documentar y probar las funciones; integrar en `main` y avisar a P1.

### T4 — P1: UNSW-NB15 y comparación de normalización L2 (fase 2, requiere T1 y T3)

- [ ] Documentar la calibración de los hiperparámetros de la red implementada.
- [ ] Comparar con L2 y sin L2 en 30 corridas por tratamiento, emparejando
  particiones y semillas. Reportar tasa de aciertos y F1 de la clase ataque.
- [ ] Aplicar una prueba estadística adecuada, documentar supuestos y
  resultados, y decidir si usar L2 en el resto del proyecto.
- [ ] Registrar la decisión en la configuración común, ejecutar desde cero,
  integrar en `main` y avisar a P3.

### T5 — P3: ensamble y cuantificación de incertidumbre (fase 1)

- [ ] Revisar el material de apoyo y cerrar con P2 el contrato ensamble → ECE.
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
- [ ] Revisión de P3 del contrato ensamble → ECE (sobre todo `predictions`).
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

### T8 — Ejecución final y entrega (P1 integra; revisan los tres)

- [ ] Comprobar que los cuatro apartados del enunciado tienen respuestas,
  pruebas, referencias, tablas y gráficas dentro del notebook único.
- [ ] Fijar versiones en `requirements.txt` y ejecutar todo desde un kernel
  limpio con los valores del enunciado; registrar duración, datos, semillas
  y resultados de las pruebas.
- [ ] Conservar las salidas de esa ejecución en `main` (ver `CONTRIBUTING.md`),
  incluida la evidencia de la prueba de entrenamiento, y exportar a
  `results/` solo las figuras y tablas necesarias.
- [ ] Revisar en conjunto que el análisis cite los números de esa ejecución.
- [ ] Resolver D1 y preparar solo los archivos de entrega acordados en
  `submission/`, con instrucciones de reproducción y sin datos innecesarios.
- [ ] Verificar el paquete final antes de entregarlo por TEC Digital.

## Dudas del enunciado y materiales faltantes

Son pendientes de interpretación para el desarrollo, no decisiones ya tomadas.
Consultar las páginas indicadas del PDF y registrar el acuerdo al resolverlas.

| ID | Página | Afecta | Pendiente |
| --- | --- | --- | --- |
| D1 | 1 | T8 | El PDF pide un ZIP con fuentes LaTeX/LyX, PDF y Jupyter. La organización solicitada por el usuario concentra toda la respuesta en un solo notebook. Confirmar el formato final antes de generar documentos; mientras tanto no se inicia un informe separado. |
| D2 | 1 | T0, T1, T2a | La firma impresa de `__init__(neurons_per_layer, alpha, max_weights)` omite `gamma`, aunque el listado de argumentos sí lo exige. Acordar y documentar una interfaz coherente. |
| D3 | 2–4 | T0, T1, T2a, T2b | Se exige softmax de salida y en R² K = 1. Una softmax de un solo componente siempre vale 1 y no permite esa clasificación. Acordar con el docente la salida/representación a utilizar antes de implementar y dejar explícita la interpretación. |
| D4 | 3 y 5 | T2a | **Parcial.** El material de apoyo de ensambles y ECE ya está en `docs/assignment/EstimacionIncertidumbre.pdf` (sección 2: ensamble entrenado sobre N particiones del entrenamiento e incertidumbre como varianza de las predicciones; sección 4: ECE). Falta `generar_datos_R2`; conseguirlo antes de sustituirlo por una implementación supuesta. |
| D5 | 2–3 | T1 | Precisar qué variante de descenso del gradiente adaptativo se espera y su relación con momentum. El PDF alterna `get_error`/`evaluar_error` y `train_mlp`/`entrenar_red`. Acordar además cómo reportar “error cero” de XOR frente al MSE. |
| D6 | 5 | T5, T6 | **Acordado por P2 el 2026-11-20; pendiente de revisión de P3.** Definición del material (§4): ECE = Σ \|B_m\|/N · \|acc(B_m) − s̄(B_m)\|, ignorando cubetas vacías, con puntajes en [0, 1]. El material no fija la conversión de la varianza ni el número de cubetas, y la firma no recibe predicciones. Acuerdos: (1) puntaje s = 1 − varianza normalizada min-max, porque la varianza no está acotada y crece con la falta de confianza; (2) reportar además la correlación de Pearson entre incertidumbre y acierto, alternativa del material; (3) 10 cubetas de igual ancho, configurables; (4) agregar el parámetro `predictions`, con etiquetas obtenidas de la salida de la última capa antes de la activación. |
| D7 | 4–5 | T7 | §4 anuncia 60 puntos pero sus incisos suman 50. La última instrucción estadística termina en “verifique si existe” sin completar la hipótesis. Confirmar alcance; el plan conserva todos los incisos visibles. |

## Acuerdos vigentes

- La solución se escribirá solo en `notebooks/tp3_redes_neuronales.ipynb`.
- Desarrollo en paralelo: una rama por tarea, cada persona edita solo sus
  secciones del notebook y la integración en `main` es de una en una.
- El notebook se versiona sin salidas hasta la ejecución final de T8.
- Mantener un único `README.md` general en la raíz, sin README por carpeta.
- Los responsables son provisionales hasta asignar nombres; no se heredaron
  automáticamente los integrantes mencionados en el TP1.
- El notebook inicial contiene solo el esqueleto de encabezados por sección,
  sin código ni respuestas. Este journal describe trabajo futuro y no
  constituye una solución de la asignación.
- ECE de §4.3 según D6: confianza 1 − varianza normalizada, Pearson como
  complemento, 10 cubetas configurables y parámetro adicional `predictions`.

## Registro de trabajo

| Fecha | Responsable | Trabajo y verificación | Siguiente paso |
| --- | --- | --- | --- |
| 2026-11-18 | Preparación del repositorio | Revisados la estructura del TP1 y las cinco páginas del enunciado. Creada la base sin avances. Verificados el formato del notebook único y vacío, la identidad del PDF, los enlaces locales y las exclusiones de Git. Las dependencias de los experimentos siguen pendientes de validar. | T0: asignar nombres, materiales e interpretaciones. |
| 2026-11-18 | Simplificación de documentación | Centralizadas las indicaciones en el README general y retirados los cinco README de subcarpetas. Se conserva la estructura con archivos vacíos. | T0 sigue pendiente. |
| 2026-11-20 | P2 (reorganización) | Reemplazada la secuencia en cascada por un plan en paralelo según las dependencias reales del enunciado. Asignada a P3 la preparación de datos UNSW-NB15. Agregados contratos entre secciones, reglas de congruencia de salidas, flujo por ramas con nbstripout y nbdime, y esqueleto de encabezados en el notebook. No se ejecutó código ni se instalaron las herramientas. | T0: aprobar el reparto entre los tres, instalar herramientas y acordar contratos. |
| 2026-11-20 | P2 (T2a, rama `p2/t2a-r2`) | Redactada la investigación de §3.2 b (neuronas ocultas frente a entradas) con referencias a Hornik et al. 1989, Sartori y Antsaklis 1991, Huang 2003, Barron 1994, Sheela y Deepa 2013 y Stathakis 2009; autores, revista, volumen, páginas y DOI comprobados en fuentes en línea. Solo Markdown; no se ejecutó código. El resto de T2a espera `generar_datos_R2` (D4) y el contrato de la red (T0). | Conseguir el generador y el material de apoyo de ECE; acordar contratos en T0. |
| 2026-11-20 | P2 (T6, rama `p2/t6-ece`) | Agregado el material de apoyo `docs/assignment/EstimacionIncertidumbre.pdf` y registrados los acuerdos de D6. Implementado el ECE de §4.3 con tres funciones auxiliares y 13 pruebas unitarias. Notebook ejecutado desde un kernel limpio con `jupyter nbconvert --execute` (copia fuera del repositorio): 13/13 pruebas correctas. Entorno: Python 3.14.7 y NumPy 2.5.5 en `.venv` local. **Bloqueo:** en esta máquina, el Control de aplicaciones de Windows impide cargar la DLL `_fblas` de SciPy, por lo que no se pueden importar SciPy ni scikit-learn. §4.3 no los usa, pero §3 (partición con `sklearn`) y las pruebas estadísticas de §4.1 y §4.4 sí. | P3 revisa el contrato ensamble → ECE; en T0, comprobar SciPy y scikit-learn en las otras máquinas y buscar una solución para esta. |
| 2026-11-20 | P2 (integración) | Integradas en `main` las ramas `p2/t2a-r2` y `p2/t6-ece`. El único conflicto fue el de las dos filas agregadas al registro; se conservaron ambas. Notebook integrado ejecutado desde un kernel limpio con `jupyter nbconvert --execute` (copia fuera del repositorio): 13/13 pruebas de §4.3 correctas. | P3 revisa el contrato ensamble → ECE; T0 sigue pendiente. |

Al integrar cada tarea, agregar una fila y actualizar las casillas, el trabajo
en curso y los acuerdos. Registrar las verificaciones realmente ejecutadas y
cualquier bloqueo; no copiar resultados sin reproducirlos.
