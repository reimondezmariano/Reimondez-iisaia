# TP 1 — Turnos online

Un formulario para un turno médico en donde se debe llenar el formulario con nombre, apellido y fecha de nacimiento, así como también las razones de la consulta. Ingresar los datos es ultra incomodo y restrictivo.

## Cómo se ejecuta

Doble click en `turnos.html`. Un solo archivo, sin dependencias.

## Qué me propuse construir

Una UI con un estilo antiquísimo. Poco útil, la información que se va escribiendo termina siendo poco legible, y además tiene condiciones muy restrictivas para pedir un turno. Salió en tres prompts, en una sola conversación de Gemini Canvas.

## Decisiones que tomé yo

**Formato general** el formato general como si fuera un antiguo windows 3.1

**Botones** Como deberían funcionar los botones fue decidido estrictamente por mi parte.

**Contenedores** Los contenedores y como debén comportarse.

## Decisiones que tomó la IA

El posicionamiento de los botones y de los contendores fue decidida por la IA. No me pareció una mala decisión. Acepté lo propuesto.

## Qué salió mal y cómo lo corregí

Tuve un problema con el botón **Cancelar**. No se solapaba con el resto de la UI. Lo tuve que definir estrictamente en el segundo prompt

En el segundo prompt de iteración dejó de funcionar una de las caracteristicas del input de la fecha de nacimiento. No se convertía en no visible. Arreglado en el tercer prompt

Las reglas fueron entendidas de forma correcta.

No tuve que corregír yo mismo en las líneas de código del HTML. Podría haber hecho el "fine tuning" de algunas cosas, como el aumento del tamaño de las letras, o como deberían de cambiar de tamaño los botones.

## Prompts

El registro completo está en [prompts.md](prompts.md).
