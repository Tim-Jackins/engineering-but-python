# Button-Activated LED

In this assignment, you will wire up a button to blink an LED.  When you push the button, the LED starts blinking. When you release the button, the LED is off. Also, while the button is pressed and the LED is blinking, the serial monitor should be saying something.

A diagram of the circuit is below.  Notice it's really two separate circuits.  In the first circuit, connect one pin (in my picture, I chose pin 2) to an LED then through a 220Ω resistor to ground. That way, setting the value of pin 2 True or False turns the LED on or off.

Next, simply connect another pin (I chose pin 12) to a button. That pin also needs to be "pulled down" to ground using a 10kΩ resistor. The other side of the button should be connected to 5V. So, when the button is pressed, I can use `button.value` to tell it's been pressed and switch the LED state. Note: mount your button firmly in the center of your breadboard.

![button_led](/images/button_activated_led.jpg)

Your code could start something like this:

button_code.png

Here's a circuit schematic:

![button_and_led_schematic](/images/button_and_led_schematic.png)

There's a good chance your brain just looked at those two schematics above and went "Well, that looks crazy; I'm just going to ignore that." Totally normal response. But before you move on, take a second to ponder those diagrams.  

On the left, you've got an Metro pin going to a resistor (zig-zag lines) to an LED (circled triangle symbol with light shooting out of it) to ground (three lines of decreasing size). When the Arduino pin is HIGH, the pin goes to 5 Volts and current will run through the resistor, through the LED, to ground and the LED will light up.

In the diagram on the right, we have an Metro pin connected, or "pulled down" to ground via a resistor (zig-zag lines).  In that situation, the Metro pin will read `False`. But when the button is pressed, the Metro will be on the 5-Volt side of the resistor and read `True`. Not so crazy, right?

Again, if you're just blowing through these assignments, try a challenge: instead of having the LED only be on when the button is pressed, see if you can make the button toggle the LED on and off. i.e., one press turns it on and a second press turns it off.

## Solution

<details><summary>Example Solution</summary>
<p>

```python
import time
import digitalio
import board

led = digitalio.DigitalInOut(board.D13)
led.direction = digitalio.Direction.OUTPUT

button = digitalio.DigitalInOut(board.D5)
button.direction = digitalio.Direction.INPUT
button.pull = digitalio.Pull.DOWN

while True:
    if button.value:  # button is pushed
        led.value = True
    else:
        led.value = False
 
    time.sleep(0.01)
```

</p>
</details>
