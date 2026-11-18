# Journal y pendientes del TP3

Estado inicial al **18 de noviembre de 2026**: estructura preparada; no hay
soluciones, código de la red, datos descargados ni experimentos ejecutados.
Fecha indicada por el enunciado: **domingo 29 de noviembre de 2026**, sin hora.

Este archivo es la fuente del estado de trabajo. Leerlo antes de cada turno y
actualizarlo antes de pasarlo a otra persona. `[x]` significa terminado y
verificado; `[ ]` significa pendiente.

## Equipo y turno

| Etiqueta | Nombre | Responsabilidad principal |
| --- | --- | --- |
| P1 | Por asignar | Red base, XOR y clasificador UNSW-NB15 |
| P2 | Por asignar | Datos R², comparación de redes y ECE |
| P3 | Por asignar | Ensamble, incertidumbre y evaluación de costo/calibración |

- **Turno del notebook:** libre; el siguiente es T0 con P1 como coordinador.
- **Tarea en curso:** ninguna.
- **Siguiente acción:** asignar nombres y resolver las dudas que bloquean T1.
- Solo una persona edita el notebook y registra el estado de ese turno.

## Orden de trabajo entre tres personas

| Orden | Tarea | Responsable | Depende de | Revisión sugerida |
| --- | --- | --- | --- | --- |
| 0 | T0: acuerdos, materiales y entorno | P1 coordina; participan los tres | — | P2 y P3 |
| 1 | T1: perceptrón y XOR (§1 y §2) | P1 | T0 y dudas de la red resueltas | P2 |
| 2 | T2: clasificador en R² (§3) | P2 | T1 y generador disponible | P3 |
| 3 | T3: clasificador UNSW-NB15 y L2 (§4.1) | P1 | T2 | P2 |
| 4 | T4: ensamble e incertidumbre (§4.2) | P3 | T3 y material de apoyo | P1 |
| 5 | T5: ECE y sus pruebas (§4.3) | P2 | T4 y definición de ECE acordada | P3 |
| 6 | T6: evaluación de ensambles (§4.4) | P3 | T5 | P2 |
| 7 | T7: ejecución final y entrega | P1 integra; revisan los tres | T6 y formato de entrega acordado | P2 y P3 |

El reparto suma aproximadamente **30 puntos detallados por persona**: P1
asume §1 + §2 + §4.1; P2 asume §3 + §4.3; P3 asume §4.2 + §4.4. La carga
real puede variar; P1 integra y los otros dos apoyan la revisión. El encabezado
de §4 anuncia 60 puntos, pero sus incisos suman 50; ver D7.

Quien todavía no tenga turno puede leer el material, investigar referencias
o revisar el cambio anterior. Las modificaciones al notebook se integran
siguiendo la secuencia de la tabla, sin editores simultáneos.

## Pendientes por tarea

### T0 — Acuerdos iniciales

- [ ] Reemplazar P1/P2/P3 por los nombres del equipo y acordar los turnos.
- [ ] Resolver o dejar documentados los acuerdos de D1–D7 que afecten la tarea siguiente.
- [ ] Conseguir el material de apoyo y la función `generar_datos_R2` (D4).
- [ ] Acordar Python, validar `requirements.txt` y registrar versiones probadas.
- [ ] Acordar representación de muestras y etiquetas, interfaz de la red,
  semillas y criterio de convergencia, para reutilizarlos en todo el notebook.

### T1 — P1: perceptrón de tres capas y XOR

- [ ] Preparar en el notebook las celdas de configuración, semillas y documentación.
- [ ] Implementar `Multilayer_perceptron` y su constructor, incluyendo la
  representación matricial de pesos y el acuerdo sobre `gamma` (D2).
- [ ] Implementar `forward(X)` con tangente hiperbólica y la salida acordada (D3).
- [ ] Implementar `backpropagate_deltas(X, T)` y `update_weights(X, T)`.
- [ ] Implementar `train_mlp(num_epochs, X, T, alpha, gamma)` y explicar la
  adaptación del descenso del gradiente con base en el material del curso (D5).
- [ ] Implementar `get_error(X, T)` con MSE y registrar el error por época.
- [ ] Documentar qué hace cada función y ejecutar al menos dos pruebas por
  función para cubrir la regla general del PDF. Como mínimos particulares,
  `forward` exige dos; constructor, entrenamiento, deltas, actualización y
  error exigen al menos una. Conservar también la captura de la prueba de entrenamiento.
