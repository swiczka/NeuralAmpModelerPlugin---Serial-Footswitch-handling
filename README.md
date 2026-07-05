# Neural Amp Modeler Plug-in - Serial Footswitch Handling & A/B Switching

This is a fork of the original [Neural Amp Modeler Plugin](https://github.com/sdatkinson/NeuralAmpModelerPlugin) by Steven Atkinson. It implements handling for serial-port-based footswitches (e.g., DIY Arduino pedals or other non-MIDI foot controllers) and allows real-time model switching.

## Features & How to Use

Same as original Gateway. The difference is you can plug two models at once: Model A and B and between switch them in real time.

You can also control output level for each model individually.

## Serial Port Configuration (IMPORTANT NOTE)

To trigger the model change action via a custom footswitch/microcontroller (e.g., Arduino), your device must send specific data over the serial port:

* **Trigger Command:** Send the string `"NEXT"` (NEXT or NEXT\n work just fine)
* **Baud Rate:** 9600
* **Port Selection:** The app automatically scans available COM ports

### Arduino Example Code:
```cpp
#define FOOTSWITCH 12 //define hardware location of footswitch on Arduino board

void setup() {
  Serial.begin(9600);
}

void loop() 
{
  int currentState = digitalRead(FOOTSWITCH);
  
  if (currentState != lastFootswitchState){
    Serial.println("NEXT");
    delay(50);
  }

  lastFootswitchState = currentState;
}
