# UART
UART (Universal asynchronous receiver-transmitter) is a data communication protocol for asynchronous serial communication. UART performs parallel-to-serial conversion on data received from a microprocessor, sends the data bits one by one, then performs serial-to-parallel conversion. The timing issue is handled by a start bit and stop bit(s). There is also an optional parity bit to determine whether the correct data is received [[1]](https://www.ti.com/lit/ug/sprugp1/sprugp1.pdf).
UART baud rates are relatively slower than the microprocessors speed. Typical baud rates are 9600, 31250 and 115200 Hz. In order to sample the data bits properly, Rx driver uses faster bit rates, generally 8x or 16x times of the baud rate. To increase the performance, most of the UART interfaces include a Tx (transmit) and a Rx (receive) FIFO buffers. 

### UART Frame
The UART frame is consists of:
* 1 Start Bit (logic low)
* 5-8 Data Bits
* 0-1 Parity Bit
* 1-2 Stop Bit(s) (logic high)

<img src="https://user-images.githubusercontent.com/51496220/235833559-c95beef7-b57e-4a39-a183-48b0f1c9f09b.png" width="300">

In IDLE mode, data transmission line is held at logic-high(1) level in which there is no data transfer. Data transmission is started when the transmission line switched from logic-high(1) to the logic-low(0). Data bits are framed with a start bit, an optional parity bit and 1 to 2 stop bit(s). The number of data bits can be configured to 5-8 bits.


### Baud Rate




### Tx Driver


### Rx Driver
UART baud rates are relatively slower than the microprocessors speed. To increase the performance, most of the UART interfaces include a Tx (transmit) and a Rx (receive) FIFO buffers. 


## Block Diagram
<img src="https://user-images.githubusercontent.com/51496220/235600974-d7dd7bc6-1c2c-4c13-9061-2960e5777a80.png" width="300">


### FPGA Implementation


## References
