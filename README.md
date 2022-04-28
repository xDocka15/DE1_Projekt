# Morse code reciever

### Team members

* Member 1(responsible for xxx)
* Member 2 (responsible for xxx)
* Member 3 (responsible for xxx)
* Member 4 (responsible for xxx)

### Table of contents

* [Project objectives](#objectives)
* [Hardware description](#hardware)
* [VHDL modules description and simulations](#modules)
* [TOP module description and simulations](#top)
* [Video](#video)
* [References](#references)

<a name="objectives"></a>

## Project objectives

Our project objective is a conversion of morse code signal to decimal numbers and alphabet letters. Representation will be executed on 7-segment display embedded to Nexys-A7-50T circuit board. <br>

By recieving a morse signal either through Arduino microcontroller or switch located on Nexys-A7-50T board we desire to count the lenght of impulse
and then sampling these respective lenghts of signal into dots and dashes, which will undergo further procedure of decoding. 
![Objective](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/Project-Images/ObjectiveIMG1.png)


<a name="hardware"></a>

## Hardware  
#### Nexys-A7-50T

The Nexys A7 board is a complete, ready-to-use digital circuit development platform 
based on the latest Artix-7™ Field Programmable Gate Array (FPGA) from Xilinx®. 
With its large, high-capacity FPGA, generous external memories, and collection of 
USB, Ethernet, and other ports, the Nexys A7 can host designs ranging from introductory combinational circuits to powerful embedded processors. 
Several built-in peripherals, including an accelerometer, temperature sensor, MEMs digital microphone, a speaker amplifier
,and several I/O devices allow the Nexys A7 to be used for a wide range of designs without needing any other components.
<br>
![Nexys-A7-50T](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/Project-Images/NexysA750T.png)<br>
#### Arduino Uno
Arduino Uno is a microcontroller board based on the ATmega328P. 
It has 14 digital input/output pins (of which 6 can be used as PWM outputs), 6 analog inputs, a 16 MHz ceramic resonator (CSTCE16M0V53-R0), 
a USB connection, a power jack, an ICSP header and a reset button.

![Nexys-A7-50T](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/Project-Images/ArduinoUnoFF.png)<br>



<a name="modules"></a>


## VHDL modules description and simulations

### clock_enable.vhd
S_cnt_local represents internal counter which is incrementing every rising edge of the clk clock signal. <br> When s_cnt_local reaches the value of g_MAX, output becomes enabled and s_cnt_local is reset.
 > 1. generates clock signal pulses
 > 2. enables clock signal by counting rising edges
 > 3. outputs the clock enable signal <br>



[Link to clock_enable.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/clock_enable.vhd)
### counter.vhd 
>  1. counts the clock enable impulses
>  2. if counter signal exceedes the limit of numbers it can process, it resets the overflow output
>  3. counter is reset through central reset or sychronous reset from decoder module
>  4. s_LED indicates when s_cnt_local is incremented
  
[Link to counter.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/counter.vhd)
### d_ff_rst.vhd
  >1. d flip-flop with synchronous reset  
  >2. if counter output overflow signal and input signal is low, d_ff_rst resets output 
 
  
  
[Link to d_ff_rst.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/d_ff_rst.vhd)
### d_ff_rst7bit.vhd
Application of 7bit d flip-flop.
  
[Link to d_ff_rst7bit.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/d_ff_rst7bit.vhd)
### decoder.vhd
  >1. takes the lenght of counter output 
  >2. if counter output is less than 3, decoder sets its output to '0', which is represented as dot
  >3. if counter output is more than 3, decoder sets its output to '1', which is represented as dash
  >4. after recieving counter output higher than 7, decoder resets and determines the number of characters recievied, which are then conveyed to its output
  
[Link to decoder.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/decoder.vhd)
### display control.vhd
  >1. assigns characters their display positions
  >2. Internal 3bit counter bin_cnt1 decides which display is to be turned on and assigns respective data to each display.
  
  
[display_control.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/display_control.vhd)
### edge detector.vhd
  >1. detects rising and falling edge of input signal
  >2. output is generated when the input signal changes state
 
  
[Link to edge_detector.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/edge_detector.vhd)
### bin_7seg.vhd
  >1. char_i represents the number of dots and dashes
  >2. with char_i converts bin_i to 7bit 7-segment ready signal, which is saved into 7bit shift register
 
  
[Link to bin_7seg.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/bin_7seg.vhd)
### shift_register.vhd
  >1. stores the dots and dashed obtained in decoder
  >2. shift register is composed of 5 d_ff_rst

  
[Link to shift_register.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/shift_register.vhd)
### shift_register7bit.vhd
  >1. stores 7-segment ready signal for each display
  >2. shift register is composed of 8 7bit d_ff_rst 
 
 
[Link to shift_register7bit.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/shift_register7bit.vhd)
<a name="top"></a>

## TOP module description and simulations

### top.vhd


[Link to top.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/ProjectDS/top.vhd)
### TB_top.vhd
In tb_top we simulate morse code  ("-.. ."), character output is ("d E")  
[Link to tb_top.vhd](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/Project-Images/tb_top.vhd) <br>
[Link to simulation](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/Project-Images/image.png)<br>
[Link to schematic](https://github.com/VadovicSamuel/Digital-Electronics-1/blob/main/Project-Images/schema.png)

<a name="video"></a>
## Video



<a name="references"></a>

## References

1. [Arduino uno](https://www.arduino.cc/en/main/arduinoBoardUno)
2. [Nexys-A7-50T](https://www.xilinx.com/products/boards-and-kits/1-zywan9.html)
3. [Github doc. Ing. Tomáš Frýza Phd.](https://github.com/tomas-fryza/digital-electronics-1)

