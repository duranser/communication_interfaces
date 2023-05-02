# UART
UART (Universal asynchronous receiver-transmitter) is a data communication protocol for asynchronous serial communication. UART performs parallel-to-serial conversion on data received from a microprocessor, sends the data bits one by one, then performs serial-to-parallel conversion. The timing issue is handled by a start bit and stop bit(s). There is also an optional parity bit to determine whether the correct data is received [[1]](https://www.ti.com/lit/ug/sprugp1/sprugp1.pdf).

## UART Frame
The UART frame is consists of:
* 1 Start Bit (logic low)
* 5-8 Data Bits
* 1-2 Stop Bit(s) (logic high)



## Block Diagram
<img src="https://user-images.githubusercontent.com/51496220/235600974-d7dd7bc6-1c2c-4c13-9061-2960e5777a80.png" width="300">


### Tx Driver


### Rx Driver


### FPGA Implementation


## References
