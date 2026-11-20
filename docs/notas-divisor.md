# Notas de diseño: Parte B monitor de voltaje de batería

Autor:Fernando

Fecha:18 de noviembre de 2026

Estado:Borrador

1. Requisitos del sistema

Se requiere diseñar un divisor de voltaje para monitorear una batería LiPo 2S, CON VOLTAJE DE 6.0 V a 8.4 V.

El voltaje de salida debe cumplir con las siguientes condiciones:

-No superar 3.0 V para proteger la entrada del ADC.

-Mantener un consumo de corriente menor a 100 microamperios.

-Utilizar resistencias de valores comerciales E24 o E12.

2.resistencia total mínima

R = V / I

Rt > 8.4 V / 0.0001 A

Rt > 84 kΩ

8.4 V es el de peor caso porque es el voltaje máximo de la batería. Al aumentar el voltaje, también aumenta la corriente que circula por el divisor,I = V / R.

3.Relación entre las resistencias

la ecuacion divisora de voltaje es:

Vout = Vin × R2 / (R1 + R2)

necesitamos que la salida sea de 3.0 V cuando la entrada alcance 8.4 V.

3.0 / 8.4 ≈ 0.3571

R2 representa el 35.71 % de la resistencia total y R1 representa el 64.29 % restante.

A partir de la ecuación del divisor:

Vout / Vin = R2 / (R1 + R2)

despejamos

R1 / R2 = (Vin − Vout) / Vout

Sustiuyo

R1 / R2 = (8.4 − 3.0) / 3.0

R1 / R2 = 5.4 / 3.0 = 1.8

R1 = 1.8 × R2

4.Cálculo ellimite minimo para R2

sustituyo la relación R1 = 1.8 × R2 en la condición de resistencia total:

R1 + R2 > 84 kΩ

1.8 × R2 + R2 > 84 kΩ

2.8 × R2 > 84 kΩ

R2 > 84 kΩ / 2.8

R2 > 30 kΩ

el resultado me dice el límite mínimo para R2.

5.Selección de valores comerciales E24 y calcular corriente

grupo A(33 y 62) o grupo B (33 y 56)???

decidi tomar los valores del grupo a 33k ohms y 62k ohms de la serie E24 por que al voltaje maximo (8.4v) me da un voltaje final de 2.918v lo cual cumple con el limite establecido de 3.0v. incluso con la tolerancia de +5% me daria un voltaje de 3.02v siendo este el peor caso.

Al ya tener nuestras resistencias asigandas calculamos la corriente:

8.4/62+33 = 8.4/95 = 88.42 micro A

Tambien se satisface el limite establecido dando como resultado 88.42 micro A con la tolerancia -5% nos daria una corriente de 93.07 micro A con un margen muy seguro de los 100microA

6.calcular voltaje de salida

como ya mencione con un voltaje de 8.4v me dio 2.918v pero y con la bateria descargada?

6.0v= 6x33/62+33 = 6x 33/95 = 2.08v

con la bateria totalmente descargada nos da un voltaje de 2.08v

7. Potencia disipada en cada resistencia

PR1 = I^2 X R1 = (88.42 X 10X6^-6 A) X 62,000 = 484.7 micro W (0.485 mW)

PR2 = I^2 X R2 = (88.42 X 10X6^-6 A) X 33,000 = 285.0 micro W (0.285 mW)

PR1 + PR2 =

8. determinar la resolucion por cuenta del ADC 12bits

VBAT = (3.3/4096) (95/33) = 0.8057mV x 2.8788 = 2.319mV

9. problema de la impedancia alta

El ADC del microcontrolador capacitor interno que necesita cargarse muy rápido cada vez que toma una muestra. Si las resistencias del divisor son muy grandes, limitan la corriente y ese capacitor interno no alcanza a llenarse a tiempo, provocando que el micro lea un voltaje más bajo del real.

10. funcion del capacitor en paralelo con R2

unciona como un pequeño "tanque de reserva" de carga justo en la entrada del ADC para llenarlo al instante cuando muestrea, y de paso forma un filtro pasa-bajas que limpia ruido de alta frecuencia de la batería.