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

| Parte | Función | Sección del manual|
| --- | --- | --- |
| Cúpula transparente | 6.6 | 6.6 |
| Paredes dobles internas | 42.5 | 6.6 |
| Paneles de acceso | 32.8 | 6.6 |
| Portillos (ovalados o tipo iris) | 6.6 | 6.6 |
| Cama y colchon | 42.5 | 6.6 |
| Sistema de calefacción y circulación de aire| 32.8 | 6.6 |
| Módulo de sensores | 6.6 | 6.6 |
| Sondas de temperatura de piel | 42.5 | 6.6 |
| Modos de control de temperatura | 32.8 | 6.6 |
| Sistema de humidificacion | 6.6 | 6.6 |
| Sistema de oxigeno | 42.5 | 6.6 |
| Filtro de entrada de aire | 32.8 | 6.6 |
| Bascula (opcional) | 6.6 | 6.6 |
| Controlador con pantalla | 42.5 | 6.6 |
| Alarmas | 32.8 | 6.6 |
| Carro con ajuste de altura | 6.6 | 6.6 |
