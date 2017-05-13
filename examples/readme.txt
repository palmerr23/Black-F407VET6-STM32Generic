For a general tutorial on STM32 ADC operation, I can recommend

http://embedded-lab.com/blog/stm32-adc-2/

Useful parameters for STM32 F4 ADCs (a full list is in stm32f4xx_hal_adc.h)

Most common values are starred*

ADC resolution
--------------
number of bits returned after an ADC conversion (less bits = faster conversion)
used for AdcHandle.Init.Resolution  

ADC_RESOLUTION_12B * (maximum accuracy)
ADC_RESOLUTION_10B 
ADC_RESOLUTION_8B  * (higher speed)
ADC_RESOLUTION_6B  

ADC sample time
--------------
the number of cycles that the ADC waits for the sample to ramp to new value before conversion (more cycles = more accurate with rapidly changing signals e.g. square waves)
used for sConfig.SamplingTime 

#define ADC_SAMPLETIME_3CYCLES  *  (for slowly changing values, e.g. battery voltage) 
#define ADC_SAMPLETIME_15CYCLES *  (rapidly changing signals, e.g. square waves)
#define ADC_SAMPLETIME_28CYCLES   
#define ADC_SAMPLETIME_56CYCLES   
#define ADC_SAMPLETIME_84CYCLES   
#define ADC_SAMPLETIME_112CYCLES 
#define ADC_SAMPLETIME_144CYCLES  
#define ADC_SAMPLETIME_480CYCLES  


The rest of the parameters in each example are set in combinations that are described in the accompanying readme.txt files. 

The following files describe most of the options 
stm32f4xx_hal_adc.h
stm32f4xx_hal_adc_ex.h
stm32f4xx_hal_dma.h
