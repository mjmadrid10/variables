Program Analysis
 
The 'SW2Count' variable is created within RAM as an 8-bit memory location by the declaration: 'unsigned char SW2Count = 0;' What is the the maximum value an 8-bit variable can store? What are some of the benefits and drawbacks of using 8-bit variables in an 8-bit microcontroller?
 
The maximum value that an 8-bit variable can store is 225. An advantage of using an 8-bit variable in an 8-bit microcontroller is that if the amount of data is less than 225, the speed will be fast. Although, a disadvantage of using an 8-bit variable in a 8-bit microcontroller is that there is a certain limit the value can go up to.
 
The constant 'maxCount' is defined using a declaration similar to that used for the SW2Count variable, but with the 'const' prefix added in the declaration. Can you think of some advantages of declaring a constant like this, using a separate statement above the main code, rather than just embedding the value of the constant where it is needed in the code?
 
It is much more efficient than just changing a variable in every single code.
 
This program should light LED D3 every time SW2 is pressed, and light LED D4 once the count reaches 50. Try it, and count how many times you have to press the button until LED D4 turns on. SW3 resets the count so you can perform repeated attempts. Did your count reach 50? Can you describe what the program is doing?(Hint: try pressing and releasing the button at different rates of speed.)
 
It did not meet my reach count of 50 as it only reached a maximum of 5 counts. This program allows you to press SW2 a few times at a lower speed but the value increases as the speed increases.
 
Modify the second 'if' structure to add the else block, as shown below:
       if(SW2Count >= maxCount)
       {
           LED4 = 1;
      }
       else
       {
           LED4 = 0;
       }
Now, press and hold pushbutton SW2 for at least 10 seconds while watching LED D4. LED D4 should stay on continuously while the value of SW2Count is higher than maxCount. If LED D4 turns off, what can you infer about the value of the SW2Count variable? Can you explain what happens to the SW2Count variable as the SW2 button is held?
 
I can infer that the value of SW2Count is lower than maxCount as SW2Count would be increasing by a value of 1.
 
We can set a limit on the SW2Count variable by encapsulating its increment statement inside a conditional statement. In your program, replace the line 'SW2Count = SW2Count + 1;' with the code, below:
           if(SW2Count < 255)
           {
               SW2Count += 1;
           }
 
This code demonstrates the use of the assignment operator '+=' to shorten the statement 'SW2Count = SW2Count + 1;' The same operation is performed,but in a more compact form. After adding this code, what is the maximum value that the SW2Count variable will reach? How does this affect the operation of LED D4 when SW2 is held?
 
LED D4 remains on as the maximum value that can be reached is 254.
 
The fundamental problem with this program is that pushbutton SW2 is sense in each cycle of the loop, and if its state is read as pressed, another count is added to the SW2Count variable. The program needs to be made to respond only to each new press, rather than just switch state -- in other words, to a *change* of SW2 state, from not-pressed to pressed. Doing this requires the use of another variable to store the prior state of SW2, so that its current state can be evaluated as being the same, or different from its state in the previous loop. Replace the initial if-else condition with the following two if conditions:
 
// Count new SW2 button presses
       if(SW2 == 0 && SW2Pressed == false)
       {
           LED3 = 1;
           SW2Pressed = true;
           if(SW2Count < 255)
           {
               SW2Count = SW2Count + 1;
           }
       }
 
       // Clear pressed state if released
       if(SW2 == 1)
       {
           LED3 = 0;
           SW2Pressed = false;
       }
These two if conditions make use of the Boolean SW2Pressed variable to store the current state of SW2 for the next cycle of the main while loop. Boolean variables can store 0/false or 1/true, interchangeably. The first if condition, above, compares the current SW2 state with the previously stored SW2Pressed variable so that a new count is only added when the SW2 button is pressed and SW2Pressed is false. In the if structure, SW2Pressed is set to true before a count is added. The following if structure resets SW2Pressed to false when the button is released. Try the code to verify that it works.
 
The conditional statement in the first if condition can also be written:
 
       if(SW2 == 0 && !SW2Pressed)
 
‘!SW2Pressed’ is equivalent to SW2Pressed being false, and is not read at ‘not SW2Pressed’. Using the variable ‘SW2Pressed in a condition will be equivalent to the statement being true.
 
