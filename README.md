# Laboratorio 4

**Universidad Militar Nueva Granada**

**Asignatura:** Instrumentación biomedica y biosensores

**Estudiantes:** Dubrasca Martínez, Mariana Leyton, Joshara Valentina Palacios

**Fecha:** 13 de octubre del 2026

**Título de la práctica:** Diseño y construcción de una incubadora neonatal a escala

# **Introducción**

La incubadora neonatal es un dispositivo médico que busca reproducir, en lo posible, las condiciones del vientre materno para asegurar la supervivencia y el desarrollo del recién nacido [1], [2]. La variable más crítica es la temperatura, que debe mantenerse alrededor de los 37 °C [3]. Los neonatos prematuros son especialmente vulnerables: su piel es más delgada y su sistema nervioso inmaduro, por lo que no regulan bien su temperatura corporal y pierden calor con facilidad [4]. A la vez, en países tropicales el exceso de calor también es un riesgo, pues puede provocar hipertermia [5]. Por esto, el control preciso de la temperatura es el núcleo del funcionamiento de una incubadora.

Las incubadoras se desarrollan desde el siglo XIX para mantener la estabilidad térmica de recién nacidos de bajo peso o enfermos, lo que mejoró de forma importante su supervivencia. Hoy son equipos de alta tecnología, aunque aún tienen retos pendientes, como reducir las pérdidas de calor del neonato, controlar mejor la humedad y disminuir la exposición al ruido y a la luz [6]. Según la Organización Mundial de la Salud, la temperatura corporal normal de un recién nacido está entre 36,5 °C y 37,5 °C, y la protección térmica busca evitar tanto la hipotermia como la hipertermia [7]. Para lograrlo, se busca mantener al neonato en un ambiente térmico neutro, es decir, aquel en el que mantiene su temperatura con el mínimo gasto de oxígeno y energía [8]. Frente a otros dispositivos de calentamiento, como las cunas de calor radiante (servo-cunas), las incubadoras cerradas reducen la pérdida insensible de agua del neonato [9].

En esta práctica se diseñó y construyó un modelo a escala que regula la temperatura interna por medio de un bombillo con relé y un ventilador dentro del rango de 36 °C a 37,5 °C, ademas de midir el peso del neonato con una celda de carga.

## ***Partes principales de una incubadora neonatal***

Para identificar las partes se tomó como referencia el manual de uso de la incubadora comercial Dräger Isolette 8000 plus [10]. Según el fabricante, este equipo proporciona un ambiente controlado para bebés prematuros y a término de hasta 10 kg, y regula la temperatura y, de forma opcional, el oxígeno y la humedad [10, Sec. 3.1].

