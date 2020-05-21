# Vulnerabilidades de ARM como MCU


![](https://tectijuana.edu.mx/wp-content/uploads/2014/11/Heading-Ing-sistemas-2048x672.png) 

**Debilidades en el procesador**
Los investigadores encontraron dos debilidades principales en los procesadores que podrían permitir a los atacantes leer información delicada que nunca debería abandonar la unidad de procesamiento central. Ambos problemas permiten a los atacantes leer información secreta que el procesador pone temporalmente a disposición fuera del chip.

Para que los procesos informáticos se ejecuten más rápido, un chip esencialmente adivinará qué información necesita la computadora para realizar su próxima función. Eso se llama ejecución especulativa. Como adivina, esa información sensible es momentáneamente más fácil de acceder.

**Meltdown y Spectre como vulnerabilidades en ARM**
**Meltdown**

La vulnerabilidad Meltdown surgió a raíz de que los CPU actuales pudieran ejecutar instrucciones fuera de orden. Se trata de una función muy cómoda que acelera el procesamiento de código, pero en algunos casos el CPU puede procesar código que es propenso a error, un código que no debería ejecutarse. Eso es, primero el CPU ejecuta el código y solo entonces se hace evidente que no se puede completar la acción, este tipo de situaciones suceden precisamente porque las instrucciones se han ejecutado fuera de orden.

Evidentemente, los resultados de estas operaciones no llegarán a ninguna parte, aunque dejarán rastros a nivel de microarquitectura, en la memoria caché del CPU, desde donde se podrían extraer. Como resultado, el caché se puede utilizar para recopilar datos que de otra forma serían inaccesibles: por ejemplo, una contraseña. Te contamos cómo funciona: un programa puede solicitar acceso a datos almacenados; el sistema, lógicamente, negará este acceso por falta de autorización. Pero, debido a la ejecución de operaciones fuera de orden, la contraseña acabará en el caché, desde donde es muy fácil de recopilar. En resumen, Meltdown podría tener lugar al intentar ejecutar una acción injustificada.

**Spectre**

La vulnerabilidad Spectre es similar a Meltdown, pero, aunque también está relacionada con la aceleración informática de la CPU, surge de la función de predicción de saltos de los CPU. Básicamente, un CPU es capaz de predecir estos saltos con cierto nivel de precisión, ya que la acción B suele ir precedida de la A. Por tanto, puede ejecutar la acción B antes de que se hayan esclarecido los resultados de A. Si la predicción ha sido correcta y la acción B sigue a la A, todo bien, y, si los resultados de A indican que el CPU debería de haber completado la acción con C, en lugar de B, el CPU abandonará el salto B y cambiará a otro en el que tenga que completar la acción C.

Como el predictor de saltos es inteligente, la mayoría de las veces recuerda el patrón de la acción, por lo que mejora el rendimiento del CPU (si B suele seguir a A, el CPU dará por hecho que en determinada situación tendrá que hacer B después de A). Pero se puede equivocar (a veces llega C en vez de B, aunque el predictor de saltos recuerda perfectamente que normalmente A va seguida de B).

Si acostumbras al sistema a que cierto salto es el correcto y siempre se ejecuta y luego cambias un parámetro para que se equivoque, el CPU lo ejecutará primero y luego lo revocará, después de descubrir que debería de haber ejecutado otro. Pero, al igual que con Meltdown, el resultado de la acción puede permanecer, por ejemplo, en el caché, desde donde se podría volver a extraer.

**Spectre 1** permite que una CPU sea engañada para cargar datos en un programa desde una dirección virtual de memoria ajena a los datos controlados por ese programa. Lo que hace, básicamente, es saltarse la verificación que hace que un programa no pueda acceder a ciertos datos por seguridad.

**Spectre v2**, una vulnerabilidad que consiste en engañar al sistema de predicción del procesador para que cargue datos externos en el BTB (Branch Target Buffer) seleccionados por el atacante. De esta manera se pueden leer datos directamente de los procesos que lo ejecuten, por ejemplo, contraseñas. Además, Spectre V2 permite que se pueda acceder a los datos de otros procesos ejecutados en el mismo hilo del procesador ya que el BTB (Branch Target Buffer) está compartido entre todos ellos.

Las consecuencias son casi las mismas: Spectre abre una trampilla para el acceso no autorizado de datos. Este acceso podría tener lugar solo en el caso de que la predicción de saltos saliera mal y, según la teoría de la probabilidad, pasaré tarde o temprano.

Ahora, si bien en primera instancia algunos de los importantes proveedores como ARM no son vulnerables a dichos fallos, más tarde fueron identificados nuevas variantes de estos mismo, aumentando el numero de estos de 2 a 27 vulnerabilidades. Entonces con el descubrimiento de estas variaciones, los que no podía afectar a ARM, lo logro, pero esto no es del todo oscuro, muchas de estas nuevas variaciones son incapaces de ser ejecutadas en ARM y otros proveedores, con lo cual, la tarea de darle solución o prevención a este tipo se fallas se reduce.

<p align="center">
<img width="394" height="479" src="url de laa imagen aqui">
</p>
