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