| Parte | Función | Sección del manual | 
| --- | --- |  ---  |
| Cúpula transparente |Encierra el compartimiento del paciente y permite observarlo. No debe levantarse con el bebé adentro; el acceso se hace por los paneles y portillos. | 2.2.11, 4.1  |
| Paredes dobles internas |Forman una doble pared en la capota que ayuda a reducir las pérdidas de calor. | 7.2.2 |
| Paneles de acceso |Permiten sacar la cama y atender al bebé. Al abrirlos se activa una "cortina" de aire caliente que limita la pérdida de calor. | 2.9.1, 2.9.3 |
| Portillos (ovalados o tipo iris) |Permiten introducir las manos sin abrir los paneles completos. | 4.3, 7.2.2 |
| Cama y colchon |Soporte del neonato; se desliza hacia afuera y se inclina (posición de Trendelenburg) con perillas.| 4.1, 7.2.2 |
| Sistema de calefacción y circulación de aire|Un calefactor y un impulsor (ventilador) calientan el aire y lo introducen al compartimiento por ranuras de ventilación. El controlador registra el porcentaje de potencia del calefactor.| 2.9.2, 5.2, 6.5 |
| Módulo de sensores |Aloja los sensores de temperatura del aire, humedad y oxígeno, y los conectores de las sondas de piel y de la báscula. | 4.5 |
| Sondas de temperatura de piel |La sonda central (amarilla, en el abdomen) controla la temperatura en modo piel; la periférica (blanca, en mano o pie) solo monitorea. | 8.1.3–8.1.5 |
| Modos de control de temperatura |Modo aire (regula la temperatura del aire) y modo piel (regula la temperatura de la piel del bebé). | 2.2.6, 8.1 |
| Sistema de humidificacion |Reservorio con agua destilada y un evaporador; permite fijar la humedad relativa entre 30 % y 95 %. | 6.5, 8.2 |
| Sistema de oxigeno |Entrada de oxígeno en la parte trasera; en modo servo controla la concentración entre 21 % y 65 % usando dos sensores redundantes. | 4.2, 6.6, 8.3 |
| Filtro de entrada de aire |Filtra el aire que entra al equipo; si se ensucia puede alterar la concentración de oxígeno y acumular CO₂. Debe cambiarse al menos cada 3 meses. | 4.2, 7.2.2 |
| Bascula (opcional) |Se instala bajo el colchón y pesa al bebé sin sacarlo; tiene funciones de cero y tara y se verifica con un peso conocido. | 6.4, 7.2.8, 8.6 |
| Controlador con pantalla |Muestra temperatura, humedad, oxígeno y tendencias, y permite ajustar los valores deseados. | 5.1, 5.2 |
| Alarmas |Avisan, entre otros, por falla de energía, baja temperatura del aire o de la piel, sonda de piel desconectada y corte por alta temperatura (el equipo no debe superar 39,9 °C). | 7.2.1, 9 |
| Carro con ajuste de altura | Soporta la incubadora, permite subirla o bajarla y tiene ruedas con freno. | 4.1, 7.2.3 |

# **Metodología**

## ***1. Diseño del sistema***

Se definió el alcance de la incubadora automatizada como el uso de sensores y actuadores junto con un microcontrolador ESP32 para lograr la función de lectura de temperatura y peso, así como visualización de las mediciones y controlar el sistema de calefacción y ventilador. Se definieron 2 variables de medición, temperatura interna que se puede medir con un termistor NTC de 10 kΩ y peso utilizando una celda de carga que esta conectada a un modulo HX711. 
Finalmente se conectó una pantalla LCD de 16 × 2 caracteres con interfaz de comunicación I2C para mostrar las variables medidas. El calentador es una bombilla controlada por un relé de estado sólido (SSR-40DA). La ventilación es controlada con un ventilador de 12 V y una etapa electrónica MOSFET. 

## ***2. Asignación de pines y configuración del hardware***

Una vez identificados los componentes, se estableció la asignación de pines del ESP32 para facilitar la integración del hardware y el desarrollo del firmware.

| Componente | Pin del ESP32 | Función |
|---|---|---|
| Termistor NTC | GPIO 34 | Entrada analógica para la medición de temperatura |
| Ventilador | GPIO 25 | Señal de control del MOSFET |
| Relé de estado sólido SSR | GPIO 23 | Señal de control del calentamiento |
| HX711 DT/DOUT | GPIO 32 | Comunicación de datos de la celda de carga |
| HX711 SCK/CLK | GPIO 33 | Señal de reloj del HX711 |
| LCD SDA | GPIO 21 | Línea de datos I2C |
| LCD SCL | GPIO 22 | Línea de reloj I2C |

La conexión de los componentes se planteó de acuerdo con los requerimientos de alimentación y comunicación de cada módulo.
Los actuadores se conectaron a través de sus respectivas etapas de potencia. El ESP32 proporciona las señales de control, pero no alimenta directamente el ventilador ni la bombilla de calentamiento como se puede apreciar en la siguente imagen

<img width="390" height="435" alt="image" src="https://github.com/user-attachments/assets/e2b57938-a5a4-402f-a66c-45172d966dba" />

## ***3. Montaje del circuito***

