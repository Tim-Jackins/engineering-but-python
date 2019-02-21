# Servo Control

You are about to graduate from Basic Metro. Congrats! This last assignment throws in a servo (a little motor).

Pretty straightforward. Just like the last assignment, your circuit uses two buttons. But this time, instead of lighting LEDs, you will be controlling a servo. Pressing and holding one button causes the servo to rotate in one direction. Pressing and holding the other button causes the servo to rotate in the other direction.

That's it.

Note: in order to control a servo, you're going to need some more tools. To control a servo you need to send it fast electronic pulses. To do that we need to import the class `PWMOut` from the library `pulseio`. So that you don't have to send those pulses manually, you should also import the class `Servo` from the library `adafruit_motor.servo`.

With the servo library import and pwm / servo object initialization, you can move a servo with something as simple as `servo.value = 180`.

I would recommend making your code should look something like this at the top:

```python
from time import sleep
from digitalio import DigitalInOut, Direction, Pull
from board import D5, D6, D10
from pulseio import PWMOut
from adafruit_motor.servo import Servo

pwm = PWMOut(D10, frequency=50)
myServo = Servo(pwm)

button1 = DigitalInOut(D5)
button1.direction = Direction.INPUT
button1.pull = Pull.DOWN

button2 = DigitalInOut(D6)
button2.direction = Direction.INPUT
button2.pull = Pull.DOWN

while True:
    if button1.value:
        print('Button 1 press')
    elif button2.value:
        print('Button 2 press')
    sleep(0.1)
```

The lines right under the imports create a pwm object which is then used to make a servo object. Inside the `while` loop I have an `if` and an `elif` reading both button states and printing values repectively. That isn't the whole program! But, it gets you started and it lets you test to see if you have your buttons wired correctly, which is huge.

That last statement bears repeating. As your programs and circuits get more complex, you will want to build them in small steps and test every step of the way. Please, please, please don't ask me why your circuit isn't working until you've used `print()` or the REPL to do some debugging. Not that I don't love helping, but debugging is one of the best skills you will ever learn.

![180_servo](/images/180_servo.jpg)

Two final notes:

- You'll want to use headers (in the parts bins) to wire it up.
- Red = positive; Brown = Ground; Orange = signal

## Solution

<details><summary>Example Solution</summary>
<p>

```python
from time import sleep
from digitalio import DigitalInOut, Direction, Pull
from board import D5, D6, D10
from pulseio import PWMOut
from adafruit_motor.servo import Servo

pwm = PWMOut(D10, frequency=50)
myServo = Servo(pwm)

button1 = DigitalInOut(D5)
button1.direction = Direction.INPUT
button1.pull = Pull.DOWN

button2 = DigitalInOut(D6)
button2.direction = Direction.INPUT
button2.pull = Pull.DOWN

while True:
    if button1.value:
        print(180)
        myServo.angle = 180
    elif button2.value:
        print(0)
        myServo.angle = 0
    else:
        myServo.angle = 90

    sleep(0.01)
```

</p>
</details>