# Seat-Heater-Control-System-using-RTOS
Description of project

Implementation of a seat heater control system for the front two seats in the car (driver seat and passenger seat). Each seat shall consist of:

The button that is used to take the input level required to set the seat temperature.
Temperature sensor to monitor the temperature value.
Heating element to control the temperature value based on the desired level using a variable intensity power as input.
Shared screen between both seats to show the current state of the system. System features:
Heating level shall have one value of the following: a. Off: The feature is off, and the temperature is not controlled. b. Low: the desired temperature is 25°C. c. Medium: the desired temperature is 30°C. d. High: the desired temperature is 35°C.
System shall control the temperature to be set within the range of the desired temperature +/- 3°C.
Diagnostics shall be present in case of failure of the temperature sensor. a. If the temperature sensor gives a value out of its range this is considered as a failure in the sensor. b. The range of the temperature sensor shall be 5°C-40°C. c. Such issues shall be logged in the memory according to the requirements.
All the data required to be presented to the user shall be shown on the screen of the car.
System contains 3 different buttons as shown in the images: a. 2 buttons in the car's middle console where each button is used to control one of the two seat heaters. b. 1 extra button in the steering wheel to control the driver seat heater to make the usage of the heater easier for the driver.
Functionality:

For each seat the user shall input the required level of heating (off, low, medium, or high) where initially off is set and each press goes one step further (from off to low, from low to medium, from medium to high, and from high to off once again).
The heater will be driven from a signal to control its intensity: a. If the current temperature is less than the desired temperature by 10°C or more the heater should be enabled with the high intensity. b. If the current temperature is less than the desired temperature by 5°C to 10°C the heater should be enabled with a medium intensity. c. If the current temperature is less than the desired temperature by 2°C to 5°C the heater should be enabled with a low intensity. d. If the current temperature is more than the desired temperature the heater should be disabled. e. The heater shall be enabled once again if the temperature becomes less than the desired temperature by 3°C. f. Note that for the purpose of testing only the heater level shall control the LED : i. Green color indicates low intensity. ii. Blue color indicates medium intensity. iii. Cyan color indicates high intensity.
The temperature sensor shall be connected to the ADC so that the current temperature is measured correctly. a. You can use an LM35 temperature sensor to measure the temperature. i. Refer to the datasheet of the sensor for its specifications. b. For the purpose of testing only, you can use a potentiometer connected to the ADC instead of the temperature sensor in order to take the temperature as input from the user with the following specifications: i. 0v-3.3v is mapped to the range 0°C-45°C. ii. Note that only the range 5°C-40°C shall be treated as the valid range.
The current temperature, the heating level, and the heater state should be displayed on the screen by sending it through the UART.
If failure was detected in the temperature sensor the seat assigned to such sensor shall stop from controlling the temperature and the red LED shall be ON to inform the user that there is a problem with the sensor.
Requirements:

It is required to implement the controller unit using Tiva C.
Software shall use FreeRTOS for handling different tasks and objects. a. The system shall be well-designed with at least 6 tasks. b. Task implementation shall be reused for two different instances (one for the driver seat and another for the passenger seat) if required. c. Shared resources must be handled such that exclusive access to the resource is achieved. d. Signals and events must be correctly handled between different tasks. e. Data sharing between different tasks must be handled properly without any loss of data. f. Responsiveness to buttons shall be as high as possible.
GPIO, UART, GPTM, and ADC modules shall be part of the MCAL modules and used in the software.
Diagnostics shall be implemented where each of the following will be stored in the RAM a. The failure along with the timestamp (using GPTM) at which the failure occurred. b. The last heating level set by the user (off, low, medium, or high) with its timestamp shall be recorded.
Runtime measurements shall be made using the GPTM for the system to monitor the following parameters: a. Execution time for each task. b. CPU load. c. Resource lock time per task for each resource. Testing Scenario:
The user set the heating level to high while the temperature was 10°C.
Initially the heater will be driven with high intensity.
When the temperature reaches 25°C the heater will be driven with medium intensity.
When the temperature reaches 30°C the heater will be driven with low intensity.
When the temperature reaches 35°C or more the heater will be disabled.
Whenever the temperature goes down to 32°C, the heater will be reenabled with low intensity.
The required data will be sent by UART to be displayed on the screen.
If the temperature was sensed to be with a value less than 5°C or more than 40°C the controlling of the temperature shall be disabled, and the user shall be informed by enabling the LED according to the requirements. Bonus: Implement non-volatile memory for the diagnostics part:
The last heating level set by the user (off, low, medium, or high) with its timestamp shall be saved in the non-volatile memory.
The diagnostics issues logged in the system shall be saved in the non-volatile memory as well.
