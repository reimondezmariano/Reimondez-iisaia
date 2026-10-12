# TP 2 — API de recetas e ingredientes

Un `openapi.yaml` que describe una API donde cada receta agrupa ingredientes y un ingrediente no existe fuera de una receta. Siete operaciones, cuatro paths, sin nada implementado: el entregable es el contrato.

## Cómo se lee

Pegar el contenido de [openapi.yaml](openapi.yaml) en [editor.swagger.io](https://editor.swagger.io). Aparece la documentación navegable del lado derecho, con cada endpoint desplegable.

## Qué me propuse construir

Una API para guardar recetas y los ingredientes de cada una. Elegí este dominio porque la relación es de pertenencia real: un "2 huevos" suelto, sin receta, no significa nada. Eso justifica anidar los paths en vez de usar un recurso plano con filtro.

## Endpoints

| Método | Path | Respuestas |
|--------|------|------------|
| GET | `/recipes` | 200 |
| POST | `/recipes` | 201, 400 |
| GET | `/recipes/{recipeId}` | 200, 404 |
| DELETE | `/recipes/{recipeId}` | 204, 404 |
| GET | `/recipes/{recipeId}/ingredients` | 200, 404 |
| POST | `/recipes/{recipeId}/ingredients` | 201, 400, 404 |
| DELETE | `/recipes/{recipeId}/ingredients/{ingredientId}` | 204, 404 |

## Decisiones que tomé yo

**Anidar `ingredients` dentro de `recipes`.** Un ingrediente depende de su receta, así que el path lo refleja: `/recipes/4/ingredients`. Si hubiera querido ingredientes compartidos entre recetas, la forma correcta era un path plano.

**Borrar una receta borra sus ingredientes.** Es la consecuencia de la pertenencia, y lo dejé escrito en el `description` del `DELETE` para que no quede librado a la implementación.

**Schemas de entrada y de salida separados.** `Ingredient` tiene `id` y `recipe_id`, que asigna el servidor. `IngredientInput` no los tiene: el `recipe_id` ya viaja en el path y no se repite en el body.

**`204` sin cuerpo en los borrados.** Si el recurso ya no existe, devolverlo en la respuesta no tiene sentido.

**`404` en el `GET` de ingredientes, no lista vacía.** Una receta que no existe y una receta sin ingredientes son situaciones distintas y merecen respuestas distintas.

**`quantity` numérico y `unit` opcional.** Un número permite escalar porciones; la unidad es opcional porque "2 huevos" no lleva ninguna.

**Validaciones en la entrada.** `name` no puede ser vacío y `quantity` tiene que ser mayor que 0.

## Qué salió mal y cómo lo corregí


El contrato que salió del prompt 1 cumplía lo pedido pero tenía un hueco: yo había escrito que `name` y `quantity` eran obligatorios, y el modelo los marcó como `required`, pero no dije nada sobre sus valores. Con ese contrato, un `name` vacío (`""`) o una `quantity` de `-3` eran válidos.

No era un error del modelo, era un error del prompt: pedí que el campo exista y no qué valores acepta. En el prompt 4 agregué `minLength: 1` a los nombres y `exclusiveMinimum: 0` a la cantidad, solo en los schemas de entrada.

La regla que me llevo: "obligatorio" y "válido" no son lo mismo, y el modelo solo resuelve lo que le pido.

Los prompts siempre dieron resultados sin errores. En ese sentido Claude interpreto lo que se pedía y supo resolver.

## Prompts

El registro completo está en [prompts.md](prompts.md). El primero fija los cuatro endpoints iniciales y la separación entre schemas de entrada y de salida; el cuarto es la corrección de validaciones.
