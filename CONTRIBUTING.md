# Colaboración entre tres personas

El plan, las dependencias y el trabajo en curso están en
[JOURNAL.md](JOURNAL.md). P1, P2 y P3 son etiquetas provisionales:
reemplazarlas por los nombres del equipo al iniciar.

Las tres personas desarrollan **en paralelo, cada una en su rama**, sobre el
notebook único. Para que eso funcione:

- cada persona edita solo las celdas de las secciones a su cargo (tabla de
  secciones del journal);
- el notebook se versiona sin salidas, de modo que los cambios en Git sean
  solo código y Markdown;
- la integración en `main` se hace de una persona a la vez.

## Preparar el clon (una vez por persona)

Con el entorno del proyecto activado (ver `README.md`):

```sh
python -m pip install -r requirements.txt
nbstripout --install
nbdime config-git --enable
```

- **nbstripout** borra salidas y contadores de ejecución del notebook al
  hacer `git add`. El archivo local conserva las salidas; Git no las recibe.
- **nbdime** permite ver diferencias y resolver conflictos del notebook por
  celdas en lugar de editar el JSON a mano (`nbdiff`, `nbmerge`,
  `git mergetool --tool nbdime`).

Ambas configuraciones son locales a cada clon y no se suben a Git. Comprobar
en T0 que funcionan en las tres máquinas.

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

3. **Trabajar** solo debajo de los encabezados propios del notebook. Hacer
   commits pequeños y, si se desea respaldo, `git push -u origin <rama>`.
   No mover ni editar celdas de otras secciones; si hace falta un cambio en
   un contrato o en la configuración común, acordarlo primero con el equipo.
4. **Actualizar con `main`** antes de integrar, para incorporar lo que otros
   ya integraron:

   ```sh
   git fetch origin
   git merge origin/main
   ```

   Resolver conflictos del notebook con nbdime. Luego reiniciar el kernel y
   ejecutar el notebook de principio a fin; si se acordó un modo de ejecución
   reducida, puede usarse aquí, pero no en T8. Revisar con `git diff` que no
   se suban salidas.
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
  kernel limpio con los valores del enunciado. Para conservar esas salidas en
  `main`, agregar `"keep_output": true` a los metadatos del notebook antes
  del commit final (nbstripout respeta esa marca). Comprobar en T0 que el
  mecanismo funciona con la versión instalada.
- Las figuras y tablas de `results/` se exportan desde esa misma ejecución.

## Antes de integrar

- Notebook único, celdas propias en su sección y pruebas relevantes ejecutadas.
- Rama actualizada con `main` y notebook ejecutado de principio a fin.
- Sin salidas en el diff del notebook (salvo el commit final de T8).
- Dependencias nuevas anotadas en `requirements.txt` y semillas registradas.
- Datos locales fuera de Git; figuras y tablas compartidas solo si son útiles.
- Journal actualizado con lo hecho, lo pendiente y las decisiones adoptadas.
