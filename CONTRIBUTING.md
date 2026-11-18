# Colaboración entre tres personas

El plan y el turno actual están en [JOURNAL.md](JOURNAL.md). P1, P2 y P3 son
etiquetas provisionales: reemplazarlas por los nombres del equipo al iniciar.

## Un turno a la vez

1. Leer el journal y acordar quién toma el siguiente turno. Solo esa persona
   edita el notebook; las otras pueden revisar o investigar sin modificarlo.
2. Una vez que exista el primer commit compartido, comenzar cada turno con
   `git switch main` y `git pull --ff-only`. Registrar el turno en el journal.
3. Resolver una tarea concreta en `notebooks/tp3_redes_neuronales.ipynb`.
   Toda la solución se mantiene en ese archivo, incluidas pruebas y análisis.
4. Si hubo código, reiniciar el kernel y ejecutar el notebook de principio a
   fin. Revisar las pruebas y evitar salidas transitorias voluminosas.
5. Actualizar el journal, crear un commit descriptivo y hacer
   `git push origin main`. Avisar al siguiente responsable cuando el cambio esté disponible.

El flujo habitual usa commits pequeños directamente en `main`. Los pull
requests son opcionales; no se necesitan ramas permanentes por persona.
Una edición del journal para reservar el turno debe compartirse antes de
empezar, junto con el aviso al equipo.

Si `pull --ff-only` falla o `push` es rechazado, detener la edición y coordinar
con quien cambió `main`. No usar `push --force` ni fusionar a ciegas el JSON
del notebook. El siguiente turno comienza después de integrar el anterior.

## Antes de entregar el turno

- Notebook único, celdas en orden y pruebas relevantes ejecutadas.
- Dependencias nuevas anotadas en `requirements.txt` y semillas registradas.
- Datos locales fuera de Git; figuras y tablas compartidas solo si son útiles.
- Journal actualizado con lo hecho, lo pendiente y las decisiones adoptadas.

Durante el desarrollo se pueden limpiar salidas pesadas; para la entrega se
conservarán deliberadamente las evidencias, tablas y figuras requeridas.
