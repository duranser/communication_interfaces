# UART
**UART (Universal asynchronous receiver-transmitter)** is a data communication protocol for asynchronous serial communication. UART performs parallel-to-serial conversion on data received from a microprocessor, sends the data bits one by one, then performs serial-to-parallel conversion. The timing issue is handled by a start bit and stop bit(s). There is also an optional parity bit to determine whether the correct data is received [[1]](https://www.ti.com/lit/ug/sprugp1/sprugp1.pdf).

UART baud rates are relatively slower than the microprocessors speed. Typical baud rates are 9600 and 115200 Hz. In order to sample the data bits properly, Rx driver uses oversampling, generally 8x or 16x times of the baud rate. To increase the performance, most of the UART interfaces include a Tx (transmit) and a Rx (receive) FIFO buffers together with control and status registers (CSRs) [[2]](https://en.wikipedia.org/wiki/Universal_asynchronous_receiver-transmitter). 

### UART Frame
The UART frame is consists of:
* 1 Start Bit (logic low)
* 5-8 Data Bits
* 0-1 Parity Bit
* 1-2 Stop Bit(s) (logic high)

<img src="https://user-images.githubusercontent.com/51496220/235833559-c95beef7-b57e-4a39-a183-48b0f1c9f09b.png" width="400">

Data bits are framed with a start bit, an optional parity bit and 1 to 2 stop bit(s). The number of data bits can be configured to 5-8 bits.


### Baud Rate
UART Baud Rate is calculated by \
$f_{baud} = \frac{f_{clk}}{1 + baudDiv}$ \
where $f_{clk}$ is the system frequency, $f_{baud}$ is the baud rate and $baudDiv$ is the dividor to achieve desired baud rate.

To obtain the desired baud rate and its **8x** or **16x** counterpart a **frequency dividor** can be used. First, oversampled baud frequency should be calculated and then real baud frequency can be obtain from it to make them synchronized.  

### Tx Driver
In IDLE mode, data transmission line is held at logic-high(1) level in which there is no data transfer. Data transmission is started when the transmission line switched from logic-high(1) to the logic-low(0). After that, data bits and an optional parity bit are transmitted by starting from least significant bits to most significant ones. When the data transmission is completed, the transmission line drives logic-high(1).

UART Tx Driver can be easily designed with a Finite State Machine (FSM) including four states:
* **IDLE**  : there is no transfer and tx line drives high,
* **START** : transmission is started and tx line is switched to low,
* **DATA**  : data bits and an optional parity bit are transmitted by starting from LSBs to MSBs,
* **STOP**  : transmission is completed and tx line drives high

<img src="https://user-images.githubusercontent.com/51496220/235855392-baff2e4c-54a5-4ead-aa35-21893fed8ad6.png" width="300">

**tx_en** is the control signal starting data transmission and **bit_index** represents the number of the data bit transmitted. 
UART Tx Driver can also have start, busy and done output control signals to inform the FIFO buffers about the status and whether new data read is necessary or not.

### Rx Driver
Different from the Tx Driver, Rx Driver uses **16x** times of the baud rate. In IDLE mode, Rx driver observes the data receive line if it switches from logic-high(1) to logic-low(0) level. If the start bit logic-low(0) lasts at least 8 sample (T/2), data bits are started to read. Each data bit is sampled at 16th sample. When the data receive is completed, Rx Driver waits for stop bit(s) logic-high(1). If stop bit(s) lasts at least 8 sample (T/2) or 16 sample (T), Rx Driver writes the received data to the FIFO Buffer.

UART Rx Driver is designed with a Finite State Machine (FSM) including four states:
* **IDLE**  : 
* **START** : 
* **DATA**  : 
* **STOP**  : 
* 
<img src="https://user-images.githubusercontent.com/51496220/236406776-2cf7b11c-54fc-47ef-b9f7-cc188a3bd035.png" width="300">


### Control and Status Registers
* **tx_en** : Enable Tx channel and start to transmit 1-bit,
* **rx_en** : Enable Rx channel and start to receive 1-bit,
* **data_bits_len** : Number of data bits is configured with 2-bit,
* **parity_set** : Parity bit option can be set with 1-bit,
* **stop_bits_len** : Stop bit(s) length is configured with 2-bit,
* **baudDiv** : A programmable baud rate can be achieved by 16-bit,
* **buffer_depth** : Depth of the FIFO Buffers can be configured by 8-bit,

* **tx_full** : tx buffer is full,
* **tx_empty**: tx buffer is empty,
* **rx_full** : rx buffer is full,
* **rx_empty**: rx buffer is empty


## Block Diagram
<img src="https://user-images.githubusercontent.com/51496220/235600974-d7dd7bc6-1c2c-4c13-9061-2960e5777a80.png" width="300">


### FPGA Implementation


## References
[1] https://www.ti.com/lit/ug/sprugp1/sprugp1.pdf
[2] https://en.wikipedia.org/wiki/Universal_asynchronous_receiver-transmitter
