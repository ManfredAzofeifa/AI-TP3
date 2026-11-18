# Instrucciones para trabajar en AI-TP3

Antes de trabajar, leer `JOURNAL.md`, `CONTRIBUTING.md` y el enunciado de
`docs/assignment/TP_3_redes_neuronales.pdf`. El estado de las tareas, los
responsables, el turno de edición y las dudas abiertas se mantienen en
`JOURNAL.md`; revisarlo también antes de dar una tarea por terminada.

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
- `docs/report/` y `submission/` son reservas para la entrega. La diferencia
  entre el notebook único acordado y el formato LaTeX/LyX + PDF del enunciado
  está anotada en `JOURNAL.md`; no iniciar un informe independiente.

## Coordinación

- Trabajar por turnos en el orden de `JOURNAL.md`. Solo una persona edita el
  notebook a la vez, aunque las tareas sean de secciones distintas.
- La siguiente persona comienza desde el último estado compartido de `main`.
  No reorganizar celdas de otra tarea durante un turno sin acordarlo.
- Actualizar el journal al terminar: tarea, verificaciones, decisiones,
  pendientes y siguiente responsable. No marcar como hecho lo no ejecutado.
- Si una duda del enunciado afecta la implementación, registrarla y documentar
  el acuerdo antes de aplicar una interpretación. No resolverla silenciosamente.

## Implementación y verificación cuando comience el desarrollo

- Mantener configuración, semillas, dependencias y parámetros reproducibles.
- Implementar la red solicitada; no sustituir sus métodos por un clasificador
  ya entrenado de una biblioteca. Las bibliotecas de apoyo se acuerdan al inicio.
- Documentar funciones y sus pruebas dentro del notebook; consultar el journal
  para los mínimos exigidos y las inconsistencias del enunciado.
- Reiniciar el kernel y ejecutar todas las celdas antes de entregar el turno
  con código. Registrar si algo no pudo ejecutarse y por qué.
- Mantener los datos completos y artefactos transitorios fuera de Git. Registrar
  su origen, preparación y rutas para que otra persona pueda reproducirlos.
- No inventar métricas, ejecuciones, referencias ni resultados. No descargar
  datasets ni ejecutar experimentos si la tarea solo prepara documentación
  o estructura.
