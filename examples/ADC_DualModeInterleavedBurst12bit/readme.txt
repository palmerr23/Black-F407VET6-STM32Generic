/**
  @page ADC_DualModeInterleavedBurst12bit  Use ADC1 and ADC2 in Dual interleaved mode and DMA mode2
 * Modified 6-May-2017 RP for Arduino / STM32GENERIC platform
  @verbatim
  ******************** (C) COPYRIGHT 2017 STMicroelectronics *******************
  * @file    ADC/ADC_DualModeInterleaved/readme.txt 
  * @author  MCD Application Team
  * @version V1.4.0
  * @date    17-February-2017
 
  * @brief   Description of the Dual interleaved mode and DMA mode2 example
  ******************************************************************************
  *
  * Redistribution and use in source and binary forms, with or without modification,
  * are permitted provided that the following conditions are met:
  *   1. Redistributions of source code must retain the above copyright notice,
  *      this list of conditions and the following disclaimer.
  *   2. Redistributions in binary form must reproduce the above copyright notice,
  *      this list of conditions and the following disclaimer in the documentation
  *      and/or other materials provided with the distribution.
  *   3. Neither the name of STMicroelectronics nor the names of its contributors
  *      may be used to endorse or promote products derived from this software
  *      without specific prior written permission.
  *
  * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
  * AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
  * IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
  * DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
  * FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
  * DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
  * SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
  * CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
  * OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
  * OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
  *
  ******************************************************************************
  @endverbatim

@par Hardware and Software environment 

  - This example runs on STM32F407xx devices under Arduino and has been optimised for the STM32GENERIC codeset: https://github.com/danieleff/STM32GENERIC

@par Example Description 


This example provides a short description of how to use 
- Two ADC peripherals to perform conversions in interleaved dual-mode.
- One regular channel, 12-bit resolution
- using DMA in mode 2 with 3Msps.
- it converts a buffer of samples and then sotware triggers another buffer.

The user needs to supply some way to vary the ADC1 channel1 input value. Three options are
- a potentiometer between 3.3v and GND, 
- a signal generator with DC coupled output of 0 < input < 3.3v
- using a DAC to generate a signal

The Dual interleaved delay is configured for 5 ADC clk cycles using mode.TwoSamplingDelay

On each DMA request (two data items are available) two bytes representing two 
ADC-converted data items are transferred as a half word.
The data transfer order is similar to that of the DMA mode 2.

A DMA request is generated each time 2 data items are available
packed into the two 16-bit halfwords of a 32-bit integer.

The ADC1 and ADC2 are configured to convert ADC Channel 1, with conversion 
triggered by software.
By this way, ADC channel 1 is converted each 6 cycles.

If the system clock is 144MHz, APB2 = 72MHz and ADC clock = APB2 /2.
Since ADCCLK = 36MHz and Conversion rate = 6 cycles
==> Conversion Time = 36M/6cyc = 6Msps.

STM32 Eval board's LEDs can be used to monitor the transfer status:
 - LED1 is ON when the ADC conversion is complete.
 - LED3 is ON when there is an error in initialization. 
  
@note Refer to "simulation.xls" file to have the diagram simulation of the example.


@note Care must be taken when using Delay(), this function provides accurate delay (in milliseconds)
      based on variable incremented in SysTick ISR. This implies that if Delay() is called from
      a peripheral ISR process, then the SysTick interrupt must have higher priority (numerically lower)
      than the peripheral interrupt. Otherwise the caller ISR process will be blocked.
      To change the SysTick interrupt priority you have to use HAL_NVIC_SetPriority() function.
      

 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
