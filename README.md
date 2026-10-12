# Laboratorio 4

**Universidad Militar Nueva Granada**

**Asignatura:** Instrumentación biomedica y biosensores

**Estudiantes:** Dubrasca Martínez, Mariana Leyton, Joshara Valentina Palacios

**Fecha:** 13 de octubre del 2026

**Título de la práctica:** Diseño y construcción de una incubadora neonatal a escala

# **Introducción**

La incubadora neonatal es un dispositivo médico que busca reproducir, en lo posible, las condiciones del vientre materno para asegurar la supervivencia y el desarrollo del recién nacido [1], [2]. La variable más crítica es la temperatura, que debe mantenerse alrededor de los 37 °C [3]. Los neonatos prematuros son especialmente vulnerables: su piel es más delgada y su sistema nervioso inmaduro, por lo que no regulan bien su temperatura corporal y pierden calor con facilidad [4]. A la vez, en países tropicales el exceso de calor también es un riesgo, pues puede provocar hipertermia [5]. Por esto, el control preciso de la temperatura es el núcleo del funcionamiento de una incubadora.

Las incubadoras se desarrollan desde el siglo XIX para mantener la estabilidad térmica de recién nacidos de bajo peso o enfermos, lo que mejoró de forma importante su supervivencia. Hoy son equipos de alta tecnología, aunque aún tienen retos pendientes, como reducir las pérdidas de calor del neonato, controlar mejor la humedad y disminuir la exposición al ruido y a la luz [6]. Según la Organización Mundial de la Salud, la temperatura corporal normal de un recién nacido está entre 36,5 °C y 37,5 °C, y la protección térmica busca evitar tanto la hipotermia como la hipertermia [7]. Para lograrlo, se busca mantener al neonato en un ambiente térmico neutro, es decir, aquel en el que mantiene su temperatura con el mínimo gasto de oxígeno y energía [8]. Frente a otros dispositivos de calentamiento, como las cunas de calor radiante (servo-cunas), las incubadoras cerradas reducen la pérdida insensible de agua del neonato [9].

En esta práctica se diseñó y construyó un modelo a escala que regula la temperatura interna por convección forzada (ventilador + elemento resistivo) dentro del rango de 36 °C a 37,5 °C, indica el estado térmico mediante un panel de tres LEDs y mide el peso del neonato con una celda de carga.

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
