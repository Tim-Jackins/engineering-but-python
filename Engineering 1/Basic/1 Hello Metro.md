# Hello Metro

Meet your new best friend, the Metro M0 Express. The Metro is like a little computer, complete with a central processing unit (CPU), flash storage, and memory. Like other microcontrollers (little computers), the Metro has several methods of interfacing with the outside world. Those 14 holes on the top side labeled Digital are called pins and are good for output (controlling things like motors, lights, etc.) as well as input (reading sensors and other devices). The bottom side has 6 analog input pins, labeled Analog In. Digital pins are binary, either on or off but, the analog pins can be lots of different values. The hardware that really sets this microcontroller apart is both a built in rainbow led light (commonly called a neopixel) and an ATSAMD21G18 chip capable of interpreting CircuitPython!

![Metro M0](/images/metro_m0.png)

On the top left side, you'll see a USB port. That USB port is super important.  It's how you will get code from your computer to your Metro. It is also how the Metro will send data back to your computer. USB stands for Universal Serial Bus. A bus is something that computers use to send data back and forth. Serial means it can only handle traffic in one direction at a time, computer to Metro or vice versa. And it's universal because USB cables are freaking everywhere!

Serial Data.png

The language we're going to using is called CirctuiPython. CircuitPython is a fork of MicroPython; a lean version of a language called Python. Python is what coders call an interpreted language. This means that programs written in this language are a tad slower then compiled languages but they are astronomically easier to debug (find problems in) and revise.

![Mu](/images/mu.png)

Let's get started controlling the Metro. Take your Metro and plug it into your computer using the cable in your box. When you plug it in the Metro will appear on your computer as a flash drive called `CIRCUITPYTHON`. If the drive appears in a different simply hit the reset button on the Metro. Now open Mu. Mu is a text editor made to work with CircuitPython and comes with some handy tools built in. One of these tools is a REPL. REPL stands for read-eval-print-loop. Basically you can give the Metro commands, like you would in a program, and it executes them. We're going to use the REPL to run our first piece of code on the Metro!

With Mu open click on the Serial button on the top tool bar. Next click inside the REPL area and press any key. This will yield something like this:

```python
Adafruit CircuitPython 3.1.2 on 2019-01-07; Adafruit Metro M0 Express with samd21g18
>>>
```

and the neopixel on your Metro will turn white (to let you know it's in REPL mode).

Now type:

```python
print('Hello World')
```

The Metro got your command, interpreted it, and then executed it printing out `Hello World` below where you typed it and prompting you for another command.

Now let's actually write a program. In the text area of Mu write this:

```python
from time import sleep

while True:
    print('Hello World!')
    sleep(.1)
```

Doesn't look too complicated. What is this program doing? First, it's importing the function `sleep` from the library `time`. What the heck does that mean?! Think of the libray as a toolbox full of condensed guides (functions) that simplify common, but complicated, tasks. Next it begins a while loop. The `True` in this line means that the loop will run forever. The two lines indented under the `while True:` are what the while loop will be running. But what is `while True:` running over and over again? This probably a good place to talk about nesting. Let's take the lines `print('Hello World')` and `sleep(.1)` for example. They are both indented one higher than `while True:` which means the two lines are *nested* in the while loop. The while will run every thing nested in it for as long of the condition, `True`, remains true. In this case forever. The nested functions printing `Hello World` and wait for .1 seconds before doing it again. The `sleep` line is very important because the without it the Metro will run this code millions of times per second and the Serial monitor will start glitching.

Now that you have code in the text area, click the save button, and save the file as shown in the photo:

![How To Save](/images/how_to_save.png)

Now look inside the REPL area. The Metro automatically sensed the new file and is now running it. You should be seeing it print `Hello World` back at you!

Check out the neopixel; it's green!

now let's add a mistake for the sake of testing: change `print('Hello World!')` to `prin('Hello World!')`. Click the save button and watch what happens. What's that crazy pixel doing? It should be holding green, switching to white, and then blinking yellow. This means there's an error and the LED is telling you what error!

- *GREEN*: `IndentationError`
- *CYAN*: `SyntaxError`
- *WHITE*: `NameError`
- *ORANGE*: `OSError`
- *PURPLE*: `ValueError`
- *YELLOW*: other error

we got white so that means we got a `NameError`. Now let's check the REPL which should look like this:

```repl
Traceback (most recent call last):
  File "<stdin>", line 4, in <module>
NameError: name 'prin' is not defined
```

The REPL confirms the type of error and tells you what line the error is on! Pretty handy.

So far, so good, but Engineering class isn't about mindlessly following directions on Canvas. It's about problem solving. It's about using your resources to figure things out. So, here's your first challenge. Keep the code you have, but add some code to your sketch to do the following:

- Instead of "Hello World" have the Serial Monitor print "Blink"
- Instead of waiting .1 seconds have your loop run every once every second

Now the fun part. Use an LED, a 220 Ω resistor (Red Red Brown), and some wires to have an LED turn on for a second, off for a second, on for a second, and so on.

*Hints:*

1. For that last part, you'll need some more toolboxes: one with tools for with pins and the other for dealing with digital values. The toolboxes you need to import are `board` and `digitalio`.
2. LEDs care which side is connected to 5V and which side is connected to ground.
3. Google is your friend, I'd start with something like `How to make an LED blink with circuitpython`.

One last thing: let's develop a good habit now and save this program in your student network drive. Go to your Metro's drive (CIRCUITPY) and copy the `code.py` file you just made to your Student Drive (H:) and rename it to `hello_metro.py`.

Okay, actually this is the last thing:
After you're done with the assignment, and have shown me a cool blinking Metro, you'll need to go back and comment your code, explaining what it actually does. To start a comment on a line simply type a `#` symbol. Mu will grey out everything past the `#` and the CircuitPython interpreter will ignore it.

Open up the `hello_metro.py` and add some comments address the following questions, but you can add as many comments as you need, in order to prove that you actually know how to do this assignment.

You don't need to comment every line, but make sure that you explain everything that's new to you, in this assignment.

```python
# What is a library?
# What is a function?
# How do you get the LED to blink on pin 9, instead of pin 13?
# Fill in the blank: "The bigger your sleep gets, the _______ the blinking becomes"
# Anything else that you need to know?
```

The reason we're forcing you to comment your code is that well documented code makes your life easier. It will help you or anyone who reads your code to understand what's going on, and why you chose to do certain things. Tomorrow, someone may ask to look at your code, or maybe you revisit this code in a month, when you start some cool project, and totally forget how to make an LED blink.

## Solution

<details><summary>Example Solution</summary>
<p>

```python
from board import D13
from digitalio import DigitalInOut, Direction
from time import sleep

led = DigitalInOut(D13)
led.direction = Direction.OUTPUT

while True:
    print('Blink')
    led.value = True
    sleep(.5)
    led.value = False
    sleep(.5)
```

</p>
</details>
