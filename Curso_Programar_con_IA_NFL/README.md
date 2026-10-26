# Programar con criterio en la era de la IA

Curso introductorio de cinco sesiones de 90 minutos, en R Markdown, para personas que nunca han programado. El hilo conductor es un caso de *scouting*: un equipo de la NFL necesita que sus analistas comparen prospectos del **NFL Scouting Combine** con resultados útiles, reproducibles y defendibles.

El curso no busca que los estudiantes memoricen comandos ni que dependan de una IA para programar. Busca que desarrollen el criterio para trabajar con código, lo escriban ellos o lo genere una herramienta: leerlo, identificar las decisiones que contiene, comprobar si calcula lo que creen y explicar qué se puede concluir. Ese mensaje no se predica: aparece en ejercicios con datos reales en los que un código que funciona, bien presentado, responde otra pregunta.

## Contenido de la carpeta

```
Curso_Programar_con_IA_NFL/
├── README.md                              <- este archivo
├── Sesion_1_Primeros_pasos.Rmd
├── Sesion_2_Explorar_y_filtrar.Rmd
├── Sesion_3_Transformar_y_resumir.Rmd
├── Sesion_4_Visualizar_y_comparar.Rmd
├── Sesion_5_Proyecto_de_scouting.Rmd
├── Curso_Programar_con_IA_NFL.zip         <- todo lo anterior, en un solo archivo
└── datos/
    └── NFL.csv
```

Cada `.Rmd` es **autocontenido**: carga sus propios datos, crea todas las variables que usa y no depende de objetos de sesiones anteriores. Incluye contexto, explicaciones, código ejecutable, ejercicios y soluciones.

## Las cinco sesiones

| Sesión | Pregunta guía | Programación | Criterio | Momento central (con datos reales) |
|--------|---------------|--------------|----------|------------------------------------|
| 1. El código no es magia | ¿Qué tenemos realmente en nuestros datos sobre los jugadores? | R y RStudio, objetos y `<-`, vectores, tablas, `read.csv()`, `head()`, `dim()`, `names()`, `str()`, `summary()`, `table()` | Ejecutar sin entender es aceptar un resultado sin saber de dónde viene | Una solución "de IA" para el peso promedio usa `na.omit()`: elimina 2,298 de 3,477 filas, entre ellas a **todos** los no elegidos, y reporta 249.5 lb en lugar de 241.9 |
| 2. La IA también decide qué datos vemos | ¿Cómo cambia nuestra conclusión cuando elegimos qué jugadores incluir? | Comparaciones y operadores lógicos, `NA` e `is.na()`, `filter()`, `select()`, `arrange()`, `%>%` | Filtrar determina de quién hablamos | Dos selecciones de "receptores rápidos" dan 85% y 86% de elegidos con definiciones distintas (la de la IA incluye 32 corredores); los corchetes producen 26 filas fantasma sin error |
| 3. Un resultado depende de cómo lo construimos | ¿Qué estamos midiendo cuando comparamos a dos grupos de jugadores? | `mutate()`, `case_when()`, `grepl()`, `ifelse()`, `group_by()`, `summarise()`, media, mediana, conteos, `na.rm` | Una definición distinta puede invertir una conclusión | Press de banca: con `na.rm = TRUE` la primera ronda es la más fuerte (22.3 rep.); rellenando faltantes con 0, queda segunda (15.2 frente a 16.2). Un Speed Score calculado en kilos da una mediana de 45 en lugar de ~100 |
| 4. Que una gráfica se vea bien no significa que esté bien | ¿Cómo sabemos si una visualización representa correctamente los datos? | `ggplot2`: barras, histogramas, dispersión, `labs()`, `facet_wrap()`, `cor()` | Ejes, escalas, omisiones y asociación frente a causalidad | Una gráfica "de IA" rotula como "Velocidad" un eje de tiempos y, con el eje cortado, convierte una diferencia del 1.4% en una del doble; la correlación peso-tiempo (0.85) casi desaparece dentro de cada posición |
| 5. Ser responsable de un análisis, aunque la IA escriba el código | ¿Podemos presentar una recomendación de scouting que podamos explicar y defender? | Integración de todo lo anterior | Verificar, documentar y defender | Mini proyecto con plantilla, rúbrica, tabla de cambios, registro de uso de IA, preguntas de defensa individual y un ejemplo resuelto |