A pushbutton's logic state can also be defined as a word in a similar way to a variable (eg. the way SW2Pressed represents 1 or 0, or true or false)which can help to make the code more readable. Add the following lines to the 'Program constant definitions' section at the top of the code:
 
 // Count new SW2 button presses
      	if(SW2 == pressed && SW2Pressed == false)
       {
           LED3 = 1;
           if(SW2Count < 255)
           {
               SW2Count = SW2Count + 1;
           }
           SW2Pressed = true;
       }
 
       // Clear pressed state if released
       if(SW2 == notPressed)
       {
           LED3 = 0;
           SW2Pressed = false;
       }
      

Programming Activities

Can you make a two-player rapid-clicker style game using this program as a starting point? Let's use SW5 for the second player's pushbutton so that the two players can face each other from across the UBMP4 circuit board.Duplicate SW2Count and SW2Pressed to create SW5Count and SW5Pressed variables. Then, duplicate the required if condition structures and modify the variable names to represent the second player. LED D4 can still light if player 1 is the first to reach maxCount. Use LED D5 to show if the second palyer wins. Use a logical condition statement to reset the game by  clearing the count and turning off the LEDs if either SW3 or SW4 is pressed.

// Count new SW2 button presses
      if(SW2 == 0 && SW2Pressed == false)
      {
          LED3 = 1;
          SW2Pressed = true;
          if(SW2Count < 255)
          {
              SW2Count = SW2Count + 1;
          }
      }
    
// Count new SW2 button presses
       if(SW2 == pressed && SW2Pressed == false)
       {
           LED3 = 1;
           if(SW2Count < 255)
           {
               SW2Count = SW2Count + 1;
           }
           SW2Pressed = true;
       }
 
       // Clear pressed state if released
       if(SW2 == notPressed)
       {
           LED3 = 0;
           SW2Pressed = false;
       }


Use your knowledge of Boolean variables and logical conditions to simulate a toggle button. Each new press of the toggle button will 'toggle' an LED to its opposite state. (Toggle buttons are commonly used as push-on, push-off power buttons in digital devices.)

if(SW2Count >= maxCount)
       {
           LED4 = 1;
       }
       else
       {
           LED4 = 0;
       }
 
      // Reset count and turn off LED D4
       if(SW3 == 0)
       {
           LED4 = 0;
           SW2Count = 0;
       }
 
 
   
        // Count new SW5 button presses
       if(SW5 == pressed && SW5Pressed == false)
       {
           LED6 = 1;
           if(SW5Count < 255)
           {
               SW5Count = SW5Count + 1;
           }
           SW5Pressed = true;
       }
 
       // Clear pressed state if released
       if(SW5 == notPressed)
       {
           LED6 = 0;
           SW5Pressed = false;
       }
 
if(SW5Count >= maxCount)
       {
           LED5 = 1;
       }
       else
       {
           LED5 = 0;
       }
 
      // Reset count and turn off LED D4
       if(SW4 == 0)
       {
           LED5 = 0;
           SW5Count = 0;
       }
 
       // Add a short delay to the main while loop.
       __delay_ms(10);
      
       // Activate bootloader if SW1 is pressed.
       if(SW1 == 0)
       {
           RESET();
       }
   }
}


A multi-function button can be used to enable one action when pressed, and a second or alternate action when held. A variable that counts loop cycles can be used to determine how long a button is held (just as the first program unitentionally did, because of the loop structure). Make a multifunction button that lights one LED when a button is pressed, and lights a second LED after the button is held for more that one second.

// Count new SW2 button presses
      if(SW2 == 0 && SW2Pressed == true)
      {
          LED3 = 1;
          SW2Pressed = true;
          if(SW2Count < 255)
          {
              SW2Count = SW2Count + 1;
          }


Do your push buttons bounce? Switch bounce is the term that describes switch contacts repeatedly closing and opening before settling in their final (usually closed) state. Switch bounce in a room's light switch is not a big concern, but switch bounce can be an issue in a toggle button because the speed of a microcontroller lets it see each bounce as a new, separate event. Use a variable to count the number of times a pushbutton is pressed and display the count on the LEDs. Use a separate pushbutton to reset the count and turn off the LEDs so that the test can be repeated. To determine if your switches bounce, try pressing them at various speeds and using different amounts of force.

Yes, my push buttons do bounce.

Did your pushbuttons bounce? Can you think of a technique similar to the multi-function button that could be implemented to make your program ignore switch bounces. Multiple switch activations within a 50ms time span might indicate switch bounce and can be safely ignored.

No, my push buttons did not bounce. Bouncing occurs in a split second. We can tell the program to ignore it, but if it keeps occurring, then we would tell the program to look at it.
