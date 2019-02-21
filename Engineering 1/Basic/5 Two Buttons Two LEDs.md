# Two Buttons Two LEDs

Pretty straightforward.

You have two buttons on your breadboard and two LEDs.

Pressing one button lights (or blinks; your call) one LED.  Pressing the other button lights (or blinks; your call) the other LED.

Things to keep in mind:

- Mount your buttons firmly in the center of your breadboard.
- Your life will be easier if you wire 5V to the positive row of the breadboard and wire GND to the negative row, as seen below.
- You are actually wiring 4 separate circuits for this assignment, 2 LED circuits, and 2 button circuits
- Never wire LEDs without a resistor. Usually 220Ω.
- Finally, this is not as hard as it seems. Didn't you just wire up a button, last assignment? Just do it twice!

This assignment isn't anything new, just a doubling of the last assignment. You got this.

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

led2 = digitalio.DigitalInOut(board.D12)
led2.direction = digitalio.Direction.OUTPUT

button2 = digitalio.DigitalInOut(board.D4)
button2.direction = digitalio.Direction.INPUT
button2.pull = digitalio.Pull.DOWN


while True:
    if button.value:  # button is pushed
        led.value = True
    else:
        led.value = False

    if button2.value:  # button is pushed
        led2.value = True
    else:
        led2.value = False

    time.sleep(0.01)
```

</p>
</details>