Cada sesión sigue aproximadamente esta distribución: problema de scouting (0–10 min), concepto y decisión analítica asociada (10–25), ejemplo guiado (25–45), práctica acompañada con o sin IA (45–65), ejercicio individual de modificación o verificación (65–80) e interpretación y cierre (80–90). Los tiempos de cada archivo están ajustados a su contenido.

### La rutina de trabajo

Las actividades siguen, sin presentarla como método, una secuencia que en la sesión 5 se hace explícita: **definir** el problema, **anticipar** el resultado, **construir** el código (propio o de una IA), **leerlo**, **comprobarlo**, **comparar** con otra decisión razonable, **documentar** los cambios y **comunicar** conclusiones y límites. La autonomía aumenta de sesión en sesión: en la 1 casi todo está guiado; en la 5 el estudiante hace todo el recorrido.

## Requisitos

- **R** 4.1 o posterior (se usó 4.3.3) y **RStudio Desktop**.
- Paquetes: `dplyr` y `ggplot2` (sesiones 2 a 5) y `rmarkdown` (para compilar). La sesión 1 solo usa R base.

Instalación, una sola vez, desde la consola de RStudio:

```r
install.packages(c("dplyr", "ggplot2", "rmarkdown"))
```

Una vez instalados los paquetes y con `datos/NFL.csv` en su sitio, **no se necesita internet durante la clase**. Los archivos no instalan nada por su cuenta: si falta un paquete, se detienen con un mensaje que dice cómo instalarlo.

## Cómo usar los materiales

1. Descarga o copia la carpeta completa (o descomprime el ZIP). Lo importante es que `datos/` quede junto a los `.Rmd`.
2. Abre el `.Rmd` de la sesión en RStudio. Los bloques de código se ejecutan con `Ctrl + Enter` (línea) o con el triángulo verde (bloque completo); RStudio los ejecuta desde la carpeta del documento, así que la ruta relativa `datos/NFL.csv` funciona.
3. Para generar el HTML, botón **Knit**.

### Soluciones visibles u ocultas

Cada archivo tiene un parámetro `soluciones` en el encabezado YAML:

- `soluciones: true` (por defecto): las soluciones aparecen **plegadas** en recuadros "Ver solución", debajo de cada ejercicio. Es la versión para repasar por cuenta propia.
- `soluciones: false`: las soluciones desaparecen por completo del HTML (no solo se ocultan). Es la versión para repartir en clase.

Para generar la versión sin soluciones: en RStudio, **Knit ▸ Knit with Parameters…** y desmarca `soluciones`; o desde la consola:

```r
rmarkdown::render("Sesion_1_Primeros_pasos.Rmd", params = list(soluciones = FALSE),
                  output_file = "Sesion_1_Primeros_pasos_sin_soluciones.html")
```

## Los datos: `NFL.csv`