El montaje se organizó por etapas con el fin de facilitar la identificación de posibles errores y comprobar individualmente el funcionamiento de cada componente.

En primer lugar, se realizó la conexión del termistor NTC y la resistencia fija para obtener una señal analógica relacionada con la temperatura emitida por la bombilla que es regulada mediante el relé Posteriormente, se conectaron la celda de carga y el módulo HX711 para adquirir las mediciones de peso. En la siguiente etapa, se integró la pantalla LCD mediante las líneas SDA y SCL del ESP32.

Finalmente, se incorporaron los circuitos de control del ventilador y del calentamiento, para ello se realizaron aberturas el la caja empleada como incubadora, con el fin de adaptar las necesidades, ademas se usó una caja de carton aparte para poder separa el circuito y su cableado del espacio destinado al bebé
<img width="287" height="436" alt="image" src="https://github.com/user-attachments/assets/2fe20bce-76c1-432c-818f-e3aa5aac701c" />


## ***4. Temperatura***

La temperatura fue medida utilizando un termistor NTC de 10 kΩ. Esta resistencia eléctrica disminuye su valor cuando la temperatura aumenta. El sensor fue conectado a un divisor de tensión cuya señal fue alimentada a la entrada analógica GPIO 34 del ESP32.

A partir de la tensión medida el firmware estima la resistencia del termistor utilizando la siguiente ecuación que corresponde al divisor de tensión:
```math
R_{NTC}=R_{fija}\left(\frac{V_s}{V_{NTC}}-1\right)
```

Donde RNTC es la resistencia del termistor estimada por el firmware, Rfija es la resistencia fija del divisor y Vs es la tensión de alimentación del divisor de tensión. VNTC es la tensión medida en el punto intermedio.

A partir de la resistencia del termistor NTC se calcula la temperatura utilizando el modelo Beta:

```math
T_K= 
\frac{1}{\frac{1}{T_0}+ 
\frac{1}{B}\ln\left(\frac{R_{NTC}}{R_0}\right)} 
```
Finalmente la temperatura en grados Celsius esta dada por:

```math
T_C=T_K-273.15 
```

Como resistencia nominal y constante Beta inicial se utilizó Rt= 10 kΩ y B= 3950 respectivamente. Se debe elegir estos valores de acuerdo al termistor utilizado.

Verificación de medida: Se verificará la medida calculando la temperatura en el ESP32 e informando con un.display() junto a la temperatura mostrada en un termómetro comercial. De esta manera podemos observar si hay desviaciones entre ambas mediciones y así decidir si es necesario recalibrar los valores de medida. Cualquier corrección deberá ser verificada mediante mediciones. 

## ***5. Pesaje***

Se realizó la medición de peso utilizando una celda de carga conectada al módulo HX711. La celda convierte la deformación generada por una carga aplicada a la misma en una señal eléctrica de baja amplitud. Esta señal es amplificada y digitalizada por el módulo HX711.

La conexión del modulo a ESP32 se realizo utilizando GPIO 32 como DT/DOUT y GPIO 33 como SCK/CLK. Para el proceso de lectura se plantea utilizar la librería HX711 en el IDE Arduino.

El proceso de calibración se realizara de la siguiente manera:

1. Fijar la celda de carga de manera segura y verificar conexiones.
2. Prender sistema y esperar estabilizar valores(unos 10s aproximadamente). 
3. Quitar los objetos sobre la plataforma y ejecutar tara.
4. Agregar una masa conocida sobre la plataforma. 
5. Tomar lectura del valor indicado por el sistema.}

Para verificar el comportamiento del sistema se puede calcular el error absoluto como:

```math
E=m_{indicada}-m_{referencia} 
```

donde. El error relativo viene dado por: 

```math
E_{\%}= 
\frac{|m_{indicada}-m_{referencia}|} 
{m_{referencia}}\times100 
```

Nota: Este calculo es válido para cuando m referencia es distinto de cero.

## ***6.  Control de temperatura***  

