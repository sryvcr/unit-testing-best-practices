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

## Consideraciones para escribir unit test:
- Se debe ser muy cuidadoso con los casos de prueba de una unidad de código:
    - Probar casos de funcionamiento correcto.
    - Probar los casos "al límite", es decir, si la función recibe un entero positivo de 32 bit, tal vez se deban incluir pruebas con el entero máximo que se puede guardar en 32 bits o con un entero negativo.
    - Probar casos con valores erroneos o no esperados, es decir, si la funcion espera un string, tal vez se deban incluir pruebas enviando un booleano u otro tipo de dato diferente.
    - Probar casos de distintos fallos o lanzamiento de excepciones.
- Al momento de encontrar un bug en el código, se recomienda escribir una prueba para reproducirlo antes de arreglarlo. De esta forma se puede asegurar que una vez resuelto, funcionará el test y este caso estará cubierto.
