![image](https://github.com/user-attachments/assets/c9cc6fab-c921-411a-b77a-75a37e118b4f)
![image](https://github.com/user-attachments/assets/e742894f-2d33-409b-8570-751ad7021d3d)
![image](https://github.com/user-attachments/assets/18c7f240-c333-479e-9a32-3c877d9f85bb)
![image](https://github.com/user-attachments/assets/85c23c0e-4227-44dc-8afe-672ce0e70a44)
![image](https://github.com/user-attachments/assets/d4029dfd-2fe9-4f72-8a55-1a64f17fe4bf)
![image](https://github.com/user-attachments/assets/ba0b297f-f0f1-40de-834e-da1e04594eec)
![image](https://github.com/user-attachments/assets/d08cfa68-2bab-48e1-94c7-0b00c5c86577)
![image](https://github.com/user-attachments/assets/07a4243d-1e00-4e94-a823-02de95df40d3)
![image](https://github.com/user-attachments/assets/7b034fb4-04c6-4ab8-b20e-f9a0e95a5654)
![image](https://github.com/user-attachments/assets/00ffe157-ed30-4263-9055-d16450e2cf70)
![image](https://github.com/user-attachments/assets/61bfc124-bfbe-4fa8-acc0-86a20f7c916c)


## Program 1 Continuous Transmission of Character 'G' via USART on AVR
```csharp
#include <avr/io.h>

// Initialize the USART (Universal Serial Communication)
void usart_init(void)
{
    // Enable transmitter (TXEN0 bit of UCSRB register)
    UCSR0B = (1 << TXEN0);
    // Set frame format: 8 data bits, no parity, 1 stop bit (UCSZ01 and UCSZ00 bits of UCSRC register)
    UCSR0C = (1 << UCSZ01) | (1 << UCSZ00);
    // Set baud rate: 9600bps (UBRR0L is loaded with 103 for 8MHz system clock)
    UBRR0L = 103;
}

// Function to send a character
void usart_send(unsigned char ch)
{
    // Wait until the Data Register is empty (UDRE0 bit of UCSRA register)
    while (!(UCSR0A & (1 << UDRE0)));
    // Put character into the USART Data Register to transmit
    UDR0 = ch;
}

int main(void)
{
    // Initialize USART communication
    usart_init();
    
    // Infinite loop to continuously send data
    while(1)
    {
        // Send the character 'G' continuously
        usart_send('G');
    }

    return 0;
}

```

## Program 2 Continuous Transmission of the Message 'The Earth is but One Country.' via USART on AVR
```csharp
#include <avr/io.h>

// Initialize the USART (Universal Serial Communication)
void usart_init(void)
{
    // Enable the transmitter by setting TXEN0 bit in UCSR0B
    UCSR0B = (1 << TXEN0);
    
    // Set the frame format: 8 data bits, no parity, 1 stop bit
    // UCSZ01 and UCSZ00 are set to configure 8-bit data frame
    UCSR0C = (1 << UCSZ01) | (1 << UCSZ00);
    
    // Set baud rate: 9600bps (UBRR0L = 103 for 8 MHz system clock)
    UBRR0L = 103;
}

// Function to send a character
void usart_send(unsigned char ch)
{
    // Wait until the Data Register is empty (UDRE0 bit in UCSR0A)
    while (!(UCSR0A & (1 << UDRE0)));
    
    // Load the character into the USART Data Register (UDR0)
    UDR0 = ch;
}

int main(void)
{
    // Initialize USART communication
    usart_init();
    
    // Message to be sent
    char message[] = "The Earth is but One Country.";
    int i = 0;
    
    // Infinite loop to continuously send the message
    while(1)
    {
        // Send each character of the message
        usart_send(message[i]);
        
        // If we reach the end of the message, loop back to the start
        if (message[i] == '\0') 
        {
            i = 0;  // Reset the index to start the message from the beginning
        }
        else
        {
            i++;  // Move to the next character
        }
    }

    return 0;
}

```


## Program 3 Receiving Serial Data via USART and Displaying on Port B in AVR
```csharp
#include <avr/io.h>

int main(void)
{
    // Set Port B as output (all pins of Port B are set as output)
    DDRB = 0xFF;

    // Enable the USART receiver by setting the RXEN0 bit in UCSR0B
    UCSR0B = (1 << RXEN0);
    
    // Set the frame format: 8 data bits, no parity, 1 stop bit
    // UCSZ01 and UCSZ00 bits in UCSR0C configure an 8-bit data frame
    UCSR0C = (1 << UCSZ01) | (1 << UCSZ00);

    // Set baud rate to 9600bps (UBRR0L is loaded with 103 for 8 MHz system clock)
    UBRR0L = 103;

    // Infinite loop to continuously receive and process data
    while (1)
    {
        // Wait until new data is received (RXC0 bit in UCSR0A indicates data reception)
        while (!(UCSR0A & (1 << RXC0)));

        // Read the received data from UDR0 and send it to Port B
        PORTB = UDR0;
    }

    return 0;
}

```


# AVR USART Control Registers: Key Concepts

## 1. UBRR (USART Baud Rate Register)
- **Purpose**: Sets the baud rate for communication.
- **Division Formula**: `UBRR = (Fosc / (16 * Baud Rate)) - 1`
- **Registers**:
  - `UBRRL`: Lower 8 bits of UBRR.
  - `UBRRH`: Higher 8 bits of UBRR (used when needed).

---

## 2. UCSRA (USART Control and Status Register A)
- **Purpose**: Monitors the status of data transmission/reception.
- **Key Bits**:
  - **UDRE (Data Register Empty)**: 1 when UDR is ready for the next byte.
  - **RXC (Receive Complete)**: 1 when new data is available in UDR.
  - **TXC (Transmit Complete)**: 1 when the last transmission is complete.

---

## 3. UCSRB (USART Control and Status Register B)
- **Purpose**: Enables specific USART features.
- **Key Bits**:
  - **RXEN (Receiver Enable)**: Enables the USART receiver.
  - **TXEN (Transmitter Enable)**: Enables the USART transmitter.
  - **RXCIE (Receive Interrupt Enable)**: Enables an interrupt when new data is received.
  - **TXCIE (Transmit Interrupt Enable)**: Enables an interrupt when a transmission completes.

---

## 4. UCSRC (USART Control and Status Register C)
- **Purpose**: Configures the data format for communication.
- **Key Bits**:
  - **UCSZ0 & UCSZ1**: Set data size (5, 6, 7, 8, or 9 bits).
  - **UPM0 & UPM1**: Set parity mode (None, Even, or Odd).
  - **USBS**: Sets the number of stop bits (1 or 2).

---

## 5. UDR (USART Data Register)
- **Purpose**: Used to send and receive data.
  - **Write** to `UDR` to transmit data.
  - **Read** from `UDR` to receive data.
- **Process**:
  - Transmit: Wait until `UDRE` is set, then write to `UDR`.
  - Receive: Wait until `RXC` is set, then read from `UDR`.

---

# Tips to Remember
1. **Baud Rate (Speed)**: Controlled by **UBRR**.
2. **Status Checking**: Monitored using **UCSRA**.
3. **Enable Features**: Controlled by **UCSRB**.
4. **Data Format**: Configured with **UCSRC**.
5. **Data Send/Receive**: Always through **UDR**.

---

# Example Process (Step-by-Step)
1. Set **UBRR** for baud rate.
2. Configure **UCSRC** for data size, parity, and stop bits.
3. Enable transmitter/receiver using **UCSRB**.
4. Write data to **UDR** for transmission.
5. Check **UDRE** or **RXC** in **UCSRA** to send/receive data.




![image](https://github.com/user-attachments/assets/3b49ed4d-4140-4765-8168-b35a781c20ea)

![image](https://github.com/user-attachments/assets/161744d5-089f-4191-9c7f-13a87cbbdc6d)

![image](https://github.com/user-attachments/assets/8cb20b22-294c-492e-ad5d-71e170449e7a)


![image](https://github.com/user-attachments/assets/cc83008a-7dc1-446a-9e2c-e7adc42c9587)

![image](https://github.com/user-attachments/assets/aaf8ec42-c5e5-4b42-b03d-cf6932ab0091)

![image](https://github.com/user-attachments/assets/8570eb62-65ae-455d-a7ad-8aacd281c88b)







# All about MAX232
# MAX232: An Overview

The **MAX232** is an integrated circuit (IC) commonly used in embedded systems to enable serial communication between a microcontroller (e.g., AVR, Arduino, PIC) and a computer or other devices that use the **RS-232** communication protocol.

## Key Features

1. **Voltage Level Conversion**:
   - Microcontrollers typically operate at **TTL voltage levels** (0–5V or 0–3.3V).
   - RS-232 devices, like computers, use higher voltage levels (±12V).
   - The MAX232 converts **TTL voltage levels** to **RS-232 voltage levels** and vice versa.

2. **Dual Transmitter and Receiver**:
   - The MAX232 has **two drivers (transmitters)** and **two receivers** to facilitate bi-directional communication.

3. **Internal Charge Pump**:
   - Generates the necessary positive and negative voltages (±10V) from a single 5V power supply, eliminating the need for an external dual-voltage supply.

4. **Capacitor Requirement**:
   - It uses a set of external capacitors (typically 1µF or 10µF) for the internal charge pump operation.

---

## Pin Configuration

The MAX232 typically comes in a 16-pin package. Important pins include:

- **T1in and T2in**: Transmitter inputs (TTL side).
- **T1out and T2out**: Transmitter outputs (RS-232 side).
- **R1in and R2in**: Receiver inputs (RS-232 side).
- **R1out and R2out**: Receiver outputs (TTL side).
- **Vcc and GND**: Power supply (5V and ground).
- **Capacitor pins**: For charge pump capacitors (C1+, C1-, C2+, C2-).

---

## Why is MAX232 Used?

1. **Voltage Compatibility**: Ensures proper communication between TTL and RS-232 devices by translating voltage levels.
2. **Reliable Communication**: Protects the microcontroller from high RS-232 voltages.
3. **Ease of Use**: Requires minimal external components (5 capacitors) and operates with a single 5V power supply.

---

## Example Use Case

Suppose you want to connect an AVR microcontroller to a PC via an RS-232 serial port. The microcontroller sends data at TTL levels (0–5V), while the PC expects RS-232 levels (±12V). The MAX232 bridges this gap:

- It converts the microcontroller’s TTL signals to RS-232 levels when transmitting to the PC.
- It converts the RS-232 signals from the PC to TTL levels when receiving data.

This makes the MAX232 an essential component in serial communication circuits involving RS-232 devices.