La lógica del control de temperatura fue diseñada para mantenerse dentro de una histéresis, comenzando desde un límite inferior de 36 °C y un límite superior de 37 °C. De esta manera se logra mantener el estado anterior del actuador dentro de la banda de histéresis y evitar conmutaciones repetidas cuando la temperatura este cerca del punto de referencia. 

La siguiente tabla resume la lógica de control establecida para el prototipo. 

Temperatura | Controladora de Calor  
--------------------|----------------------  
Menor o igual a 36°C| Solicita calor.  
Mayor o igual a 37°C| Apaga calor.  
Valor intermedio | Mantener estado anterior.  

Por simplicidad, la lógica para la ventilación fue la complementaria a la lógica mostrada en la tabla anterior. 

Temperatura | Controladora de Ventilación  
--------------------|---------------------------  
Mayor o igual a 37°C| Solicita ventilador.  
Menor o igual a 36°C| Apaga ventilación.  
Valor intermedio | Mantener estado anterior.  

Las señales de control son generadas basado en la temperatura calculada desde el ESP32. Cuando la medición es marcada como inválida, el programa coloca las señales de control de calor y ventilación en el estado de apagado. 

## ***7.  Control de los actuadores***  

El calentamiento es controlado desde la salida GPIO 23 del ESP32, conectado a la entrada de control del relé de estado sólido SSR-40DA. Este componente permite conmutar la carga aplicada al calentamiento desde una señal de bajo voltaje siempre y cuando se cumplan las recomendaciones del fabricante y las condiciones eléctricas de conexión de la carga. 

El ventilador de 12 V es controlado desde GPIO 25 a través de una etapa de potencia con MOSFET. Este tipo de componentes permiten usar una señal proveniente desde el microcontrolador para regular el flujo de corriente hacia el motor sin requerir que el GPIO provea directamente dicha corriente. 

Al conectar los actuadores se recomienda revisar que las fuentes de alimentación seleccionadas sean adecuadas para las cargas que regulan. Adicionalmente, los circuitos de bajo voltaje deben mantenerse separados eléctricamente de los circuitos de potencia. Por la presencia de carga conectada a corriente alterna se recomienda que el montaje cuente con aislamiento, protección contra sobrecorriente y un mecanismo independiente de corte por temperatura. La conexión de la red eléctrica debe ser probada siguiendo procedimientos adecuados y por personal calificado. 

## ***8.  Visualización de las variables en la LCD***

Se decidió incluir una pantalla LCD de 16 × 2 caracteres para hacer un seguimiento más sencillo del sistema. El dispositivo fue conectado a través de la comunicación I2C teniendo SDA en GPIO 21 y SCL en GPIO 22. La comunicación con la pantalla se implementó usando la biblioteca LiquidCrystal_ I2C. 

La pantalla fue dividida en dos filas, teniendo la primera fila reservada para mostrar la temperatura y la segunda fila para mostrar el peso calculado por el sistema. El valor de dirección I2C de la pantalla debe ser verificado en el dispositivo montado ya que este valor puede variar. 

Cuando se estén realizando las pruebas, se debe confirmar que ambas líneas se muestran y que los valores mostrados corresponden con las mediciones procesadas por el microcontrolador. Si se detectan mediciones inválidas, se deberían mostrar mensajes de error que permitan identificar un error de lectura de una medición válida. 

## ***9.  Secuencia final***  

La secuencia establecida es la siguiente:  

Inicializar la comunicación serial y configurar entradas y salidas 
Inicializar pantalla LCD y módulo HX711  
Tare balanza si el módulo está disponible  
Leer señal analógica proveniente del termistor  
Calcular resistencia estimada y convertir a temperatura.  
Determinar si la lectura de temperatura es válida 
Implementar la lógica de histéresis determinando los estados de los actuadores. 
Leer balanza y convertir a peso si el módulo está disponible. 
Actualizar información mostrada en la pantalla LCD.  
Mostrar valores medidos y estados de control en el monitor serial 
Repetir ciclo de adquisición y control.  

