SAARD: Smart Assistive Activity Recognition Device
An ML-powered assistive device that helps visually and hearing impaired people understand their surroundings. It recognizes objects through a camera, speaks what it sees, and warns the user about nearby obstacles with a buzzer and vibration.
> Final-year B.E. (CSE) project, VTU, Angadi Institute of Technology & Management, Belagavi (2021-22). Published in IJCRT: [https://www.ijcrt.org/viewfull.php?&p_id=IJCRT2208186].
![SAARD prototype in blind-stick form](images/saard-prototype.jpg)
Problem
Most assistive tools target a single disability (blind or deaf) or focus only on communication. They don't tell users what is around them, so users stay dependent on other people. SAARD aims to give differently abled people a low-cost, real-time device that describes their environment and alerts them to obstacles.
Features
Object recognition with audio output: a camera captures the scene, a pretrained model detects objects, and the result is spoken to the user
Obstacle alerts: an ultrasonic sensor detects objects within about 3 meters and triggers a buzzer and vibration motor through the microcontroller
Vibration alerts for sound: designed to help users with hearing impairment (see the project report)
Remote image alert: can send a captured image to a phone through LINE Notify
How it works
The ESP32-CAM streams video over Wi-Fi to a small web page.
The page runs COCO-SSD (TensorFlow.js) to detect objects trained on the COCO dataset, drawing bounding boxes with confidence scores.
Detected object names are converted to speech and played through headphones.
In parallel, the ultrasonic sensor measures distance. When an obstacle is within range, the Arduino UNO activates the buzzer and vibration motor.
Tech stack
Area	Tools
Hardware	ESP32-CAM, Arduino UNO, ultrasonic sensor, buzzer, vibration motor, FTDI module
ML	TensorFlow.js, COCO-SSD, COCO dataset
Languages	C/C++ (Arduino), JavaScript
Other	Web Speech API, LINE Notify
Setup
Install the Arduino IDE and the ESP32 board package.
Open the sketch in `code/` and set your own Wi-Fi name and password:
```cpp
   const char* ssid     = "YOUR_WIFI_NAME";
   const char* password = "YOUR_WIFI_PASSWORD";
   ```
Connect the ESP32-CAM through the FTDI module and upload the sketch.
Open the Serial Monitor to find the device IP, then open it in a browser to see the live detection page.
Wire the ultrasonic sensor, buzzer and vibration motor to the Arduino UNO as described in the project report.
> Never commit real Wi-Fi passwords or LINE Notify tokens. Keep them in a local config file that is listed in `.gitignore`.
Results
![Detection output on mobile](images/output-mobile.png)
The prototype detects everyday objects in real time and speaks the label, and the obstacle alert triggers when something comes close.
Limitations and future work
No sign language support (this needs a separate dataset and model)
Does not recognize traffic lights or road signs without further training
The device can be made more compact and wearable
Team
Tejashwini Bhosale
Shruti Kambar
Sunita Channametri
Tejashwini Ankale
Guide: Prof. Anjana Kulkarni, Dept. of CSE, AITM Belagavi
