# Debouncing the MSP430G2553 and MSP430F5529
A button is a mechanical component that interfaces with the MSP430.  A button is essentially two metal plates that are brought into contact when the button is pressed, closing the circuit.  A phenomenon that can sometimes occur is called 'bouncing'.  This is where if the button was pressed rapidly, the contacts have a tendency to 'bounce' back and forth.  As one can imagine, this can cause all kinds of issues on the board (ex. one button press can be interpreted as many).  In order to remedy this, a timer is used to delay the time between button press and recognition by the MSP430.  This can effectively negate the bouncing that occurs after the button is pressed.

## How does this code work?
When the button is pressed, the button interrupt is disabled for a short time.  This means that the MSP430 cannot accept any more incoming information from the button until the timer counts up to CCR0.  CCR0 can be set as any value, but 20,000, and an internal divider of 4 was observed to be the best choice for a delay.  This delay isn't percieveable to the human eye, but provides just enough time for the button to stop bouncing.  Also, when the interrupt occurs, the LED is flipped either on or off for a visual comfirmation of whether the button was pressed.

## Differences between the MSP430G2553 and MSP430F5529
The only differences between the boards is their different pin assignemnts.  This can be changed by altering the LED and Button macros located at the top of the code.

<!--- 
# Software Debouncing
In previous labs, we talked about how objects such as switches can cause some nasty effects since they are actually a mechanical system at heart. We talked about the simple hardware method of debouncing, but due to the many different design constraints, you may not be able to add or adjust hardware. Debouncing is also only one of many applications which would require the use of built in Timers to allow for other processes to take place.

## Task
You need to utilize the TIMER modules within the MSP430 processors to implement a debounced switch to control the state of an LED. You most likely will want to hook up your buttons on the development boards to an oscilloscope to see how much time it takes for the buttons to settle. The idea here is that your processor should be able to run other code, while relying on timers and interrupts to manage the debouncing in the background. *You should not be using polling techniques for this assignment.*

## Deliverables
You will need to have two folders in this repository, one for each of the processors that you used for this part of the lab. Remember to replace this README with your own.

### Hints
You need to take a look at how the P1IE and P1IES registers work and how to control them within an interrupt routine. Remember that the debouncing is not going to be the main process you are going to run by the end of the lab.

## Extra Work
### Low Power Modes
Go into the datasheets or look online for information about the low power modes of your processors and using Energy Trace, see what the lowest power consumption you can achieve while still running your debouncing code. Take a note when your processor is not driving the LED (or unplug the header connecting the LED and check) but running the interrupt routine for your debouncing.

### Double the fun
Can you expand your code to debounce two switches? Do you have to use two Timer peripherals to do this?
--->
