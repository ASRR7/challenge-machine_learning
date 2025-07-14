# challenge-machine_learning
Challenge de Machine Learning de Alura Latam - ONE Next Education

<br>

Durante este desafio se continua el análisis del dataset del desafio anterior, pero esta vez implementando modelos de machine learning para lograr una predicción de los clientes en riesgo de abandono.

## Mejores modelos

Con las modificaciones al umbral se alcanzaron mejores resultados en recall, lo que hace que el modelo identifique a una mayor cantidad de clientes que van a abandonar el servicio.

- **_DecisionTreeClassifier_** profundidad de n=3. Con 35 falsos negativos y 815 falsos positivos. Clasificando correctamente 526 correctos positivos y 805 correctos negativos.

- **_LogisticRegression_**. Con 40 falsos negativos y 722 falsos positivos. Clasificando correctamente 521 correctos positivos y 898 correctos negativos.

- **_RandomForest_**. n_estimators=100, profundidad n=20. Con 82 falsos negativos y 613 falsos negativos. Clasificando correctamente 479 correctos positivos y 1007 correctos negativos.


Con estos modelos se puede implementar una estrategia agresiva para evitar la cancelación de los clientes aunque eso significa tener algunos falsos positivos de clientes que no se iban a ir del servicio.

## **Conclusiones**

<hr> <br>

### Modelo ganador
El mejor modelo fue _DecisionTree_, con parámetro `max_depth=5`, logrando un recall de 94% en la clasificación de clientes que posiblemente abandonarán, aunque sacrificando la presición con solo 39%. Este modelo prioriza clasificar correctamente a los clientes que abandonarán, por lo que al implementarlo se pueden obtener resultados muy rápidos para identificar a clientes en potencial abandono y utilizar estrategias como descuentos, mejora del servicio, entre otras, que logren evitar el abandono del cliente.

_El modelo fue serializado para ser utilizado:_ `champion.pkl`

<hr> <br>

### Variables a considerar
Para el mejor modelo las variables más importantes fueron:

- contract_two_year                 || **0.381847**
- contract_one_year                 || **0.310014**
- tenure                            || **0.107896**
- internet_service_fiber_optic      || **0.094772**

Con estas cuatro variables se forma un 89.45%

<br>

Esto también se confirma al analizar las variables más importantes para _RandomForest_:

- _**tenure**_                       || **0.212266**
- charge_monthly                     || **0.190196**
- payment_method_electronic_check    || **0.071118**
- _**contract_two_year**_            || **0.069177**
- _**internet_service_fiber_optic**_ || **0.049685**
- _**contract_one_year**_            || **0.047278**

Con estas seis variables se forma un 63.97%, entre las que se encuentran las mismas cuatro variables del modelo _DecisionTree_.

<br>

Con lo anterior podemos observar que los más fuertes indicadores de abandono son _tenure_, *contract_one_year* y *contract_two_year*. Esto resulta evidente, pues si los clientes tiene contratos a uno o dos años, no pueden cancelar el servicio a diferencia de los que tienen contrato mensual. 

Esto también se relaciona con _tenure_ pues con el tiempo se va formando la lealtad y es más dificil que los clientes cambien del servicio al que ya están acostumbrados.
<br>

Gracias al modelo de regresión logística podemos observar que *charge_monthly* y *internet_service_no* son los mayores factores de riesgo para el abandono.
Podemos interpretar que *charge_monthly* influye bastante porque los clientes buscan la mejor calidad que les pueda ofrecer un precio, y al incrementar los costos del servicio buscarán que la calidad también aumente.

Para el *internet_service_no* que es el segundo mayor factor de riesgo de abandono podemos ayudarnos de otros servicios que tienen factores negativos (influyen a que el cliente no cancele), como por ejemplo: *phone_service*, *streaming_tv*, *streaming_movies*, *online_security*, *tech_support*, entre otros.
Esto podría representar que a los clientes que tienen una mayor cantidad de servicios es más dificil el abandonar el servicio, mientras que a los clientes que no tienen internet (y por ende tampoco todos los servicios extras) es más fácil que abandonen pues solamente tienen el servicio de teléfono.

<hr> <br>

### Estrategias a implementar para mitigar el abandono


1. Como primera estrategia y evitar que más clientes abandonen, se debe de utilizar el modelo serializado en la base de datos de los clientes que todavía están activos para hacer un análisis e identificar a los posibles clientes que tienen posibilidades de abandonar e intentar mejorar el servicio, así como ofrecer promociones o descuentos a sus facturas al incluir servicios extras, ya que como anteriormente se mencionó, *charge_monthly* es de los puntos más influyentes para el abandono.

<br>

2. Una vez manejados a los clientes ya existentes que pueden abandonar, se debe de implementar una estrategia que atienda a los potenciales nuevos clientes. Para ello se debe de ofrecer promociones o beneficios al contratar el servicio en períodos de uno o dos años, esto para lograr crear una lealtad del cliente y hacer que sea menos probable su abandono. Del mismo modo, incluir descuentos al contratar una mayor cantidad de servicios porque como se ha visto, el tener una mayor cantidad de servicios reduce la probabilidad de abandono.

<br>

3. Aunque las estrategias anteriores sean de utilidad para disminuir el abandono tanto de los clientes actuales como de los futuros, también se tendría que hacer un análisis que incluya los factores económicos para saber si el ofrecer mejores servicios, descuentos y promociones es viable financieramente, puesto que la cantidad de clientes que cancelan es pequeña comparado con la cantidad de clientes que se mantienen. Sin embargo, también puede ser una oportunidad de ofrecer mejores servicios que no solo hagan que los clientes ya existentes eviten cancelar, sino también que al mejorar la reputación y visibilidad de un buen servicio sea de utilidad para atraer a nuevos clientes.
