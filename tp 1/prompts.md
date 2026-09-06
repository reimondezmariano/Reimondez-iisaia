# Prompts — TP 1

El registro del proceso, en orden. Tres prompts en una sola conversación de Gemini Canvas. El artefacto quedó terminado en el tercero.

---

## 1 — Prompt inicial

```
Construí un formulario de solicitud para el médico.

Estructura:
- <header> con el título "Formulario de solicitud para turno médico":
  
- Crear 3 contededores de interacción donde se puedan ingresar los datos del paciente. Un <input> que para nombre del paciente. Otro <input> que sea el apellido.
  Y un tercer <input> que tenga la fecha de nacimiento, con el formato correspondiente
- Una <section> que diga "Razones de la consulta", y debajo un contenedor <input> principal, que sea para rellenar con texto libre
- un <button> "Aceptar" y un  <button> "Cancelar".



Estilo:
- Estilo windows 3.1, en blanco y negro.
- El puntero debe tener un estilo acorde al windows 3.1. 2px o 3px de grosor


Comportamiento:

- El paciente tiene que rellenar los campos de forma acorde para poder clickear el botón aceptar.
- Al ingresar el apellido en el <input>, a medida que se tipea una letra, va aumentando en 2px el tamaño de la letra.
- Al ingresar el nombre en el <input>, a medida que se tipea una letra, las letras se muestran al revés, de forma espejada.
- Al ingresar la fecha por completa en el <input>, los valores se vuelven no visibles.

- Al escribir el texto libre en la <section> "Razones de la consulta", si no se llega a una cantidad de 100 caracteres, se devuelve un mensaje de error diciendo "Falta más información para su consulta".
- Al escribir el texto libre en la <section> "Razones de la consulta", si sobrepasa la cantidad de 120 caracteres, se devuelve un mensaje de error diciendo "Demasiada información. Dirijase urgente al médico".
- Si se sumplen las condiciones necesarias, es decir, todos los campos han sido llenados, se habilita la opción del <button> "Aceptar". Al posar el puntero por el <button> "Aceptar", se dispara un timer y si no sé se hace click antes de los 150ms, el botón aceptar se mueve de manera random en el espacio, y el <button> "Cancelar" agranda su tamaño en 10px en ancho, y 5px en alto.
- Clickear en el <button> "Cancelar" vuelve todo a la situación inicial
- Si el usuario hace click en el <button> "Aceptar" antes de que desaparezca, se tiene el siguiente error "Turnos onlines colapsados. Dirijase personalmente al sanatorio"

Constraints:
- Un solo archivo HTML, con el CSS en un <style> y el JS en un <script>.
- Vanilla JS, sin frameworks ni dependencias externas.

**Qué intentaba lograr:** el artefacto entero de una sola vez.

**Qué devolvió:** el tablero funcionando, respetando lo pedido. Todos los inputs y los botones funcionan como corresponde.

**Qué hice con eso:** lo acepté. Pero creo que puedo mejorar/empeorar un par de features del artefacto. e".

---


## 2 — iteración

Quiero hacer unos cambios:
-el <button> Cancelar se debe hacer aún vez más grande cada vez, y que se vaya solapando con el resto de la interfaz, 30px en ancho, y 15px en alto. También tiene que ir creciendo el tamaño del texto acorde.
-el <button>  Aceptar se debe ir haciendo cada vez más pequeño. 10px en ancho, 5px en alto
-Tocar la "X", como boton de salida, hace que el sistema de un Mensaje de éxito diciendo "Turno reservado exitosamente"
-la cantidad de caracteres en el <input> razones de la consulta debe ser mayor a 1000, pero menor a 1002


**Qué intentaba lograr:** mejorar/empeorar la UI con un par de detalles

**Qué devolvió:** ahora no funciona lo de la fecha de nacimiento. No se hace transparente. El boton cancelar no se solapa con el resto de la UI. 

**Qué hice con eso:** Voy a remarcar lo de la fecha de nacimiento, para que vuelva a funcionar. Lo del botón cancelar voy a intentar de re-escribirlo de forma distinta.


## 3- Iteracion

-La fecha de nacimiento una vez ingresada debe desaparecer, como estaba en la primera versión.
-El <button> "cancelar" debe aumentar su tamaño y solapar el resto de los componentes. La idea es que los bloquee y los tape de forma que no se pueda usar nada más que el botón cancelar.
-El texto ingresado en <input> apellido tiene que crecer 5px por letra ingresada

**Qué intentaba lograr:** hacerle un fine tuning y dejarla listo

**Qué devolvió:** devolvió lo que deseaba

**Qué hice con eso:** Aceptado, fue lo esperado


---

## Conversación completa

Una sola conversación de Gemini Canvas, sin reiniciar el hilo. El artefacto final tiene 468 líneas en un archivo.