- [ ] Resolver XOR: cuatro entradas booleanas y etiquetas, arquitectura y
  diagrama, calibración y curvas para los hiperparámetros probados.
- [ ] Reportar predicciones de las cuatro entradas, criterio de error cero y
  número de iteraciones de convergencia; distinguir clasificación y MSE (D5).
- [ ] Ejecutar desde cero y entregar a P2 la interfaz y las pruebas de la red.

### T2 — P2: clasificador en R²

- [ ] Incorporar el generador provisto; documentar sus parámetros y semillas.
- [ ] Generar y graficar un conjunto linealmente separable y otro no separable.
- [ ] Usar la partición 80 % entrenamiento / 20 % validación de `sklearn`.
- [ ] Probar las cuatro configuraciones con D = 2, K según el acuerdo D3,
  α = 0.01, M ∈ {20, 2} y γ ∈ {0, un valor no nulo documentado}.
- [ ] Entrenar cada configuración durante P = 50 iteraciones en ambos
  escenarios: ocho combinaciones en total, con particiones comparables.
- [ ] Mostrar curvas de entrenamiento y validación, una tabla de gráficas y
  una tabla de errores finales por configuración y escenario.
- [ ] Analizar α, tamaño de capa oculta y error; investigar la relación con
  el número de entradas y citar artículos científicos dentro del notebook.
- [ ] Ejecutar desde cero y entregar el notebook a P1.

### T3 — P1: UNSW-NB15 y comparación de normalización L2

- [ ] Elegir y registrar la fuente, versión, archivos y forma de obtener los
  datos; identificar clase ataque, atributos y columnas que puedan revelar la etiqueta.
- [ ] Preparar las categorías con one-hot usando los atributos exigidos;
  documentar el tratamiento de columnas y ajustar el preprocesamiento solo
  con entrenamiento, evitando filtrar información de prueba.
- [ ] Definir particiones reproducibles 80 % entrenamiento / 20 % prueba y
  documentar la calibración de los hiperparámetros de la red implementada.
- [ ] Comparar con L2 y sin L2 en 30 corridas por tratamiento, emparejando
  particiones y semillas. Reportar tasa de aciertos y F1 de la clase ataque.
- [ ] Aplicar una prueba estadística adecuada, documentar supuestos y
  resultados, y decidir si usar L2 en el resto del proyecto.
- [ ] Ejecutar desde cero y dejar a P3 el protocolo de datos y el modelo base.

### T4 — P3: ensamble y cuantificación de incertidumbre

- [ ] Revisar el material de apoyo y acordar la interfaz del ensamble con P2.
- [ ] Implementar `train_ensemble` con modelos de mínimos cuadrados de
  clasificación según el enunciado, documentando cómo se construyen sus miembros.
- [ ] Implementar `run_ensemble_uq` para evaluar la varianza de las salidas.
- [ ] Implementar `quantify_uncertainty_ensemble(x, model, N=10)` reutilizando
  el ensamble entrenado; usar puntajes del producto punto antes de la activación.
- [ ] Documentar y ejecutar al menos dos pruebas unitarias de la
  cuantificación; cubrir también las funciones auxiliares según la regla general.
- [ ] Ejecutar desde cero y entregar a P2 las salidas y su significado para ECE.

### T5 — P2: expected calibration error

- [ ] Resolver con el material de apoyo la definición, entradas, intervalos y
  procedencia de predicciones/puntajes de ECE; registrar el acuerdo D6.
- [ ] Implementar `calculate_expected_calibration_error(X, y, uncertainties)`
  según la definición acordada y documentar la relación con la última capa.
- [ ] Diseñar, ejecutar y explicar al menos dos pruebas unitarias de ECE.
- [ ] Ejecutar desde cero y entregar a P3 la función y su protocolo de evaluación.

### T6 — P3: ECE, costo de ejecución y comparación de ensambles

- [ ] Crear 10 particiones reproducibles de 70 % entrenamiento / 30 % prueba.
- [ ] Evaluar N ∈ {10, 100, 1000} sobre las mismas particiones comparables:
  30 combinaciones de tamaño y partición. Registrar semillas y protocolo.
- [ ] Medir ECE y tiempo; especificar qué incluye cada tiempo y registrar el entorno.
- [ ] Reportar media y desviación estándar del ECE por N y los tiempos medidos.
- [ ] Aplicar una prueba estadística adecuada para comparar configuraciones,
  documentando la interpretación adoptada ante la frase incompleta de D7.