El periodo de lectura inicial definido para el sistema es de un segundo. La integración debe de incluir la capacidad de detectar errores de comunicación y/o señales inválidas para evitar mostrar mediciones que puedan ser catalogadas erróneamente como válidas. 

# **Resultados**

## ***Medición de temperatura***

| Estado | Temperatura medida | Bombillo | Ventilador | 
| --- | --- |  ---  |  ---  |
| Inicio (Ambiente) | 25,63 °C  | Solicitado  | Apagado  |
| Limite superior alcanzado | 37,08 °C  | No solicitado  | Encendido  |

## ***Medición de peso***

| Prueba | Medida obtenida | 
| --- | --- |
| Inicial | 0 g  | 
| Objeto conocido | 1,400 g  |

# **Análisis de resultados**

## ***Estrategia de control implementada para la medición de la temperatura***

El control de temperatura se implementó en el ESP32 como un control ON-OFF con histéresis de dos actuadores, a partir de la lectura del termistor NTC:

| Condición | Bombillo con relé | Ventilador | Propósito | 
| --- | --- |  ---  |  ---  |
| T ≤ 36,0 °C | Encendido  | Apagado  | Calentar la cámara  |
| 36,0 °C < T < 37,0 °C | Mantiene su estado anterior  | Mantiene su estado anterior  | Zona de histéresis  |
| T ≥ 37,0 °C | Encendido  | Apagado  | Calentar la cámara  |

La banda de histéresis de 1 °C (36,0–37,0 °C) evita que los actuadores conmuten continuamente cuando la temperatura está cerca de un umbral. El límite superior se fijó en 37,0 °C, por debajo del máximo de 37,5 °C que pide la guía, para dejar un margen frente al sobreimpulso.

- Con la cámara a temperatura ambiente de 25,63 °C, muy por debajo de 36 °C, el sistema solicitó calentamiento y mantuvo el ventilador apagado, que es la respuesta esperada. Esto confirma que la lectura del termistor y la lógica de decisión funcionan.
- El sistema logró llevar la cámara desde 25,63 °C hasta 37,08 °C, es decir, subió más de 11 °C. Esto muestra que el bombillo usado como fuente de calor de 10W, fue suficiente para alcanzar el rango clínico en la cámara del prototipo.
- Al superar 37,0 °C el bombillo se apagó y el ventilador se encendió, como estaba programado. La temperatura registrada en ese momento (37,08 °C) supera el umbral programado en solo 0,08 °C y se mantiene dentro del rango de 36,0 a 37,5 °C que exige la guía. Ese pequeño exceso se explica por la inercia térmica: cuando el relé apaga el bombillo, su vidrio y el aire cercano siguen calientes y entregan calor a la cámara por un tiempo.

## ***Estrategia de control implementada para la medición del peso***

La báscula, formada por una celda de carga y el módulo HX711, se calibró con un factor de 0,5347 y se puso en cero (tara) al iniciar el sistema.

| Prueba | Masa patrón | Lectura | Error absoluto | Error relativo | 
| --- | --- | --- | --- | --- |
| Inicial | 0 g  | -0,51 g  | 0,51 g  |  --  |
| Objeto conocido | 1,600 g  | 1,400 g  | 0,2 g  | 12,5 %  | 

Los errores se calcularon como:

<img width="449" height="168" alt="image" src=https://github.com/estmarianaleyton-cmyk/Laboratorio.4/blob/main/error.png>

- Un error relativo del 12,5 % parece grande, pero corresponde a solo 0,2 g. El porcentaje sale alto porque el objeto patrón es muy liviano: 1,6 g es apenas el 0,03 % de la capacidad de la celda de carga. Con masas tan pequeñas, cualquier variación mínima de la lectura pesa mucho en el porcentaje.
- Sin carga, la báscula marcó −0,51 g en vez de 0 g. Esa desviación es mayor que el error medido con el objeto, lo que indica que el ruido y las variaciones de la celda después de la tara y ruido eléctrico del HX711 limitan la resolución de la báscula a unas décimas de gramo.
- El peso de un recién nacido está aproximadamente entre 500 g y 4500 g. Si el error absoluto se mantiene en el orden de 0,2 a 0,5 g, para un bebé de 2000 g representaría apenas un 0,01 % a 0,03 %, lo cual sería despreciable en la práctica clínica.