- **Fuente:** conjunto *NFL Combine - Performance Data (2009 - 2019)*, publicado en Kaggle por el usuario *redlineracer* (https://www.kaggle.com/datasets/redlineracer/nfl-combine-performance-data-2009-2019), que es el que usa el cuaderno de referencia https://www.kaggle.com/code/redlineracer/nfl-scouting-combine. Según su descripción, los datos se descargaron de Pro Football Reference.
- **Licencia:** CC0 (dominio público), según la ficha del conjunto en Kaggle. Por eso se incluye una copia en `datos/`.
- **Si necesitas descargarlo de nuevo:** en la página del conjunto en Kaggle, botón *Download* (puede requerir una cuenta gratuita). Descomprime el archivo y coloca `NFL.csv` dentro de `datos/`, sin cambiarle el nombre.
- **Versión usada:** 3,477 filas y 18 columnas. MD5 `4f1c61b185b57703a8e175776cc49d93`; SHA-256 `a61ff78b87f46c0d94a1d24c78588da31d7bdb83d23cb18c8a8299cc0b273e23`. Para comprobarlo en R: `tools::md5sum("datos/NFL.csv")`. Cada sesión avisa si el archivo no tiene esas dimensiones.

### Diccionario de variables

El archivo **no documenta las unidades**. Las de esta tabla se dedujeron de los rangos y se comprobaron cuando fue posible (se indica cómo).

| Columna | Tipo en R | Contenido | Unidades | Faltantes |
|---------|-----------|-----------|----------|-----------|
| `Year` | entero | Año del Combine, 2009 a 2019 | — | 0 |
| `Player` | texto | Nombre. En 3,073 filas va seguido de `\` y un código (p. ej. `Beanie Wells\WellCh00`) | — | 0 |
| `Age` | entero | Edad, de 18 a 28 | años | 550 (539 son no elegidos) |
| `School` | texto | Universidad (253 distintas) | — | 0 |
| `Height` | numérico | Estatura | metros. Todos los valores son múltiplos exactos de 2.54 cm: se midió en pulgadas enteras (18 valores distintos) | 0 |
| `Weight` | numérico | Peso | kilogramos. Al convertirlos a libras salen enteros: se midió en libras | 0 |
| `Sprint_40yd` | numérico | Carrera de 40 yardas | segundos (menos es más rápido) | 174 (160 de ellos en 2017–2019) |
| `Vertical_Jump` | numérico | Salto vertical | centímetros (múltiplos de media pulgada) | 697 |
| `Bench_Press_Reps` | entero | Repeticiones en press de banca con 225 lb | repeticiones (mínimo 2, no hay ceros) | 905 |
| `Broad_Jump` | numérico | Salto largo | centímetros (múltiplos de una pulgada) | 728 |
| `Agility_3cone` | numérico | Prueba de tres conos | segundos | 1,217 |
| `Shuttle` | numérico | Prueba *shuttle* | segundos | 1,140 |
| `Drafted..tm.rnd.yr.` | texto | Equipo / ronda / número de selección / año del draft | — | 1,223 (exactamente los no elegidos) |
| `BMI` | numérico | Índice de masa corporal. Coincide con `Weight / Height^2` | kg/m² | 0 |
| `Player_Type` | texto | `offense`, `defense`, `special_teams` | — | 0 |
| `Position_Type` | texto | 7 grupos de posiciones (p. ej. `backs_receivers`, que reúne QB, RB, WR, TE y FB) | — | 0 |
| `Position` | texto | 20 posiciones (WR, CB, RB, OT, DT...) | — | 0 |
| `Drafted` | texto | `Yes` / `No` | — | 0 |

### Hechos verificados que usan los materiales

- 2,254 jugadores elegidos y 1,223 no elegidos. `Drafted..tm.rnd.yr.` falta exactamente cuando `Drafted == "No"`, y el año del texto coincide con `Year` en todas las filas.
- Entre 2009 y 2017 hay entre 322 y 333 jugadores por año; 2018 tiene 308 y 2019 solo 220.
- La primera ronda (identificada con el patrón `"/ 1st /"`) nunca supera 32 jugadores por año; 2019 tiene 14. Buscar solo `"1st"` clasificaría mal a 168 jugadores elegidos en otras rondas (por ejemplo, la selección 121).
- `na.omit()` aplicado a la tabla completa deja 1,179 filas, todas de jugadores elegidos.
- El nombre no identifica de forma única a un jugador: hay cuatro "Chris Jones" distintos (dos sin código).

### Aspectos que el archivo no permite verificar

Los materiales los presentan como preguntas abiertas, no como hechos:

- Por qué faltan los resultados de las pruebas (si el jugador no la hizo, se lesionó o no se registró), y por qué los tiempos de 40 yardas faltantes se concentran en 2017–2019.
- Si 2018 y, sobre todo, 2019 están completos respecto a los participantes reales del Combine.
- Qué edad registra `Age` (¿al Combine?, ¿al draft?). Que casi todos los faltantes sean de no elegidos es compatible con que provenga de los registros del draft, pero no lo confirma.
- Qué es exactamente el código que acompaña a algunos nombres (parece un identificador de Pro Football Reference).
- Si el tiempo de 6.00 segundos en 40 yardas (un guardia ofensivo de 2011) es real o un error de captura.

## La IA en el curso

- **Ninguna actividad requiere IA**, y ninguna la prohíbe. Cada actividad con IA tiene una alternativa equivalente sin ella.
- Las "propuestas de un asistente de IA" que aparecen en las sesiones 1 a 4 son **respuestas representativas redactadas para el curso**, del tipo que suelen devolver estas herramientas ante la petición indicada. Están fijadas en el documento para que todos trabajen con el mismo material, tengan o no acceso a una IA y aunque las herramientas cambien. No son transcripciones de una herramienta concreta, y sus "errores" no son artificiales: son decisiones plausibles (eliminar faltantes, rellenarlos con ceros, interpretar un nombre de columna, cortar un eje) que producen código que funciona.
- Quien tenga acceso a una IA encontrará en cada sesión peticiones concretas para probar, con la indicación de verificar también las explicaciones que dé la herramienta.

## Control de cambios y reproducibilidad

Sin convertirlo en un curso de Git: desde la sesión 1 los estudiantes guardan una versión funcional antes de modificar (`_v1`, `_v2`...) y llevan una **bitácora** breve (qué cambié, por qué, si cambió el resultado). En la sesión 5 entregan una **tabla de cambios** y un **registro de uso de IA**. La reproducibilidad se trabaja con rutas relativas, archivos que compilan de principio a fin y cifras que se pueden rastrear hasta su código. Quien ya use Git puede sustituir las copias numeradas por *commits* con mensajes descriptivos.

## Evaluación

Formativa y basada en la comprensión, no en la cantidad de código. La rúbrica de la sesión 5 tiene siete criterios (comprensión del código, decisiones y supuestos, verificación, interpretación, justificación de cambios, reproducibilidad y comunicación) en tres niveles, y se acompaña de ocho preguntas para una defensa individual breve con el archivo abierto. **Usar IA no resta ni suma puntos**: se evalúa si el estudiante entiende, verifica y justifica lo que presenta.

## Notas para quien imparte el curso

- **Sesión 1.** El tropiezo más común es que R no encuentre el archivo: casi siempre es una carpeta mal nombrada o una consola en otra carpeta. El bloque `file.exists("datos/NFL.csv")` existe para diagnosticarlo antes de importar. La primera vez que se hace Knit, RStudio puede pedir instalar paquetes; conviene hacerlo antes de clase.
- **Sesión 2.** Dedicar tiempo a que `NA < 4.4` dé `NA` y a la técnica de "hacer que las cuentas cuadren"; es la comprobación que más se reutiliza después.
- **Sesión 3.** El orden de las condiciones en `case_when()` y la diferencia entre "no hizo la prueba" y "levantó cero veces" son los dos puntos que más discusión generan. Si el grupo va lento, el ejercicio 3 es opcional.
- **Sesión 4.** El error de usar `%>%` en lugar de `+` aparece siempre; está mostrado a propósito. Pedir que lean los avisos de `ggplot2` en voz alta.
- **Sesión 5.** Conviene aprobar las preguntas propias en los primeros diez minutos y empujar hacia preguntas pequeñas. Si no hay tiempo para defensas individuales, se pueden hacer en parejas con la lista de preguntas; el ejemplo resuelto está pensado para revisarse después de clase.

## Verificación de los materiales

Los cinco archivos se compilaron a HTML sin errores con R 4.3.3, `dplyr` 1.1.4, `ggplot2` 3.4.4, `knitr` 1.45 y `rmarkdown` 2.25, tanto con `soluciones: true` como con `soluciones: false`, y las cifras citadas en el texto se contrastaron con la salida de R. Con versiones más recientes de los paquetes, algunos mensajes de aviso o de error pueden estar redactados de otra forma y las tablas pueden imprimirse con distinto número de decimales; las cifras no deberían cambiar si se usa la misma versión de `NFL.csv`.
