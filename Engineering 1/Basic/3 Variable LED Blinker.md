# Variable LED Blinker

You're getting the hang of this, right? Let's try this next assignment with minimal help from me. Look at the code below. Your instructions are in the code comments (code comments start with a double slash, #).

## Maybe add a photo for this \/

```python
from board import D13
from digitalio import DigitalInOut, Direction
from time import sleep

led = DigitalInOut(D13)
led.direction = Direction.OUTPUT

delayVar = 2

while True:
    '''
    This is a comment block
    Use led.value and sleep() to make an LED blink
    It should blink on for 2 seconds, then off for 2 seconds
    then on for 1.8 seconds, then off for 1.8 seconds
    then on for 1.6 seconds, then off for 1.6 seconds
    Once it gets to 0.2 seconds, it should keep blinking
    You get the idea...
    Hint: delayVar is a "variable." It can vary.
    Use the Serial Monitor to print the delay times.
    You got this.
    '''
    sleep(.1)
```

Notes:

- Don't just make a bunch of lines of code, one for each time increment. You should always be striving for efficiency in your code. Take advantage of your delayVar variable.
- You might need an if statement to have delayVar stop changing once you get to 0.2 seconds.
- Again, if you're just flying through these assignments, try to challenge yourself. Spice it up. Add a second LED. Print something cool to the Serial Monitor. Be creative.

Last thing:

By now, maybe you can start thinking about commenting your code while you're writing it?

You must address the following questions, but you can add as many comments as you need. Make sure that you explain everything that's new to you, in this assignment.

```python
# You've been using void loop and void setup for a while now.  What's the purpose?
# What's a variable?  How do they make your life easier?
# Why am I forcing you to use your Serial monitor, even though you're sure that your code is going to run perfectly?
# Include a link to the Arduino reference page where you found (and researched) all the different variable types.

# Anything else that you need to remember?
```

## Solution

<details><summary>Example Solution</summary>
<p>

```python
import time
import digitalio
import board

led = digitalio.DigitalInOut(board.D13)
led.direction = digitalio.Direction.OUTPUT

led2 = digitalio.DigitalInOut(board.D5)
led2.direction = digitalio.Direction.OUTPUT

delay = 1
dif = -1

while True:
    if delay == 0:
        dif = 1
    elif delay == 1:
        dif = -1
    delay += dif * .1
    delay = round(delay, 2)
    print(delay)
    led.value = True
    time.sleep(delay)
    led.value = False
    led2.value = True
    time.sleep(delay)
    led2.value = False
```

</p>
</details>
