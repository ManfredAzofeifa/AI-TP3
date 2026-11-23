# Instrucciones para trabajar en AI-TP3

Antes de trabajar, leer `JOURNAL.md`, `CONTRIBUTING.md` y el enunciado de
`docs/assignment/TP_3_redes_neuronales.pdf`. El estado de las tareas, los
responsables, las dependencias, el trabajo en curso y las dudas abiertas se
mantienen en `JOURNAL.md`; revisarlo también antes de dar una tarea por terminada.

## Alcance

- Este repositorio empieza como estructura de trabajo, sin soluciones del TP1
  ni del TP3. No incorporar implementaciones, resultados o conclusiones del
  repositorio de referencia.
- La única fuente de la solución es
  `notebooks/tp3_redes_neuronales.ipynb`: código, funciones auxiliares, pruebas
  unitarias, explicaciones, referencias, experimentos y conclusiones van allí.
- Usar la extensión estándar de Jupyter, `.ipynb`. No crear otros notebooks,
  módulos `utils.py` ni scripts con partes de la solución.
- Los Markdown del repositorio son guías de trabajo; no deben responder los
  ejercicios. `results/` solo contiene exportaciones del notebook.
- Mantener un único `README.md` general en la raíz; no crear README por carpeta.
- `docs/report/` recibe el informe LaTeX de T9 y `submission/` el ZIP de
  entrega. El informe se redacta en T9, con el notebook ya terminado en T8
  (D1 en `JOURNAL.md`); hasta entonces el trabajo va solo al notebook.

## Coordinación

- El desarrollo es en paralelo, con una rama por tarea según `CONTRIBUTING.md`.
  Editar solo las celdas de las secciones del notebook que el journal asigna
  a la persona de la tarea; no mover ni modificar celdas de otras secciones
  sin acordarlo.
- Respetar las dependencias del journal: no ejecutar ni reportar resultados
  que dependan de una tarea todavía no integrada en `main`. El código puede
  escribirse antes contra los contratos acordados en T0.
- No cambiar contratos entre secciones ni la configuración común sin
  registrar el acuerdo en el journal.
- Versionar el notebook sin salidas hasta la ejecución final de T8: limpiarlas
  antes de cada commit y revisar `git diff` (ver `CONTRIBUTING.md`). Cada
  sección usa su propia semilla de `SEEDS` y nombres de variables con prefijo.
- Integrar en `main` de una persona a la vez, después de actualizar la rama
  con `main`.
- Actualizar el journal al integrar: tarea, verificaciones, decisiones,
  pendientes y a quién se desbloquea. No marcar como hecho lo no ejecutado.
- Si una duda del enunciado afecta la implementación, registrarla y documentar
  el acuerdo antes de aplicar una interpretación. No resolverla silenciosamente.

## Implementación y verificación cuando comience el desarrollo

- Mantener configuración, semillas, dependencias y parámetros reproducibles.
- Implementar la red solicitada; no sustituir sus métodos por un clasificador
  ya entrenado de una biblioteca. Las bibliotecas de apoyo se acuerdan al inicio.
- Documentar funciones y sus pruebas dentro del notebook; consultar el journal
  para los mínimos exigidos y las inconsistencias del enunciado.
- Reiniciar el kernel y ejecutar todas las celdas antes de integrar una tarea
  con código. Registrar si algo no pudo ejecutarse y por qué.
- Mantener los datos completos y artefactos transitorios fuera de Git. Registrar
  su origen, preparación y rutas para que otra persona pueda reproducirlos.
- No inventar métricas, ejecuciones, referencias ni resultados. No descargar
  datasets ni ejecutar experimentos si la tarea solo prepara documentación
  o estructura.
