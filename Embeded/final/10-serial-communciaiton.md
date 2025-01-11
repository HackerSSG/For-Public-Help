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
