# Unit Testing, Mejores Prácticas
---

## Qué son las pruebas unitarias:
Permiten comprobar el correcto funcionamiento de una unidad de código. Por ejemplo, en *programación funcional* una *función* o en *programación orientada a objetos* una *clase*. El propósito de este tipo de pruebas es garantizar que cada componente se comporte adecuadamente, es decir, funciona como debe funcionar, responde como debe responder, falla cuándo y cómo debe de fallar y acepta lo que tiene que aceptar. Ademas esta práctica permite seguir desarrollando de manera ágil en el largo plazo.

## Elementos principales de una prueba unitaria:
- Conjunto de entradas a probar
- Unidad de trabajo a probar
- Conjunto de salidas esperadas en la unidad probada de acuerdo a las entradas

## Características de una buena prueba unitaria:
- *Rápida*: las pruebas unitarias deben tomar poco tiempo en ejecutarse. Si es demorada la ejecución puede haber una mala optimización en el test.
- *Aisladas*: pueden correr de forma independiente y no necesitan de factores externos (librerías, clases, otros test… etc) ni la ejecución previa de otros test para funcionar. Cuando una prueba depende de algo externo es necesario "fingir" o engañar a la prueba unitaria a traves de un **mock**.
- *Repetible*: una prueba unitaria siempre devuelve el mismo resultado si no cambia nada entre las ejecuciones, si esto no pasa, quiere decir el test no es confiable y se debe revisar el código testeado y/o la prueba.
- *Auto chequable*: la prueba debería ser capaz de detectar automáticamente si pasó o falló, sin interacción humana, además de esto, debe dar retroalimentación en caso de fallar.
