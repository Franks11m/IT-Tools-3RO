```
"href" : "http://www.youtypeitwepostit.com/api/",
"items" : [
{ "href" : "http://www.youtypeitwepostit.com/api/messages/21818525390699506",
"data": [
{ "name": "text", "value": "Prueba." },
{ "name": "date_posted", "value": "2013-04-22T05:33:58.930Z" }
],
"links": []
},
...
}
```
Mira el documento en su totalidad, y el propósito de todas estas restricciones se vuelve claro.
Collection+JSON es una forma de servir listas, pero no listas de estructuras de datos, que puedes
hacer con JSON normal, sino listas que describen recursos HTTP.
El objeto collection tiene una propiedad `href`, y su valor es una cadena JSON. Pero no es
cualquier cadena, es la URL a la que acabo de enviar una solicitud GET:
```
{ "collection":
{
"href" : "http://www.youtypeitwepostit.com/api/"
}
}
```
El estándar de Collection+JSON define esta cadena como "la dirección utilizada para recuperar una
representación del documento" (en otras palabras, es la URL del recurso de la colección). Cada objeto dentro de la lista de `items` de la colección tiene su propia propiedad `href`, y cada
valor es una cadena que contiene una URL, como http://www.youtypeitwepostit.com/api/messages/
21818525390699506 (en otras palabras, cada elemento de la lista representa un recurso HTTP
con su propia URL).
Un documento que no sigue estas reglas no es un documento Collection+JSON: es solo
un JSON cualquiera. Al permitirte estar atado por las restricciones de Collection+JSON,
obtienes la capacidad de hablar sobre conceptos como recursos y URLs. Estos conceptos no están
definidos en JSON, que solo puede hablar de cosas simples como cadenas y listas.

## Escribir en una API

<img src="Capturas/Captura de pantalla 2024-10-15 220354.png" alt="drawing" width="350"/>

¿Cómo usaría la API para publicar un mensaje en el microblog? Esto es lo que dice la especificación de Collection+JSON:

> Para crear un nuevo elemento en la colección, el cliente primero utiliza el objeto `template` para componer
una representación válida del elemento y luego utiliza HTTP POST para enviar esa representación al
servidor para su procesamiento.

Eso no es exactamente una descripción paso a paso, pero apunta hacia la respuesta. Collection
+JSON funciona de manera similar a HTML. El servidor te proporciona alguna clase de
