# Hardware PWM on the MSP430G2553 and MSP430FR2311
Much like the Software PWM, this code was designed for PWM on the LEDs availiable on the boards.  Initially, the LED starts at 50% brightness.  When the button is pressed, it increments by 10%.  Once it reaches 100%, it resets back down to 0%.

## How does this code work?
This utilizes the OUTMOD function of the MSP430; this is why it is considered a 'hardware' PWM.  By setting OUTMOD, CCR1 is enabled toggle/set functionality.  CCR0 is initially set to 1000 and never changes.  UP mode is selected, so the timer counts up to CCR0 and then resets to 0.  CCR1 is initially set to 500 (50% of CCR1).  The MSP430 compares CCR0 and CCR1, if they are the same value, the timer interrupt occurs.  By changing CCR1, the LED's time on and off is changed, thus changing its brightness. 

## Differences bewteen the MSP430G2553 and MSP430FR2311
There only differences between these two boards is the change of register locations.  Otherwise, the code requires little  to no modification.


<!---
# Hardware PWM
Now that you have done the software version of PWM, now it is time to start leveraging the other features of these Timer Modules.

## Task
You need to replicate the same behavior as in the software PWM, only using the Timer Modules ability to directly output to a GPIO Pin instead of managing them in software. One way to thing about what should happen is that unless your are doing some other things in your code, your system should initialize, set the Timer Modules, and then turn off the CPU.

## Deliverables
You will need to have two folders in this repository, one for each of the processors that you used for this part of the lab. Remember to replace this README with your own.

### Hints
Read up on the P1SEL registers as well as look at the Timer modules ability to multiplex.

## Extra Work
### Using ACLK
Some of these microprocessors have a built in ACLK which is extremely slow compared to your up to 25MHz available on some of them. What is the overall impact on the system when using this clock? Can you actually use your PWM code with a clock that slow?

### Ultra Low Power
Using a combination of ACLK, Low Power Modes, and any other means you may deem necessary, optimize this PWM code to run at 50% duty cycle with a LED on the MSP430FR5994. In particular, time how long your code can run on the fully charged super capacitor. You do not need to worry about the button control in this case, and you will probably want to disable all the GPIO that you are not using (nudge, nudge, hint, hint).
--->
