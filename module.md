[Materi](https://raw.githubusercontent.com/kym-wa/handson-smk/main/Materi-Arduino.pdf)

## Exercise 1

```c++
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
```

## Exercise 2

<img src="schematic/Exercise 2.png" style="height: 500px;"/>

```c++
void setup() {
  pinMode(3, OUTPUT);
}

void loop() {
  digitalWrite(3, HIGH);
  delay(1000);
  digitalWrite(3, LOW);
  delay(1000);
}
```

## Exercise 3

```c++
void setup() {
  pinMode(3, OUTPUT);
}

void loop() {
  analogWrite(3, 100);
}
```

### Exercise 3.1

```c++
void setup() {
  pinMode(3, OUTPUT);
}

void loop() {
  for (int i = 0; i < 255; i++) {
    analogWrite(3, i);
    delay(10);
  }

  for (int i = 255; i > 0; i--) {
    analogWrite(3, i);
    delay(10);
  }
}
```

## Exercise 4

<img src="schematic/Exercise 4.png" style="height: 500px;"/>

```c++
void setup() {
  pinMode(A0, INPUT);
  Serial.begin(115200);
}

void loop() {
  int a0 = analogRead(A0);
  Serial.println(a0);
}
```

## Exercise 5

<img src="schematic/Exercise 5.png" style="height: 500px;"/>

```c++
void setup() {
  pinMode(A0, INPUT);
  pinMode(3, OUTPUT);
  Serial.begin(115200);
}

void loop() {
  int a0 = analogRead(A0);
  Serial.println(a0);
  if(a0 > 100) {
    digitalWrite(3, LOW);
  }
  else {
    digitalWrite(3, HIGH);
  }
}
```

## Exercise 6

<img src="schematic/Exercise 6.png" style="height: 500px;"/>

```c++
void setup() {
  pinMode(7, INPUT_PULLUP);
  Serial.begin(115200);
}

void loop() {
  int pb = digitalRead(7);
  Serial.println(pb);
}
```

## Exercise 7

<img src="schematic/Exercise 7.png" style="height: 500px;"/>

[Download Library](https://raw.githubusercontent.com/kym-wa/handson-smk/main/library/Arduino-IRremote-master.zip)

```c++
#include <IRremote.h>

int IR_RECEIVE_PIN = 11;

void setup()
{
  Serial.begin(115200);
  IrReceiver.begin(IR_RECEIVE_PIN);
}

void loop() {
  if (IrReceiver.decode()) {
    IrReceiver.printIRResultShort(&Serial);
    IrReceiver.resume();
  }
}
```

## Exercise 8

```c++
#include <IRremote.h>

int IR_RECEIVE_PIN = 11;

void setup()
{
  Serial.begin(115200);
  pinMode(13, OUTPUT);
  IrReceiver.begin(IR_RECEIVE_PIN);
}

void loop() {
  if (IrReceiver.decode()) {
    IrReceiver.printIRResultShort(&Serial);
    IrReceiver.resume();

    if (IrReceiver.decodedIRData.command == 0x16) {
      Serial.println("0");
      digitalWrite(13, LOW);
    } else   if (IrReceiver.decodedIRData.command == 0xC) {
      Serial.println("1");
      digitalWrite(13, HIGH);
    }
  }
}
```