# **Discusión**
## Pregunta 1: Otras variables críticas en el monitoreo neonatal

Además de la temperatura y el peso:

- **Frecuencia cardíaca (FC) y ECG:** detecta bradicardia y taquicardia, que son signos tempranos de inestabilidad.
- **Saturación de oxígeno (SpO₂):** evita tanto la hipoxia como la hiperoxia, que en prematuros se asocia con retinopatía; los rangos objetivo se han estudiado ampliamente.
- **Frecuencia respiratoria y apnea:** la apnea del prematuro es frecuente por la inmadurez del centro respiratorio.
- **Humedad relativa:** en prematuros reduce las pérdidas insensibles de agua y de calor [13].
- **Glucosa:** la hipoglucemia es común y puede causar daño neurológico [13].
- **Bilirrubina:** la ictericia neonatal requiere fototerapia si supera ciertos umbrales [14].
- **Presión arterial:** indica perfusión y estado hemodinámico.
- **Ruido y luz ambiental:** el exceso afecta el desarrollo neurológico y el sueño.

## Pregunta 2: ¿Qué falta para una incubadora neonatal real?

- **Cumplimiento normativo:** IEC 60601-1 (seguridad eléctrica) e IEC 60601-2-19 (requisitos específicos de incubadoras) [11], más el registro ante la autoridad sanitaria local.
- **Seguridad independiente:** termostato de corte separado del control principal y sensores redundantes.
- **Sistema de alarmas:** priorizado y con alertas audibles y visuales (IEC 60601-1-8).
- **Control de humedad:** humidificador con control en lazo cerrado [11].
- **Circulación y filtrado de aire:** flujo homogéneo y filtro HEPA.
- **Ruido y vibración bajos:** idealmente por debajo de 45 dB dentro de la cámara.
- **Materiales biocompatibles** y fáciles de desinfectar.
- **Gestión de riesgos y calidad:** El cumplimiento de normas que permitan brindar seguridad y minimizar riegos al paciente
- **Validación clínica y calibración** de los sensores.
- **Alimentación de respaldo** (batería o UPS).

## Pregunta 3: Semejanzas entre incubadora y servo-cuna

- Ambas son equipos de **termorregulación** para bebes.
- Ambas usan **control servo**: un sensor de temperatura de piel ajusta la potencia del calefactor.
- Ambas tienen **alarmas** de temperatura, falla de sensor y desconexión [11], [12].
- Ambas ofrecen **modo manual y modo servo**.
- Ambas buscan mantener la **temperatura corporal neutra** (36.5–37.5 °C) y reducir el gasto energético del bebé [13].
- La principal diferencia es que la incubadora es un **ambiente cerrado** (calor por convección), mientras que la servo-cuna es **abierta** (calor radiante). Por eso la servo-cuna da mejor acceso al paciente, pero tiene mayores pérdidas de agua. Cada una se rige por su propia norma [11], [12].


# **Conclusión**

El presente trabajo consistió en el desarrollo de una incubadora automatizada usando ESP32, con lo cual se generó la interrogante de que sensores, actuadores y sistemas de control podrían integrarse a la misma. Se eligió monitorizar temperatura y peso, mostrar las mediciones en una pantalla LCD, y usar una lógica de histéresis para controlar el calentamiento y ventilación de la incubadora. El prototipo diseñado es una plataforma académica para empezar a entender cómo instrumentar y automatizar cuidados neonatales. Sin embargo, antes de usarla en un recién nacido, se requeriría validar experimentalmente las mediciones, incrementar la precisión y homogeneidad del control térmico, monitorear otras variables fisiológicas y contar con alarmas y protecciones independientes. Como trabajo futuro, se debería probar su funcionamiento en condiciones controladas, registrar los resultados obtenidos y verificar su seguridad y confiabilidad sin involucrar recién nacidos hasta tanto cumpla con los requerimientos técnicos, clínicos y regulatorios ya que es necesario realizar pruebas experimentales y evaluar los errores de medición para determinar su desempeño real y establecer las mejoras necesarias.

