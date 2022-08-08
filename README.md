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

## Mejores practicas pruebas unitarias:
- *Nomenclatura*: es muy importante asignar un nombre correcto para que cualquiera tenga contexto y pueda entender qué es lo que hace.
    - Colocar el nombre del método usado
    - Escenario que se está probando
    - Valor esperado

    ```python
    def test_single(): 💩
        pass
    ```
    ```python
    def test_single_number_returns_same_number(): ✅
        pass
    ```
- *Etapa de preparación*: se recomienda dividir en partes la prueba unitaria, primero instanciando los objetos necesarios, después configurar dichos objetos y añadirles el valor o dejarlos en el estado deseado para la prueba, y al final dejar las validaciones. Esto permite a nuestros test mayor limpieza en el código.
    - Organizar objetos (inicializarlos)
    - Acciones sobre los objetos
    - Comprobación sobre lo esperado
    ```python
    def test_add_empty_string_returns_zero(): 💩
        string_calculator = StringCalculator()
        assert string_calculator.add("") == 0
    ```
    ```python
    def test_add_empty_string_returns_zero(): ✅
        string_calculator = StringCalculator()
        actual = string_calculator.add("") 
        assert actual == 0
    ```
- *Separar cadenas de texto*: al validar campos es bueno separar las cadenas de texto de lo que se va a chequear para decir de forma explícita a qué hace referencia ese valor que vamos a probar; si en un futuro este valor cambia, solo cambia la línea de código donde se define.
    - Dar un significado a los inputs
    - Muestra lo que se está tratando de probar, no lo que se quiere lograr
    ```python
    def test_add_maximun_sum_result_raise_overflow_exception(): 💩
        string_calculator = StringCalculator()
        with pytest.raises(OverflowException):
            string_calculator.add("1001")
    ```
    ```python
    def test_add_maximun_sum_result_raise_overflow_exception(): ✅
        MAXIMUM_RESULT = "1001"
        string_calculator = StringCalculator()
        with pytest.raises(OverflowException):
            string_calculator.add(MAXIMUM_RESULT)
    ```
- *Evitar la lógica*: esto es un problema muy recurrente, generalmente se piensa que como se sigue programando se puede meter lógica y validar, hacer loops, o utilizar otro tipo de funciones. Esto no se debería hacer. Las pruebas unitarias deberían tener la mínima lógica posible. La prueba solo debe validar el resultado de una sola acción.
    ```python
    def test_add_multiple_numbers_returns_correct_result(): 💩
        string_calculator = StringCalculator()
        expected = 0
        test_cases = [
            "0,0,0",
            "0,1,2",
            "1,2,3",
        ]
        for test_case in test_cases:
            assert expected == string_calculator.add(test_case)
            expected += 3
    ```
    En el caso de python y pytest se puede parametrizar este test para evitar la lógica y repetirla con diferentes datos (esto se puede hacer en los demás lenguajes de programación y framework de testing)
    ```python
    @pytest.mark.parametrize(
        ("string_to_test", "expected"),
        (
            ("0,0,0", 3),
            ("0,1,2", 6),
            ("1,2,3", 9),
        )
    )
    def test_add_multiple_numbers_returns_correct_result(
        string_to_test,
        expected
    ): ✅
        string_calculator = StringCalculator()
        actual = string_calculator.add(string_to_test)
        assert actual == expected
    ```
