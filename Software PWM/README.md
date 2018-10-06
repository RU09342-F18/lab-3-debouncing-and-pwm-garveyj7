# Software PWM on the MSP430G2553 and MSP430FR2311
This code uses the capture compare registers (CCRn's) on the MSP430 to produce PWM.

Initially, the LED starts at 50% brightness.  When the button is pressed, the brightness of the LED increases by 10%.  When the brightness reaches 100%, the LED goes down to 0%.

## How does it work?
This code utilizes the capture compare registers (CCRn's) on the MSP430s.  By comparing the two, the MSP can decide when to output a high, and when to output a low.  By periodically switching between high and low, a PWM signal is created.

CCR0 is defined as 1000 and remains constant throughout the code.  CCR1 is initially set as 500 in order to produce an initial 50% duty cycle (500 is 50% of 1000).  When the button is pressed, CCR1 increments by 100 (10% duty cycle of CCR0).

When the code runs, the CPU only active when the button is pressed.  Else, if the button isn't pressed, the CPU remains asleep, saving power.

Macros were used to define the LED and Button bits.  This is helpful when converting the code to another board because changing two lines of code is far easier than changing all of the bits individually.

## Changes between the boards
The main difference between the boards is that the G2553 uses the timer A module while the FR2311 uses the timer B module.  Otherwise, the register locations change from board to board because the buttons and LEDs are on different ports.

<!--- # Software PWM
Most microprocessors will have a Timer module, but depending on the device, some may not come with pre-built PWM modules. Instead, you may have to utilize software techniques to synthesize PWM on your own.

## Task
You need to generate a 1kHz PWM signal with a duty cycle between 0% and 100%. Upon the processor starting up, you should PWM one of the on-board LEDs at a 50% duty cycle. Upon pressing one of the on-board buttons, the duty cycle of the LED should increase by 10%. Once you have reached 100%, your duty cycle should go back to 0% on the next button press. You also need to implement the other LED to light up when the Duty Cycle button is depressed and turns back off when it is let go. This is to help you figure out if the button has triggered multiple interrupts.

## Deliverables
You will need to have two folders in this repository, one for each of the processors that you used for this part of the lab. Remember to replace this README with your own.

### Hints
You really, really, really, really need to hook up the output of your LED pin to an oscilloscope to make sure that the duty cycle is accurate. Also, since you are going to be doing a lot of initialization, it would be helpful for all persons involved if you created your main function like:

```c
int main(void)
{
	WDTCTL = WDTPW | WDTHOLD;	// stop watchdog timer
	LEDSetup(); // Initialize our LEDS
	ButtonSetup();  // Initialize our button
	TimerA0Setup(); // Initialize Timer0
	TimerA1Setup(); // Initialize Timer1
	__bis_SR_register(LPM0_bits + GIE);       // Enter LPM0 w/ interrupt
}
```

This way, each of the steps in initialization can be isolated for easier understanding and debugging.


## Extra Work
### Linear Brightness
Much like every other things with humans, not everything we interact with we perceive as linear. For senses such as sight or hearing, certain features such as volume or brightness have a logarithmic relationship with our senses. Instead of just incrementing by 10%, try making the brightness appear to change linearly.

### Power Comparison
Since you are effectively turning the LED off for some period of time, it should follow that the amount of power you are using over time should be less. Using Energy Trace, compare the power consumption of the different duty cycles. What happens if you use the pre-divider in the timer module for the PWM (does it consume less power)?
--->
