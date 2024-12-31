# digital_clock_proteus
A Digital Clock is designed using basic digital logic components from scratch.

# Introduction
In this Open-Handed Problem, a digital clock is designed.
Design Outlines
1.	Use logic gates, flip – flops, latches, multiplexers, demultiplexers and 7 segment displays.
2.	12-hour clock.
3.	Incorporate control for time adjust.
4.	Incorporate control for setting an alarm.

# Components Used
Below is a list of important components used in this design, besides the logic gates AND, OR, and NAND.
J-K Flip Flops (74111):

![image](https://github.com/user-attachments/assets/28a90b62-5ddd-41e7-9c96-c574ed06f80f)

This is the most used component in a digital clock circuit. It is responsible for counting up for the second, minute and hour blocks and is used inside the time adjust control to allow the user to control the digits at the different second, minute and hour locations.
Multiplexers/Demultiplexers (74157):

![image](https://github.com/user-attachments/assets/0e709c0c-d01a-481a-96d8-e7e7b95ee737)

This is an essential component in the making of digital clock. It works alongside other digital circuitry to connect the time adjust counter to the minutes and hours block. If the clock needs to be adjusted, first the mode of clock is changed, this changes the multiplexer from outputting a constant HIGH signal to outputting the time adjust counter’s count (Q0Q1Q2Q3) to the minute or hours block, where it is connected to the preset and clear pins of J-K flip flops, so that the user can adjust the time of clock.
BCD to 7 Segment Decoder (74247):

![image](https://github.com/user-attachments/assets/46d7bcb2-ff9c-4578-892d-bef89debc7ae)

This component is responsible for converting the 4 bit count result from the different second, minute, and hour JK counters and converting it to output suitable for a Common Anode 7 Segment.
Latch (74373):

![image](https://github.com/user-attachments/assets/14ec15f0-1084-4329-a439-a3c624a889c9)

This is responsible for latching the adjusted time for the minutes and hours flip flops. This is used so that the adjusted time stays still, till the mode of the clock is changed from the time adjust mode to normal mode. 

# Block Diagram

![image](https://github.com/user-attachments/assets/11a95f02-756d-4bcd-8088-54056835e28d)

Time Adjust counter counts from 0 to 9 and it is a controlled counter. Two inputs are fed into this block, one for incrementing, and one for mode of clock. 8 outputs are taken out of this block, 4 for presets and 4 for clear signal.
Demultiplexer has two inputs fed to it beside the 8 from the previous block. These, two inputs are responsible for selecting whether the time adjust is connected to minutes, or hours block.
By selecting the right configuration for the demultiplexer, a block is adjusted in time, and this is how time would be adjusted for the minutes and hours block.
The Seconds Counter counts from 0 to 59 with the help of mod 10 and mod 6 counters. The two counters are connected in a way that the reset signal of mod 10 counter, both, resets the mod 10 counter and increments the mod 6 counter. In this way, the seconds block counts from 0 to 59 in 59 seconds.

The seconds/minutes/hours counter have 8 JK flip flops that perform this, when the count is at 60, a clear signal is sent to restart the seconds counter and increment the minutes counter.
The Hour Counter counts from 0 to 12, this is made possible by using 8 JK flip flop. When the count is at 09, the units digit is reset and the tens digit is incremented, and when the count for the tens digit is 1 and the units digit is 2, the hours block is completely reset.

Display consists of 6, 7 segment led displays, they are connected to the seconds, minutes and hours block.
After the clock and it’s time adjustment control has been established, the complete system is duplicated beside it, with the slight change of removed clock signal, unnecessary connections between the JK flip-flops and added switches and controls for setting an alarm.
This replicated block is then used to set the seconds, minutes and hours digits, much like the time adjustment control that was constructed earlier. Once the alarm is set, the 4-bit outputs of these blocks are compared with the clock constructed earlier, using XNOR gates and, AND gates. If both of them are same a HIGH signal is sent as an output and fed to the alarm control, which sets off the alarm.

# Schematic
# Complete Diagram:

![image](https://github.com/user-attachments/assets/4c837db2-ea44-4acc-990e-5c2b6c36dbbf)

# Time Adjust Counter:

![image](https://github.com/user-attachments/assets/f9f634dc-a115-4c82-b1ba-48727c683870)

The Increment Switch counts up when at HIGH, and stops counting when LOW. The Mode Switch runs the clock normally when HIGH and in time adjust mode when LOW. There are 9 outputs, 8 of them are the preset and clear signal for the JK flip flops ahead, while the clock CLK* signal is an input for the clock signal that runs the clock at a period of 1 second.

# Time Adjust Counter – Child Sheet:

![image](https://github.com/user-attachments/assets/a8c3e000-b0de-4f08-8e7a-94c458324e44)

Inside of this block is a JK flip flop counter that counts from 0 to 9 and resets at 10 (1010) count. The 4-bit output from the 4 JK flip flops is fed to Multiplexers that output the preset and clear signals, which makes a total of 8 outputs. These 8 outputs are first fed into the circuit on the left. The circuit on the left is responsible for either giving out a HIGH or giving out the preset and clear signals, which is controlled by the CON input from outside of this block.

# MUX – Child Sheet:

![image](https://github.com/user-attachments/assets/b73020a2-aedd-4fe7-b2dc-923538aa4281)
![image](https://github.com/user-attachments/assets/27b09b53-b21c-4648-9a00-2178cce97820)

This multiplexer connected with the 4-bit outputs of the Time adjust counter JK flip flops are responsible for giving out the appropriate signals for Preset and Clear Signals. The ‘E’ signal is connected to the ‘Q’ output of the JK flip flop and ‘H’ is kept HIGH constantly, when Q is LOW, the outputs ‘S’ and ‘R’ are HIGH and LOW respectively.

# Demultiplexer Block:

![image](https://github.com/user-attachments/assets/f6fb6998-6d0a-42b4-8850-e22da379c62f)

This is the demultiplexer responsible of connecting the time adjust outputs to the different Seconds, Minutes and Hours blocks. There are 3 inputs sent to this Demultiplexer block besides the 8 outputs of the previous block.
The ‘A’ and ‘B’ input are responsible for controlling whether the 8 time adjust inputs are connected with the minute’s digits or hours digits.
The CONTROL input is responsible for letting the Demultiplexer know whether the mode of clock is set to time adjust or normal, if it is set to time adjust, then the demultiplexer operates, if not, then all the outputs of this block give out constant HIGH.

# Demultiplexer – Child Sheet:

![image](https://github.com/user-attachments/assets/4830c847-779a-4660-b59b-b05038a8f514)

The circuitry of the child sheet replicates the operation of a demultiplexer, the 8 inputs are connected with the AND gates to which ‘A’ and ‘B’ inputs are accordingly. This results in 32 outputs from this block, which are then fed to 74157 demultiplexer TTL ICs, which are responsible for either outputting the demultiplexer outputs or giving out HIGH, controlled by the CONTROL input.

# Seconds, Minutes and Hours Counter Blocks:

![image](https://github.com/user-attachments/assets/a46068a6-1485-41af-8b6e-73d7710174d6)

These 5 blocks are responsible for counting in the clock sequence. From 0 to 59 and 0 to 12.
The first seconds block counts from 0 to 9, at the 10th count it resets and sends a HIGH signal to the next block, which increments the count from 0 to 1. The second second’s block counts from 0 to 5 in this way and then resets and sends a HIGH signal to the minutes block.
The minute’s block does the same as above and hours block does it a little differently, since it counts from 0 to 12.

# Hour’s Block – Child Sheet:

![image](https://github.com/user-attachments/assets/58c218d7-ed1d-4923-983d-0dc832c5ba60)

In this block we have 8 JK flip flops, the first 4 count from 0 to 9 and resets at the 10th count, the second 4 flip flops, count from 0 to 1 and reset at the 2nd count, when the count of the first four flip flop is 3 and the count of the second four flip flop is 1, all 8 JK flip flops reset.
There are four latches used here, so that the preset and clear signals don’t vanish when the time adjusted is shifted from one digit to the other.

# Simulation
# Running the simulation:

![image](https://github.com/user-attachments/assets/dcf97cd6-603b-4760-b5d9-974283c1def9)
![image](https://github.com/user-attachments/assets/468bd3a8-1c2d-4fda-8091-f341de0cf1eb)
![image](https://github.com/user-attachments/assets/215b65c7-e70c-4ea2-8d8f-799d06172218)

# After left running a couple of seconds, the second 1st digit resets:

![image](https://github.com/user-attachments/assets/35a4d799-0048-4f14-b2ac-5b5341fb3c30)
![image](https://github.com/user-attachments/assets/48503d2f-d8db-4902-9b76-6d5b65f6a81d)

# Seconds to Minutes Increment:

![image](https://github.com/user-attachments/assets/f68b4b8a-8538-4427-9531-a7d3f08153b7)
![image](https://github.com/user-attachments/assets/e51bde75-5aa7-452c-9565-3d9f54bda7d7)

# Minutes to Hours Increment:

![image](https://github.com/user-attachments/assets/fcbe1bca-fd48-4774-ac64-0fd3b551ccd9)
![image](https://github.com/user-attachments/assets/c2a20317-2ca4-4c5c-adfb-f4f86b1e2284)

# Clock Reset:

![image](https://github.com/user-attachments/assets/b35d8822-cb32-4105-8c1d-ac3254b063ac)
![image](https://github.com/user-attachments/assets/e02cd0cc-b370-4514-ae39-b66d5972e477)
