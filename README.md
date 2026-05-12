# EXPERIMENT-01-INTERFACING-A-DIGITAL-OUTPUT-TO-IOT-DEVELOPMENT-BOARD


**DATE: 30/04/2026**

**NAME: INIYASRI S**

**ROLL NO: 212223230081**

**DEPARTMENT: AIDS**

## Aim

To Interface a Digital output (LED) to ARM IOT development board and write a program to blink an LED.

## Components required

- STM32 CUBE IDE
- ARM IOT development board
- STM programmer tool

## Theory

The ARM (Advanced RISC Machine) architecture is widely used in microcontrollers and processors due to its efficiency, low power consumption, and high performance. ARM processors follow the Reduced Instruction Set Computing (RISC) design, making them ideal for embedded systems, mobile devices, and IoT applications. Many well-known semiconductor companies, including STMicroelectronics, use ARM-based architectures to develop powerful and energy-efficient microcontrollers.

One such microcontroller is the STM32WLE5JC, which is part of the STM32 family and is based on the ARM Cortex-M4 core. It is specifically designed for LoRaWAN® and other sub-GHz wireless communication applications, making it ideal for IoT and LPWAN (Low Power Wide Area Network) solutions. This microcontroller integrates a LoRa® transceiver, eliminating the need for an external radio module and reducing both cost and power consumption. With a maximum clock speed of 48 MHz, 256 KB of Flash memory, and 64 KB of RAM, it provides enough computing power for real-time data processing and wireless communication.

The STM32WLE5JC is known for its ultra-low power consumption, making it perfect for battery-operated IoT devices such as smart agriculture sensors, environmental monitoring systems, industrial automation, and asset tracking. It supports multiple communication interfaces, including I2C, SPI, and UART, allowing seamless integration with various sensors and peripherals. Additionally, it features built-in security capabilities such as AES 256-bit encryption and a True Random Number Generator (TRNG) for secure data transmission.

With its power-efficient design, built-in LoRaWAN support, and flexible communication options, the STM32WLE5JC is an excellent choice for developers looking to build long-range, low-power IoT applications. It is fully compatible with STM32CubeIDE and LoRaWAN middleware, making development and deployment easier for engineers and learners alike.

## Procedure

1. Click on STM 32 CUBE IDE, the following screen will appear
   
 <img width="1919" height="1199" alt="Screenshot 2026-05-01 134710" src="https://github.com/user-attachments/assets/9cac74a6-e771-48d3-a269-34e62692ef28" />



2. Click on FILE, click on new stm 32 project
   
<img width="1919" height="1199" alt="Screenshot 2026-05-01 134817" src="https://github.com/user-attachments/assets/f934e89d-319a-4340-b3c1-eaa36ef93cd6" />
<img width="1919" height="1199" alt="Screenshot 2026-05-01 134943" src="https://github.com/user-attachments/assets/b136c196-302b-47ae-b3de-9f5316840ab1" />


3. Select the target to be programmed as shown below and click on next
   
![Screenshot 2025-03-11 134231](https://github.com/user-attachments/assets/09e61f3d-224f-4ca8-96d4-7336869df5c7)

4. Select the program name
   
![image](https://user-images.githubusercontent.com/36288975/226189316-09832a30-4d1a-4d4f-b8ad-2dc28f137711.png)

5. Corresponding ioc file will be generated automatically
   
![Screenshot 2025-03-11 134528](https://github.com/user-attachments/assets/df427edd-e24a-4612-a858-aeae859b379f)


6. Select the appropriate pins as GPIO, in or out, USART or required options and configure
   
![Screenshot 2025-03-11 134617](https://github.com/user-attachments/assets/125ee548-30b1-4c88-932f-adf07984522f)

![Screenshot 2025-03-11 134642](https://github.com/user-attachments/assets/0adfbb58-4cad-408a-9300-f4808b53cac4)


7. Click on Ctrl+S, automatically C program will be generated
   
![Screenshot 2025-03-11 134709](https://github.com/user-attachments/assets/70b83b79-1569-4f14-99d5-e2adbb4e692d)

8. Edit the program and as per required 

<img width="1919" height="1199" alt="Screenshot 2026-05-01 135129" src="https://github.com/user-attachments/assets/b5729c57-c418-479b-94c0-99f14cf9c9d5" />



9. Use project and build all 

<img width="1919" height="1199" alt="Screenshot 2026-05-01 135209" src="https://github.com/user-attachments/assets/cf62f438-307b-466e-86a3-ffe7bcb82ed9" />


10. Once the project is bulild 

<img width="730" height="247" alt="Screenshot 2026-05-01 135218" src="https://github.com/user-attachments/assets/b2a53464-69d9-4c3f-a036-5c68792ecc14" />


11. connect the iot board to power supply and usb

12. After connecting open the STM cube programmer

![Screenshot 2025-03-11 135208](https://github.com/user-attachments/assets/bb67ab6b-81a5-450c-b170-4276a9b87ef2)


13. Connect the STM board through the COM port, then upload the corresponding project ELF file/Hex file or Bin file in Erasing & Programming Window,while ensuring the board is in flash mode, and click on 'Start Program'.
    
   <img width="1600" height="859" alt="WhatsApp Image 2026-05-01 at 2 04 11 PM" src="https://github.com/user-attachments/assets/e4ea4846-5b99-4e5f-b1ad-09f20dffae03" />


14.  After the file download is complete, switch your board to run mode and press the reset button to see the output






## STM 32 CUBE PROGRAM

```
#include "main.h"

void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
  HAL_Init();
  SystemClock_Config();
  MX_GPIO_Init();

  while (1)
  {
    HAL_GPIO_WritePin(GPIOA, GPIO_PIN_0, GPIO_PIN_SET);
    HAL_Delay(4000);

    HAL_GPIO_WritePin(GPIOA, GPIO_PIN_0, GPIO_PIN_RESET);
    HAL_Delay(4000);
  }
}

void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};

  __HAL_PWR_VOLTAGESCALING_CONFIG(PWR_REGULATOR_VOLTAGE_SCALE2);

  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_MSI;
  RCC_OscInitStruct.MSIState = RCC_MSI_ON;
  RCC_OscInitStruct.MSIClockRange = RCC_MSIRANGE_6;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_NONE;

  HAL_RCC_OscConfig(&RCC_OscInitStruct);

  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK |
                               RCC_CLOCKTYPE_SYSCLK |
                               RCC_CLOCKTYPE_PCLK1 |
                               RCC_CLOCKTYPE_PCLK2;

  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_MSI;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;
  RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;

  HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_0);
}

static void MX_GPIO_Init(void)
{
  GPIO_InitTypeDef GPIO_InitStruct = {0};

  __HAL_RCC_GPIOA_CLK_ENABLE();

  HAL_GPIO_WritePin(GPIOA, GPIO_PIN_0, GPIO_PIN_RESET);

  GPIO_InitStruct.Pin = GPIO_PIN_0;
  GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
  GPIO_InitStruct.Pull = GPIO_NOPULL;
  GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;

  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);
}
```

## OUTPUT
**OFF**
<img width="1600" height="1200" alt="WhatsApp Image 2026-05-01 at 1 59 57 PM" src="https://github.com/user-attachments/assets/ab2d8762-2c81-4282-b596-8efe21ce5313" />


**ON**
<img width="1600" height="1200" alt="WhatsApp Image 2026-05-01 at 2 00 08 PM" src="https://github.com/user-attachments/assets/d454ea70-3508-4668-806d-7258970815db" />



## Result

Interfacing a digital output with ARM microcontroller based IOT development is executed and the results are verified.
