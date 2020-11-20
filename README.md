# UART-PROTOCOL
##  Raj Kumar Laldev 
 Advance VLSI Lab  Silicon institute of technology Bhubaneswar,India  
 rajbihar5364@gmail.com
 # Table of Contents
 - [Intrduction]()
  *  [Application Background]()
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

# Intrduction
Protocol: A set of rules and regulations is called a
protocol. Different type of protocols are available.
1.  Bus protocol: APB,AHB,AXI,ASB,ACE 
2. Peripheral protocol.
- High speed: PCIe, SATA, SAS, Ethernet, USB, MIPI.
- Low speed :UART,SPI,I2C.

 Fig.1  Single wire connection ![Alt](img1.jpg)

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

fig.2  System on chip     ![Alt](img2.jpg)