# **Referencias**

[1] C. G. K. Tran et al., "Designing a low-cost multifunctional infant incubator," J. Lab. Autom., vol. 19, no. 3, pp. 332–337, Jun. 2014. https://doi.org/10.1177/2211068214530391

[2] L. Restrepo-Pérez, N. Durango-Londoño, N. E. Gómez-Suárez, F. González-Ramírez y N. Rivera-Bonilla, "Prototipo de incubadora neonatal," Revista Ingeniería Biomédica, vol. 1, no. 1, pp. 55–59, 2007. http://www.scielo.org.co/pdf/rinbi/v1n1/v1n1a12.pdf

[3] M. van Leeuwen et al., European Standards of Care for Newborn Health: Temperature management in newborn infants, EFCNI, Nov. 2018. https://newborn-health-standards.org/standards/standards-english/care-procedures/temperature-management-in-newborn-infants/

[4] R. B. Knobel-Dail, "Role of effective thermoregulation in premature neonates," Research and Reports in Neonatology, vol. 4, pp. 147–156, 2014. https://doi.org/10.2147/RRN.S52377

[5] R. E. Black et al., "Global, regional, and national causes of child mortality in 2008: a systematic analysis," Lancet, vol. 375, pp. 1969–1987, Jun. 2010. https://doi.org/10.1016/S0140-6736(10)60549-1

[6] R. Antonucci, A. Porcella y V. Fanos, "The infant incubator in the neonatal intensive care unit: unresolved issues and future developments," J. Perinat. Med., vol. 37, no. 6, pp. 587–598, 2009. https://doi.org/10.1515/JPM.2009.109

[7] World Health Organization, Thermal protection of the newborn: a practical guide, WHO/RHT/MSM/97.2. Ginebra: WHO, 1997. https://www.who.int/publications/i/item/WHO_RHT_MSM_97.2

[8] T. I. Sherman, J. S. Greenspan, N. St. Clair, S. M. Touch et al., "Optimizing the neonatal thermal environment," Neonatal Network, vol. 25, no. 4, pp. 251–260, 2006.

[9] V. Flenady y P. G. Woodgate, "Radiant warmers versus incubators for regulating body temperature in newborn infants," Cochrane Database Syst. Rev., no. 4, art. CD000435, 2003. https://doi.org/10.1002/14651858.CD000435

[10] Drägerwerk AG & Co. KGaA, Instructions for use Isolette 8000 plus, Incubator, Software 5.n, ed. 4, doc. MU25944. Lübeck, Alemania, Jul. 2019. https://www.draeger.com/Content/Documents/Content/isolette-8000-plus-sw-5n-ifu-mu25944-en.pdf

[11] IEC 60601-2-19:2020+AMD1:2023. *Medical electrical equipment – Part 2-19: Particular requirements for the basic safety and essential performance of infant incubators*. https://webstore.iec.ch/en/publication/89860

[12] IEC 60601-2-21. *Medical electrical equipment – Part 2-21: Particular requirements for the basic safety and essential performance of infant radiant warmers*. Consulta la edición vigente en https://webstore.iec.ch

[13] World Health Organization (2022). *WHO recommendations for care of the preterm or low-birth-weight infant*. https://www.who.int/publications/i/item/9789240058262

[14] Kemper, A.R. et al. (2022). Clinical Practice Guideline Revision: Management of Hyperbilirubinemia in the Newborn Infant 35 or More Weeks of Gestation. *Pediatrics*, 150(3),https://doi.org/10.1542/peds.2022-058859
