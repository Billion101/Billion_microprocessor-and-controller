
# ການທົດລອງຕໍ່ວົງຈອນ Labs  : 8 Servo Motor

## I. ຈຸດປະສົງຂອງວົງຈອນການທົດລອງ
Servo Motor ແມ່ນອຸປະກອນທີ່ສາມາດຄວບຄຸມເຄື່ອງຈັກ ຫລື ລະບົບການເຮັດວຽກໃຫ້ເປັນໄປຕາມຄວາມຕ້ອງການ ເຊັ່ນ ຄວບຄຸມຄວາມໄວ (Speed), ຄວບຄຸມແຮງບິດ (Torque), ຄວບຄຸມຕໍາແໜ່ງ (Position) ໂດຍໃຫ້ຜົນລັບຕາມຄວາມຕ້ອງການດ້ວຍຄວາມແມ່ນຍໍາສູງ.
Servo Motor ເປັນໂປຣເຈັກທີ່ໃຊ້ໂຕຂອງ Potentiometer ໃນການຄວນບຄຸມການໝຸມຂອງ Motor.






___

## II. ອຸປະກອນ

| ຊື່            | ຈຳນວນ |
|---------------|--------|
| Arduino IDE  | 1      |
| Breadboard   | 1      |
| Potentiometer      | 1      |
| Servo Motor        | 1      |




___

## III.	ວົງຈອນແລະcode
![](../image/58.png) 
![](../image/59.png) 
___
<!-- ![](../image/60.png)  -->
~~~cpp
#include <Servo.h>

Servo myservo;  // create servo object to control a servo

int potpin = A0;  // analog pin used to connect the potentiometer
int val;    // variable to read the value from the analog pin

void setup() {
  Serial.begin(9600);
  myservo.attach(9);  // attaches the servo on pin 9 to the servo object
 
}

void loop() {
  val = analogRead(potpin);           // reads the value of the potentiometer (value between 0 and 1023)
  Serial.print("pot = ");
  Serial.print(val);
  Serial.print(", servo = ");
  val = map(val, 0, 1023, 0, 180);     // scale it to use it with the servo (value between 0 and 180)
  
  Serial.println(val);
  myservo.write(val);                  // sets the servo position according to the scaled value
  delay(15);                           // waits for the servo to get there
}

~~~
## IV.	ຜົນຂອງການທົດລອງ
ຜົນການທົດລອງການສາມາດສະຫລຸບໄດ້ວ່າ: ໂດຍມັນເປັນວົງຈອນທີ່ຈະໃຊ້ Potentiometer ໃນການຄວບຄຸມການໝຸມຂອງ Servo Motor. ເຊີ່ງ Servo Motor ມັນຈະມີການໝຸມຈະມີການເຄື່ອນທີ່ຕາມການບິດຂອງ Potentiometer ແລະ ມັນຈະສາມາດໝຸມໄດ້ທີ່ 180 ອົງສາ.
[Go to Next Page](lab9.md)
[Back to Last Page](lab7.md)