# Prompts — TP 2 (API de recetas e ingredientes)

El registro del proceso, en orden. Herramienta: Claude.
Algunos de los prompts fueron realizados con la ayuda de la herramienta Promptmaster. También el brainstorming para comenzar con el TP se hizo con Claude.

---

## 1 — Prompt inicial

```
Necesito un openapi.yaml para una API de recetas e ingredientes.
Un ingrediente pertenece a una receta y no existe fuera de ella.

Recursos:
  Recipe      { id, name, servings?, prep_time_minutes? }
  Ingredient  { id, recipe_id, name, quantity, unit? }

Endpoints:
  GET    /recipes                              → 200 lista
  POST   /recipes                              → 201 / 400 si falta name
  GET    /recipes/{recipeId}/ingredients       → 200 lista / 404 si la receta no existe
  POST   /recipes/{recipeId}/ingredients       → 201 / 400 si falta name o quantity / 404 si la receta no existe

Reglas:
- Schemas de entrada y de salida separados (RecipeInput/Recipe, IngredientInput/Ingredient).
  El id y el recipe_id los asigna el servidor, así que no van en los schemas de entrada.
- quantity es number; unit es string opcional.
- Los ids de path son integer.
- Cada respuesta de error lleva un description claro.
```

**Qué buscaba:** fijar los cuatro endpoints, los tipos y la separación entre schema de entrada y de salida, dejando `recipe_id` fuera de la entrada porque ya viene en el path.

**Resultado:** el yaml salió con los cuatro endpoints y los códigos pedidos, y validó en editor.swagger.io.

---

## 2 — GET y DELETE de una receta

```
Agregá el path /recipes/{recipeId} con dos operaciones:
- GET: devuelve 200 con la receta (schema Recipe) o 404 si no existe.
- DELETE: devuelve 204 sin cuerpo si borró, o 404 si la receta no existe.
  Borrar una receta borra también todos sus ingredientes; aclaralo en el description.
No modifiques nada de lo existente.
```

**Qué buscaba (prompt 2):** sumar el path de un ítem individual y el borrado. Pedí `204` explícito y que el cascade quede escrito en el contrato, porque es la consecuencia de que el ingrediente dependa de la receta.

---

## 3 — Borrar un ingrediente

```
Agregá DELETE /recipes/{recipeId}/ingredients/{ingredientId}, que devuelva
204 sin cuerpo si borró y 404 si la receta o el ingrediente no existen.
No modifiques nada de lo existente.
```

**Qué buscaba:** completar el borrado a nivel ingrediente. Pedí `204` explícito y que el `404` cubra los dos casos (receta inexistente o ingrediente inexistente), porque el path tiene dos ids y cualquiera puede fallar.

---

## 4 — Validaciones

```
En RecipeInput e IngredientInput, agregá minLength: 1 al campo name.
En IngredientInput, quantity tiene que ser mayor que 0 (exclusiveMinimum: 0).
Aplicalo solo a los schemas de entrada; no toques los de salida ni nada más.
```

**Qué buscaba:** que un nombre vacío o una cantidad de cero o negativa no pasen la validación. Hasta el prompt 3, `""` era un `name` válido, y una cantidad de `-3` también. Lo limité a los schemas de entrada porque lo que devuelve el servidor ya pasó por esa validación.
