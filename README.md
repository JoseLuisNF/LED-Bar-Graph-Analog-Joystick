<a href="https://cooltext.com"><img src="https://images.cooltext.com/5619344.png" width="1050" height="88" alt="LED-Bar-Graph & Analog-Joystick" /></a>

Exposicion de Sistemas Programables

![AHAHAHA](https://user-images.githubusercontent.com/99285798/190015378-798b7335-c80f-464b-a1c7-bc71c640e2d1.png)
----
<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky">Nombre del sensor</th>
    <th class="tg-0pky">Costo del sensor</th>
    <th class="tg-0pky">Lugar donde se encontro</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">LED Bar Graph</td>
    <td class="tg-0pky">$122.54</td>
    <td class="tg-0pky">Ebay</td>
  </tr>
  <tr>
    <td class="tg-0pky">Analog Joystick</td>
    <td class="tg-0pky">$254.38</td>
    <td class="tg-0pky">Shop.Pimoroni</td>
  </tr>
</tbody>
</table>

----
Joystick Analogo

![image](https://user-images.githubusercontent.com/99285798/190511239-eae2feda-4400-4f2c-a572-9b02f31f89c1.png)
Condiciones de Uso:
1. Conectar 5 pines de la pico al joystick
GND a GND (Cualquier pin de tierra)
+5V a 3V3 Out (pin 36). Si, a 5V el Joystick funcionara con el 3V3 con la energia de la pico
VRx a GP27 / ADC1 (pin fisico 32)
VRy a GP26 / ADC0 (pin fisico 31)
SW a GP16 (pin fisico 21). Esto funcionara con la mayoria de los GPI's

2. Iniciar un programa en Micropython IDE
3. Importar los modulos necesarios

from machine import Pin, ADC
import utime

4. Crear variables ejeX y ejeY y asignarlas a los GP en pines 26 y 27

xAxis = ADC(Pin(27))
yAxis = ADC(Pin(26))

5. Crar una variable boton y asignarla a un objeto pin

button = Pin(16,Pin.IN, Pin.PULL_UP)

6. Crear un bucle continuo que revise la impresion de los valores X-Y

while True:
    xValue = xAxis.read_u16()
    yValue = yAxis.read_u16()
    buttonValue= button.value()
    print(str(xValue) +", " + str(yValue) + " -- " + str(buttonValue))
    utime.sleep(0.1)

7. Empezar la ejecucion del codigo y ver los resultados en Mycropython
8. Detener ejecucion
9. Crear variables de estado de X, Y y boton. Colocarlos dentro del bucle, dandole valor default al joystick

xStatus = "middle"
yStatus = "middle"
buttonStatus = "not pressed"

10. Usar If/Else de forma adecuada en los controles
 if xValue <= 600:
        xStatus = "left"
    elif xValue >= 60000:
        xStatus = "right"
    if yValue <= 600:
        yStatus = "up"
    elif yValue >= 60000:
        yStatus = "down"
    if buttonValue == 0:
        buttonStatus = "pressed"
11. Imprimir las variables de estado

print("X: " + xStatus + ", Y: " + yStatus + " -- button " + buttonStatus)

12. Al final el codigo debe de ser similar a esto

from machine import Pin, ADC
import utime

xAxis = ADC(Pin(27))
yAxis = ADC(Pin(26))
button = Pin(16,Pin.IN, Pin.PULL_UP)

while True:
    xValue = xAxis.read_u16()
    yValue = yAxis.read_u16()
    buttonValue = button.value()
    xStatus = "middle"
    yStatus = "middle"
    buttonStatus = "not pressed"
    if xValue <= 600:
        xStatus = "left"
    elif xValue >= 60000:
        xStatus = "right"
    if yValue <= 600:
        yStatus = "up"
    elif yValue >= 60000:
        yStatus = "down"
    if buttonValue == 0:
        buttonStatus = "pressed"
    print("X: " + xStatus + ", Y: " + yStatus + " -- button " + buttonStatus)
    utime.sleep(0.1)

----
LED Bar Graph

![image](https://user-images.githubusercontent.com/99285798/190718306-d688994a-271c-42e2-bb79-d0d63938c3ff.png)

Para la utilizacion del LED Bar Graph es necesario tener una cantidad de resistencias de 22 Ohms, no obstante dada la cantidad de resistencias requeridas se deben de cambiar por un multiresistor para que puedan cubrir todos los puertos del Bar Graph como se muestra en la siguiente imagen

![image](https://user-images.githubusercontent.com/99285798/190718792-453a6b02-527d-45f2-af16-b52bff4f46c4.png)

