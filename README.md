# UART-PROTOCOL
##  Raj Kumar Laldev 
 Advance VLSI Lab  Silicon institute of technology Bhubaneswar,India  
 rajbihar5364@gmail.com
 # Table of Contents
 - [Introduction](#Introduction)
  * [Application Background]()
- [UART protocol data flow]()
- [How UART works]()
   * [Verilog Implementation]()
   * [Baud rate generate]()
- [Design of UART transmitter]()
  * [Transmitter  state machine]()
  * [Verilog implementation of state machine]()
- [Design of UART receiver]()
  * [Receiver state machine]()
  *  [Verilog implementation of state machine]()
- [Oversampling procedure]()
-  [Results]()
-  [Conclusion]()
- [Acknowledgement]()

# Introduction
Protocol: A set of rules and regulations is called a
protocol. Different type of protocols are available.
1.  Bus protocol: APB,AHB,AXI,ASB,ACE 
2. Peripheral protocol.
- High speed: PCIe, SATA, SAS, Ethernet, USB, MIPI.
- Low speed :UART,SPI,I2C.

   **Single wire connection** ![Alt](img1.jpg)

- One of the biggest challenge in SOC design is the on chip communication between the different components.
-  The different bus protocols used for interconnection .
-  Most of the times, the IP cores are designed with many different interfaces and communication protocols and this can be a problem while integrating into an SOC. 
- To avoid this problem, standard on-chip bus structures and protocols were developed. Exchange of information from one system to another system with a medium is called communication.
-  A set of rules and regulations that allow two electronic devices to connect to exchange the data with one and another. 
-  Universal asynchronous receiver-transmitter (UART) is one of the simplest and oldest forms of device-todevice digital communication. You can find UART devices as a part of integrated circuits (ICs) or as individual components.
-   UART stands for a universal asynchronous transmitter and receiver. 
-  UART Protocols is a serial communication with two wired protocols. 
- The data cable signal lines are labelled as Rx and Tx.
-   Serial communication is commonly used for transmitting and receiving the signal.

 **System on chip**   ![Alt](img2.jpg)

- It is transferred and receives the data serially bit by bit without class pulses. 
-  The UART takes bytes of data and sends the individual bits in a sequential manner.
- UART is a half-duplex protocol. 
- Half-duplex means transferring and receiving the data but not at the same time. 
- It uses a single data line for transmitting and receiving the data. It has one start bit, 8-bit data and onestop bit mean the 8-bit data transfer one’s signal is high to low.

## Application Background
 ![Alt](img3.jpg)

UART is one of the most simple and most commonly used Serial Communication techniques. Today, UART is being used in many applications like GPS Receivers, Bluetooth Modules, GSM and GPRS Modems, Wireless Communication Systems, RFID based applications etc.

# UART protocol data flow
![Alt](img4.jpg)

These special bits are: Start bit, Priority bit, Stop bit.
**START BIT** :When a word is given to UART for asynchronous transmission, a bit called *“START BIT”* is added to the beginning of each word that is to be transmitted.
The start bit is used to alert the receiver that a word of data is about to sent, and to force the clock in the receiver into synchronization with the clock in the transmitter.

**DATA BIT OR DATA FRAME**: After the start bit, the individual bits of data are sent, with the least significant Bit(LSB) being sent first. Each bit in the transmission is transmitted for exactly the same amount of time as all of the other bits. And the receiver looks at the wire at approximately halfway through the period assigned to each bit to determine if the bit is 1 or 0. For example, if it takes 2 second to send each bit, the receiver will track the signal after 1 second has passed.

**PARITY BIT**: remove the problem of loss of some bits during the transmission of a signal, error correction mechanism must be added to the transmitted data. Parity bit error checking mechanism is one of the simplest methods to detect any error in received data. In asynchronous serial communication, a parity bit is added at the end of data bits to check the number of 1’s.

**STOP BIT**: At the end of each data packet, stop bit i.e. 1 is added to indicate the end of one data packet. At the receiver end, this stop bit is used to stop the reception of Data.

# How UART works

Two UARTs communicate directly with each other.
 - The transmitting UART converts parallel data from a controlling device like a CPU into serial form.

    ![Alt](img5.jpg)

- Transmitting it in serial to the receiving UART.
 - Receiver UART then converts the serial data back into parallel data for the receiving device. 
 -  Only two wires are needed to transmit data between two UARTs.
 -  Data flows from TX pin of the transmitting UART to the Rx pin of the receiving UART.
 -  UART transmit data asynchronously, which means there is no need to transmit clock signal with the transmitted data. 
 -  Instead of clock, the transmitter transmit data with some special bits to synchronize the sending and receiving units. 
 -  These bits define the beginning and end of the data packet so the receiving UART knows when to start and stop reading the bits. 
 -  As soon as the start bit is detected, the receiver observe the start bit for 50[percent]of the receiving baud rate, if it is the receiver start sampling other data bits at the middle of each bit otherwise receiver set flag for framing error.
After detecting the 8 bit data, the receiver then looks for the parity bit which is generated by the transmitter for the single bit error detection. 
-  If the parity bit is detected properly, the receiver looks for the stop bit to stop the reception of data. 
-  After the successful detection of stop bit the receiver line goes high logic state to indicate idle state and start looking for the next start bit.

    ![Alt](img6.jpg)

The UART that is going to transmit data receives the data from a data bus. The data bus is used to send data to the UART by another device like a CPU, memory, or microcontroller. Data is transferred from the data bus to the transmitting UART in parallel form. After the transmitting UART gets the parallel data from the data bus, it adds a start bit, a parity bit, and a stop bit, creating the data packet. Next, the data packet is output serially, bit by bit at the Tx pin.    

The receiving UART reads the data packet bit by bit at its Rx pin. The receiving UART then converts the data back into parallel form and removes the start bit, parity bit, and stop bits. Finally, the receiving UART transfers the data packet in parallel to the data bus on the receiving end:

## Verilog Implementation
This project is divided into 3 main modules for the easy and clear understanding and also for the ease in further development of project. **1.Baudrate generator 2. UART transmitter and 3. UART receiver**
- These 3 module are further divided into sub modules. 
-  All the modules are connected by instantiating each module in the main module.
## Baud rate generate

![Alt](img7.jpg)

- Baud rate generator determines transmission speed in asynchronous communication. 
-  It is the number of symbols per second transferred. 
-  Each bit is 1/(baud rate) wide. 
-  Baud rate=clock freq./(16 divisor) Some standard baud rate:
-  2400 
-  9600 
-  19200
-  38400

     ![Alt](img8.jpg)

# Design of UART transmitter

- UART transmitter controls transmission by fetching a
data word in parallel format and directing the UART
to transmit it in a serial format

  ![Alt](img9.jpg)

  - This module is further divided into 4 sub modules:- 
 1) **TX Controller fsm**: Generates all the necessary signal required to transmit data at right time 
 2) **Parity generator**: Generate parity for the 8 bit input data.
 3) **PISO(Parallel In Serial Out)**:Takes the 8 bit input binary data and convert it into 1 bit serial data.
 4) **Tx mux**: It is 4x1 Mux to transmit 4 different type of data viz.start bit, data bit, parity bit and the stop bit.

## Transmitter  state machine
  ![Alt](img9.jpg)
  *finite-state machine (FSM) or finitestate automaton (FSA)*
- It is an abstract machine that can be in exactly one of a finite
number of states at any given time. The FSM can change
from one state to another in response to some inputs; the
change from one state to another is called a transition. An
FSM is defined by a list of its states, its initial state, and the
inputs that trigger each transition.

 From the above figure we have to take two STATES for data shifting, given as follows
**1.present state and 2.next state**.

 Verilog implementation from above figure.  ![https://www.edaplayground.com/x/4jQu]()
