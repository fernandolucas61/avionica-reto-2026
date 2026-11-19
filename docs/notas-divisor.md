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

5.Selección de valores comerciales E24

Pendiente:elegir los valores comerciales de R1 y R2 de la serie E24.

La selección deberá cumplir con las siguientes condiciones:
-La resistencia total debe ser mayor a 84 kΩ.
-La relación entre R1 y R2 debe mantener Vout por debajo o igual a 3.0 V cuando Vin sea de 8.4 V.
-Se deben considerar las tolerancias de las resistencias para verificar el peor caso.

Resuelto:
-Relación entre resistencias: R1 / R2 = 1.8.
-Resistencia mínima de R2: R2 > 30 kΩ.
-Resistencia total mínima: Rtotal > 84 kΩ.
-Identificación de 8.4 V como peor caso.

Pendiente:
-Seleccionar R1 y R2 con valores comerciales E24.
-Calcular el voltaje de salida para 6.0 V y 8.4 V.
-Calcular la corriente y la potencia disipada en cada resistencia.
-Determinar la resolución del ADC de 12 bits y su equivalencia en voltaje de batería.
-Analizar la función del capacitor conectado en paralelo con R2.
-Revisar el efecto de la impedancia de salida del divisor sobre la lectura del ADC.