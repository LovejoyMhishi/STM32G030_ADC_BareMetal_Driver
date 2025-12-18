<h1 align="center" style="color:#4CAF50;">
 ⚡ STM32G030 ADC Bare-Metal Driver
</h1>

<p align="center">
  <em>Low-level Analog-to-Digital Converter (ADC) driver for STM32G030 microcontrollers</em><br>
</p>

---
## 🌟 What It Does

This C-based driver enables embedded systems to **configure and read analog signals** using the internal ADC peripheral of the STM32G030 microcontroller.

### It supports:

- 📥 Initializing the ADC with custom clock and resolution settings  
- 📤 Reading 12-bit digital values from analog input channels  
- 🔁 Continuous conversion mode for real-time signal sampling  
- 🧠 Polling-based data acquisition without HAL or LL libraries  

---

## 🧠 Core Concepts

The driver manages critical ADC operations, assuming:

- ⏱️ The ADC peripheral clock must be enabled before configuration  
- ⚡ The internal ADC voltage regulator must stabilize before use  
- 🎯 ADC calibration is required for accurate conversions  
- 🛠️ GPIO pins connected to ADC channels must be configured as analog inputs  
- 🔄 Polling mode is used for end-of-conversion detection  

---

## 🔧 Key Features

### 🔁 ADC Operations

- `ADC1_Init()` – configures ADC clock, resolution, calibration, and channel selection  
- `ADC1_Start()` – starts ADC conversions in continuous mode  
- `ADC1_Read()` – retrieves the latest ADC conversion result  

### ⚙️ Configuration & Control

- ADC clock prescaler configuration  
- Programmable sampling time selection  
- Channel selection via `ADC_CHSELR`  
- Continuous conversion mode support  
- CMSIS-based register-level control  

---

## 📦 Configuration

- ADC channel selection via `ADC_CHSELR` (e.g., `CHSEL0` for PA0)  
- Sampling time configuration through `ADC_SMPR`  
- ADC clock prescaler setup using `ADC_CCR`  
- Resolution and data alignment configuration via `ADC_CFGR1`

## 🧪 Example Usage

```c
#include "adc.h"

#define V_REF_plus 3.3f   
         
int main(void)
{
    ADC1_Init();          // Initialize ADC peripheral
    ADC1_Start();         // Start continuous conversion

    while (1)
    {
        uint16_t adc_raw = ADC1_Read();

        /*
         * Convert ADC value to measured voltage
         */
        float VrefInt = (V_REF_plus * adc_raw / 4095.0f);
    }
}
