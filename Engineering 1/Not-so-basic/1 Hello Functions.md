# Hello Functions

Functions are one of the most powerful tools in a programmer's toolbox, therefore pretty important for us engineers. In a very simple sense, a function is just quick way to recycle code that you use frequently. And whether you realized it or not, you are already familiar with functions. Your friends print() and sleep() are functions. Let's briefly look at the anatomy of a function. Check out the code below:

```python
def printButtonState(pin):
    buttonState = pin.value # Pin value is either True or False
    if buttonState:
        print('Button is pressed!')
    else:
        print('Button is not pressed.')

```

That little chunk of code is function called `printButtonState` and it will print a line to the serial monitor, telling us what our button is up to. It enables me to execute five lines of code with just one line. Somewhere in my code I just call the function with one line.

```python
printButtonState(button)
```

and my Metro will run the five lines in the function. Cool huh? Let's look at two other parts of a function. First, an argument is something that gives the function info to go on. The argument for the function is the variable inside the parenthesis (or `pin` in the above example). Another important part is `return` functions can return info for the rest of your code to use. The example below returns a string for your main code to use.

```python
def printButtonState(pin):
    buttonState = pin.value
    if buttonState:
        return 'Button is pressed!'
    else:
        return 'Button is not pressed.'
```

This function returns a string when the function is called.  So, later in my code I could say:

```python
print(getButtonState(button))
```

Because the function is accepting any object:

```python
print(getButtonState(myButtonOne))
print(getButtonState(myButtonTwo))
```

with just one function, I can print out the states of two different buttons!

Okay, enough about functions for now. Let's put them to use. Your assignment is to get two new Metro components — the HC-SR04 ultrasonic sensor and the FS90R continuous rotation servo, both pictured below — working and to take advantage of functions in the process.

![servo_hc-sro](/images/servo_hc-sro.jpg)

Now for the tricky part.  Your code must accomplish the following

- You need a function that uses the HC-SR04 to calculate the distance of an object and return that distance in centimeters.
- You must move the servo based on that distance and the servo motion must happen via function or functions.

An example loop function could look something like this:

```python
while True:
    if getDistance(sonar) < 5 :
        moveServo(servo, 1)
    elif getDistance(sonar) < 10 :
        moveServo(servo, 2)
    else
        stopServo(servo)
    sleep(.01)
```

That is just an example. Be creative. The goal is to clean up your loop function, make it readable, and to move reused chunks of code into functions. And remember, Google is your friend.

## Solution

<details><summary>Example Solution</summary>
<p>

```python
from time import sleep
from board import D13, D12, D10
from digitalio import DigitalInOut, Direction
from pulseio import PWMOut
from adafruit_motor.servo import Servo
from simple_hcsr04 import HCSR04

sonar = HCSR04(trigger_pin=D13, echo_pin=D12)

pwm = PWMOut(D10, frequency=50)
myServo = Servo(pwm, min_pulse=750, max_pulse=2250)

def moveServo(servo, direction):
    if direction == 1:
        servo.angle = 180
    elif direction == 2:
        servo.angle = 0

def stopServo(servo):
    servo.angle = 0

while True:
    if HCSR04.distance < 10:
        myServo.angle = 180
    elif HCSR04.distance > 15:
        myServo.angle = 0
    else:
        myServo.angle = 90
    time.sleep(0.01)
```

</p>
</details>
