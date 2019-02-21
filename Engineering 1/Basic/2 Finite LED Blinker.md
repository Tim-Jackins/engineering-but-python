# Finite LED Blinker

Congratulations. If you got through that last assignment, you are already on your way to becoming a CircuitPython programming expert. That last assignment required a bunch of details:

- Writing CircuitPython code for the first time!
- Using a REPL
- Libraries (time, board, digitalio), functions (sleep), classes (DigitalInOut), variables (led, Direction), loops (while), and conditionals (True, False).
- Realizing that any coding typo can really mess with your day

That's a lot of stuff. We talked about libraries and functions in the first lesson but now let's tackle variables, classes, and conditions.

A variable is a bit of computer memory that you create and name for storing information. Although there are multiple data types, CircuitPython uses a double pointer system too avoid using data type declarations. This makes declaring variables easier.

Examples:

```python
myAge = 16          # This is an integer
myName = "Frank"    # This is a string
pi = 3.14159265     # This is a float
```

As you can see, creating a variable requires you to simply type a name and assign it a value using an equals sign or "assignment operator". While the above variables are declared with simple numbers or letters, there's a more cooler type of variable called an object that can be declared with a class. Classes can also be imported from libraries in the same way that functions can. Classes are used to make variables called objects. These objects are collections of methods, functions related to the objects purpose, and attributes, variables like the ones above related to the objects purpose, used to control something. Wow that was wordsy! For example, CircuitPython uses objects to control the Digital IO and Analog pins on your Metro:

```python
from board import D13                           # Import a pin object
from digitalio import DigitalInOut, Direction   # Import the object for controlling the pin

led = DigitalInOut(D13)                         # Create an object called led for controlling the pin that the LED is plugged into
led.direction = Direction.OUTPUT                # Set an attribute of the led object

print(led.value)                                # Print an attribute of the led object

led.deinit()                                    # Use the method deinit() to free up the pin
```

Now let's learn about conditionals!

A conditional is a statement that can be read by the computer as True or False. Conditional statements check to see if a condition is true, using the if keyword. Below is some valid code. Even if you're totally new to programming, I think you should be able to read it and make sense of what it's doing.

```python
myAge = 16
myAge = myAge + 1

if myAge == 18 :
    print("Just old enough to vote!")
elif myAge < 18 :
    print("Sorry. Gotta wait.")
else:
    print("You're good to go!")
```

Notice a few things:

- When checking to see if two things are equal, you use a double equals, ==.
- If statements use tabs to enclose what you are doing if a certain condition is true.



Your assignment:

1. Make a new Arduino sketch that blinks an LED on and off
2. At the top of your code, after your imports, create a integer variable called counter and set it equal to zero.
3. Use that variable and a conditional statement to stop the LED from blinking once counter reaches a certain number
4. Use the serial monitor to print out the value of counter.

By the way, if you are just crushing these assignments and you want a challenge, try something more complex. Try to have one LED blink 5 times and then have another one blink 5 times or something like that.

Last thing:
After you're done with the assignment, you'll need to go back and comment your code.

The first 3 lines of your code should be, for this and all future programs:

```python
# Title
# Name
# Brief description of what this code is supposed to do.
```

You must address the following questions, but you can add as many comments as you need, in order to prove that you actually know how to do this assignment. You don't need to comment every line, but make sure that you explain everything that's new to you, in this assignment.

For example:

```python
# What does an if statement do?
# Do you always need an else?   What happens if you don't use an else?
# What is the difference between "x++" and "x=x+1"  ?
# What should your Serial Monitor display when your code runs once?
# Fill in the blank: "A single equal sign is used to __________________, and a double equal sign is used to __________________".
# Include a link to the CircuitPython reference webpage that shows all the different types of conditional statements.
# Anything else that you need to remember?
```

## Solution

<details><summary>Example Solution</summary>
<p>

```python
from board import D13
from digitalio import DigitalInOut, Direction
from time import sleep

led = digitalio.DigitalInOut(board.D13)
led.direction = digitalio.Direction.OUTPUT

for i in range(10):
    print('Count value:', i)
    led.value = True
    sleep(.2)
    led.value = False
    sleep(.2)

# or

counter = 0

while True:
    print('Count value:', counter)
    if counter < 10:
        led.value = True
        sleep(.2)
        led.value = False
        sleep(.2)
    else:
        sleep(.4)
    counter += 1
```

</p>
</details>
