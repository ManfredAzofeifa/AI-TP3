# Colaboración entre tres personas

El plan, las dependencias y el trabajo en curso están en
[JOURNAL.md](JOURNAL.md). Las etiquetas P1, P2 y P3 (tabla «Equipo» del
journal) se usan en las tareas y en los nombres de las ramas.

Las tres personas desarrollan **en paralelo, cada una en su rama**, sobre el
notebook único. Para que eso funcione:

- cada persona edita solo las celdas de las secciones a su cargo (tabla de
  secciones del journal);
- el notebook se versiona sin salidas (se limpian en PyCharm antes de cada
  commit), de modo que los cambios en Git sean solo código y Markdown;
- la integración en `main` se hace de una persona a la vez.

## Preparar el clon (una vez por persona)

Crear el entorno con Python 3.15.0 según `README.md` (instala las versiones
exactas de `requirements.txt`) y, con el entorno activado:

```sh
nbdime config-git --enable
```

- **nbdime** permite ver diferencias y resolver conflictos del notebook por
  celdas en lugar de editar el JSON a mano (`nbdiff`, `nbmerge`,
  `git mergetool --tool nbdime`). `.gitattributes` ya asocia los `.ipynb` con
  sus controladores; el comando registra esos controladores en el clon.
- **WSL:** clonar dentro del sistema de archivos de Linux (por ejemplo `~/`),
  no en `/mnt/c`, y usar solo el Git de WSL con ese clon.
- **Windows:** si el Control de aplicaciones bloquea las bibliotecas de SciPy,
  ejecutar en Linux las secciones que usan SciPy o `sklearn`.

No se usa nbstripout: renumera los identificadores de celda (`s4-3-pruebas`
pasa a ser `"14"`) y reescribe todo el archivo. Los identificadores marcan de
quién es cada celda, así que deben conservarse.

## PyCharm y el kernel del `.venv`

PyCharm es el editor del equipo. Su servidor de Jupyter administrado por el IDE
arranca el kernel con el intérprete del proyecto, así que **no hace falta
registrar ni crear kernels**: basta con que el intérprete del proyecto sea el
`.venv`.

1. Crear el `.venv` según `README.md` y abrir la carpeta del repositorio en
   PyCharm (*File › Open*).
2. Elegir el intérprete del proyecto. PyCharm suele detectar el `.venv` solo;
   si no, en *Settings › Project › Python Interpreter › Add Interpreter › Add
   Local Interpreter*, elegir el entorno existente:
   - Linux, macOS o WSL: `.venv/bin/python`. En WSL, con un intérprete de tipo
     WSL que apunte a esa ruta dentro de la distribución.
   - Windows: `.venv\Scripts\python.exe`.

   La barra de estado debe mostrar `.venv (3.15.0)`. La carpeta `.idea/` está
   ignorada por Git, así que esta configuración es de cada persona.
3. Abrir `notebooks/tp3_redes_neuronales.ipynb`. En la barra del notebook, el
   servidor debe ser **IDE-Managed Server (Auto)**. Dejarlo así: no ejecutar
   `ipykernel install`, no elegir otro kernel ni conectar un servidor externo.
   Así los metadatos del notebook (`kernelspec` `python3`) no cambian.
4. Ejecutar `s0-config`: debe imprimir Python 3.15.0, las versiones de
   `requirements.txt` y la raíz del repositorio.
5. Si se instala algo en el `.venv` o el kernel queda en mal estado,
   reiniciarlo desde la barra del notebook; sigue siendo el mismo intérprete.

**Antes de cada commit:** botón *Clear All Outputs* de la barra del notebook,
guardar (Cmd/Ctrl+S) y revisar `git diff`. Comprobado en T0 (macOS): ejecutar,
limpiar y guardar deja el diff vacío. PyCharm guarda `outputs` y
`execution_count` después de `source` en las celdas de código, y el
repositorio ya está en ese formato. Si el notebook se guarda con Jupyter Lab o
`nbconvert`, ese orden cambia en todas las celdas de código: no hacer commit de
un notebook guardado así.

## Flujo de una tarea

1. **Reservar.** Actualizar la tabla «Trabajo en curso» del journal en `main`
   con un commit pequeño (`git pull --ff-only` antes) y avisar al equipo.
2. **Crear la rama** desde el último `main`, con el formato
   `<persona>/<tarea>-<tema>`:

   ```sh
   git switch main
   git pull --ff-only
   git switch -c p2/t6-ece
   ```

3. **Trabajar** solo debajo de los encabezados propios del notebook. Antes de
   cada commit, en PyCharm: *Clear All Outputs*, guardar y revisar con
   `git diff` que el notebook solo cambia en código y Markdown. Hacer commits
   pequeños y, si se desea respaldo, `git push -u origin <rama>`.
   No mover ni editar celdas de otras secciones; si hace falta un cambio en
   un contrato o en la configuración común, acordarlo primero con el equipo.
4. **Actualizar con `main`** antes de integrar, para incorporar lo que otros
   ya integraron:

   ```sh
   git fetch origin
   git merge origin/main
   ```

   Resolver conflictos del notebook con nbdime. Luego reiniciar el kernel y
   ejecutar el notebook de principio a fin; aquí puede usarse la ejecución
   reducida (`TP3_QUICK=1`), pero no en T8. Limpiar las salidas y revisar con
   `git diff` que no se suban.
5. **Integrar** cuando nadie más esté integrando (avisar antes):

   ```sh
   git switch main
   git pull --ff-only
   git merge --no-ff p2/t6-ece
   git push origin main
   ```

   En la misma integración, actualizar el journal: casillas, trabajo en
   curso, verificaciones ejecutadas, decisiones y pendientes.
6. **Avisar** a quien dependa de la tarea (columna «Depende de» del journal).

Los pull requests son opcionales y sirven para la revisión sugerida. Si un PR
tiene conflictos en el notebook, resolverlos localmente con nbdime en la rama,
no en el editor web de GitHub.

Si `pull --ff-only` falla o `push` es rechazado, otra persona integró antes:
volver al paso 4 con la rama. No usar `push --force` en `main` ni resolver a
ciegas conflictos del JSON del notebook.

## Salidas del notebook y ejecución final

- Durante el desarrollo las salidas solo existen en la copia local de cada
  persona. Cada sección usa su propio generador aleatorio, creado con su
  semilla de la configuración común, y variables con prefijo de sección, para
  que sus resultados no dependan del orden o de lo que hagan otras secciones.
- En T8, con todas las tareas integradas, una persona ejecuta todo desde un
  kernel limpio, sin `TP3_QUICK`, con los valores del enunciado, y hace commit
  del notebook con esas salidas. Es el único commit con salidas.
- Las figuras y tablas de `results/` se exportan desde esa misma ejecución.
- El informe LaTeX se redacta después, en T9, con los resultados de T8.

## Antes de integrar

- Notebook único, celdas propias en su sección y pruebas relevantes ejecutadas.
- Rama actualizada con `main` y notebook ejecutado de principio a fin.
- Sin salidas en el diff del notebook (salvo el commit final de T8).
- Entorno igual a `requirements.txt`; cambiar una versión o agregar una
  biblioteca solo con acuerdo registrado en el journal. Semillas registradas.
- Datos locales fuera de Git; figuras y tablas compartidas solo si son útiles.
- Journal actualizado con lo hecho, lo pendiente y las decisiones adoptadas.