- [ ] Graficar y comentar los resultados dentro del notebook; exportar solo
  las figuras y tablas que se necesiten en `results/`.
- [ ] Ejecutar desde cero y pasar a revisión final con P1.

### T7 — Revisión conjunta y entrega

- [ ] Comprobar que los cuatro apartados del enunciado tienen respuestas,
  pruebas, referencias, tablas y gráficas dentro del notebook único.
- [ ] Ejecutar todo desde un kernel limpio y registrar dependencias, duración,
  datos utilizados, semillas y resultados de las pruebas.
- [ ] Revisar en conjunto los resultados y conservar las salidas finales
  necesarias, incluida la evidencia de la prueba de entrenamiento.
- [ ] Resolver D1 y preparar solo los archivos de entrega acordados en
  `submission/`, con instrucciones de reproducción y sin datos innecesarios.
- [ ] Verificar el paquete final antes de entregarlo por TEC Digital.

## Dudas del enunciado y materiales faltantes

Son pendientes de interpretación para el desarrollo, no decisiones ya tomadas.
Consultar las páginas indicadas del PDF y registrar el acuerdo al resolverlas.

| ID | Página | Pendiente |
| --- | --- | --- |
| D1 | 1 | El PDF pide un ZIP con fuentes LaTeX/LyX, PDF y Jupyter. La organización solicitada por el usuario concentra toda la respuesta en un solo notebook. Confirmar el formato final antes de generar documentos; mientras tanto no se inicia un informe separado. |
| D2 | 1 | La firma impresa de `__init__(neurons_per_layer, alpha, max_weights)` omite `gamma`, aunque el listado de argumentos sí lo exige. Acordar y documentar una interfaz coherente. |
| D3 | 2–4 | Se exige softmax de salida y en R² K = 1. Una softmax de un solo componente siempre vale 1 y no permite esa clasificación. Acordar con el docente la salida/representación a utilizar antes de implementar y dejar explícita la interpretación. |
| D4 | 3 y 5 | No se adjuntaron `generar_datos_R2` ni el material de apoyo de ensambles/ECE. Conseguirlos antes de sustituirlos por una implementación supuesta. |
| D5 | 2–3 | Precisar qué variante de descenso del gradiente adaptativo se espera y su relación con momentum. El PDF alterna `get_error`/`evaluar_error` y `train_mlp`/`entrenar_red`. Acordar además cómo reportar “error cero” de XOR frente al MSE. |
| D6 | 5 | La firma de ECE no recibe modelo ni predicciones; el texto habla de “pesos” de la última capa y antes usa puntajes previos a activación. Verificar en el material de apoyo qué valores y definición de calibración se esperan. |
| D7 | 4–5 | §4 anuncia 60 puntos pero sus incisos suman 50. La última instrucción estadística termina en “verifique si existe” sin completar la hipótesis. Confirmar alcance; el plan conserva todos los incisos visibles. |

## Acuerdos vigentes

- La solución se escribirá solo en `notebooks/tp3_redes_neuronales.ipynb`.
- Se usará un turno de edición para todo el notebook, con traspaso secuencial.
- Mantener un único `README.md` general en la raíz, sin README por carpeta.
- Los responsables son provisionales hasta asignar nombres; no se heredaron
  automáticamente los integrantes mencionados en el TP1.
- El notebook inicial queda vacío. Este journal describe trabajo futuro y
  no constituye una solución de la asignación.

## Registro de trabajo

| Fecha | Responsable | Trabajo y verificación | Siguiente paso |
| --- | --- | --- | --- |
| 2026-11-18 | Preparación del repositorio | Revisados la estructura del TP1 y las cinco páginas del enunciado. Creada la base sin avances. Verificados el formato del notebook único y vacío, la identidad del PDF, los enlaces locales y las exclusiones de Git. Las dependencias de los experimentos siguen pendientes de validar. | T0: asignar nombres, materiales e interpretaciones. |
| 2026-11-18 | Simplificación de documentación | Centralizadas las indicaciones en el README general y retirados los cinco README de subcarpetas. Se conserva la estructura con archivos vacíos. | T0 sigue pendiente. |

En cada turno agregar una fila y actualizar las casillas, el turno y los
acuerdos. Registrar las verificaciones realmente ejecutadas y cualquier
bloqueo; no copiar resultados sin reproducirlos.
