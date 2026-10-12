# IA generativa, empleo y carreras en Bogotá

Visor interactivo de los resultados de la Parte II del estudio «La IA y el futuro de la educación terciaria en Bogotá», elaborado para la Agencia Atenea.

Qué parte del empleo de Bogotá está expuesta a la IA generativa, en qué oficios la persona sigue siendo necesaria y qué hacer con cada carrera de pregrado. Datos: GEIH 2025 (DANE), SNIES 2025 (MEN), índice de exposición de la OIT (2025), índice de complementariedad del FMI (2023) calculado con O*NET.

## Contenido

| Archivo | Qué es |
|---|---|
| `index.html` | El visor completo: una sola página, con los datos incluidos. No necesita servidor ni librerías externas. |
| `fuentes/` | Tipografías IBM Plex Sans y Source Serif 4 (licencia SIL Open Font License). |
| `datos/` | Los datos de cada visualización en CSV (UTF-8), el diccionario de carreras y un ZIP con todo. |

## Publicar en GitHub Pages

1. En GitHub, cree un repositorio público nuevo (por ejemplo, `visor-ia-bogota`).
2. Suba todo el contenido de esta carpeta a la raíz del repositorio (botón **Add file → Upload files**, arrastre los archivos y carpetas, y luego **Commit changes**). Incluya el archivo oculto `.nojekyll`.
3. Vaya a **Settings → Pages**. En **Source** elija **Deploy from a branch**, rama `main`, carpeta `/ (root)`, y guarde.
4. Al cabo de uno o dos minutos el visor queda en `https://<usuario>.github.io/visor-ia-bogota/`.

Cada pestaña tiene su propia dirección (por ejemplo `…/#carreras` o `…/#buscar`), útil para enlazar desde un informe o una presentación.

## Insertarlo en el sitio de la Agencia Atenea

Con un `iframe`. El parámetro `?embed=1` reduce los márgenes, y el visor informa su altura a la página que lo contiene para que no aparezcan barras de desplazamiento:

```html
<iframe id="visor-ia" src="https://<usuario>.github.io/visor-ia-bogota/?embed=1"
        title="IA generativa, empleo y carreras en Bogotá"
        style="width:100%;border:0;min-height:900px" loading="lazy"></iframe>
<script>
  window.addEventListener("message", function (e) {
    if (e.data && e.data.visorIA === "altura") {
      document.getElementById("visor-ia").style.height = e.data.h + "px";
    }
  });
</script>
```

## Actualizar los datos

El visor se genera con `build.py` a partir de los resultados del proyecto de R (`resultados/flourish/` y `resultados/carreras_pregrado_2025_cuadrantes.csv`) y del archivo `etiquetas_carreras.csv` con los nombres cortos de las carreras. Para actualizarlo: correr el proyecto de R, correr `build.py` y volver a subir `index.html` y `datos/`.

## Notas de lectura

- Exposición no equivale a pérdida de empleo: indica tareas que la IA generativa podría transformar.
- Una «carrera» es un campo detallado de la CINE-F 2013 (A.C.), no un programa académico. Los nombres cortos son una ayuda de lectura; el nombre oficial y el código aparecen junto a cada carrera.
- Las cifras provienen de encuestas y no incluyen errores estándar. Las ocupaciones y carreras pequeñas son menos precisas.

Elaboración: Juan Sebastián Rodríguez León para la Agencia Atenea, octubre de 2026.
