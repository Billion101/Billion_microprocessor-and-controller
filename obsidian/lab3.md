
# ການທົດລອງຕໍ່ວົງຈອນ Labs  : 3 RGB

## I. ຈຸດປະສົງຂອງວົງຈອນການທົດລອງ
RGB ແມ່ນ ຊຸດຫຼອດໄຟ LED ທີ່ມີຫຼອດໄຟ LED ສີແດງ, ຂຽວ ແລະນ້ຳເງິນລວມກັນໃນຊຸດດຽວ ຕາມປົກກະຕິແລ້ວ ໄຟ LED ແບບ RGB ສາມາດສ້າງສີຕ່າງໆ ທີ່ມອງເຫັນໄດ້ຄ່ອນຂ້າງຄົບຄຸມ. ຢ່າງໃດກໍ່ຕາມ, ຂໍ້ຈຳກັດຂອງໄຟປະເພດນີ້ ແມ່ນວ່າທັງຊຸດຂອງໄຟ LED ຈະສາມາດສ້າງແສງສີດຽວໃນເວລາດຽວກັນເທົ່ານັ້ນ ແລະໃຊ້ເອັຟເຟັກແສງແບບດຽວກັນ ເນື່ອງຈາກມີ IC ຕົວດຽວຄວບຄຸມການເຮັດວຽກ.
RGB ໃນໂປຣເຈັກນີ້ຈະເປັນການທີ່ທີ່ໃຊ້ຄໍາສັ່ງໃຫ້ດອກໄຟປ່ຽນສີຂອງມັນຕາມຄ່າທີ່ເຮົາເຊັດໄວ້ ແລະ ໃຊ້ຄຳສັ່ງໂດຍສັ່ງຜ່ານ Serial Monitor ຫລື ຜ່ານບອດຂອງວົງຈອນໃນການປ່ຽນສີຂອງໂດຍໄຟ.

___

## II. ອຸປະກອນ

| ຊື່            | ຈຳນວນ |
|---------------|--------|
| Arduino IDE  | 1      |
| Breadboard   | 1      |
| Resistor (220Ω) | 1      |
| RGB         | 1      |

___

## III.	ວົງຈອນແລະcode
![](../image/36.png) 
![](../image/37.png) 
~~~cpp
int ledPins[] = {11, 10, 9};

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);

  // Using for loop instead of range-based for-each loop
  for (int i = 0; i < sizeof(ledPins) / sizeof(ledPins[0]); i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  // put your main code here, to run repeatedly:
  
  while (Serial.available() > 0) {
    // read input from serial monitor
    String input = Serial.readStringUntil('\n'); // Read until newline

    // Turn off all LEDs using a for loop
    for (int i = 0; i < sizeof(ledPins) / sizeof(ledPins[0]); i++) {
      digitalWrite(ledPins[i], LOW);
    }
    delay(10);

    if (input == "on" || input == "rgb" || input == "rbg" || input == "grb" || input == "gbr" || input == "brg" || input == "bgr" ) {
      // Turn on all LEDs using a for loop
      for (int i = 0; i < sizeof(ledPins) / sizeof(ledPins[0]); i++) {
        digitalWrite(ledPins[i], HIGH);
      }
    }

    else if (input == "off") {
      // Turn off all LEDs using a for loop
      for (int i = 0; i < sizeof(ledPins) / sizeof(ledPins[0]); i++) {
        digitalWrite(ledPins[i], LOW);
      }
    }

    else if (input == "r") {
      digitalWrite(ledPins[0], HIGH);
    }

    else if (input == "g") {
      digitalWrite(ledPins[1], HIGH);
    }

    else if (input == "b") {
      digitalWrite(ledPins[2], HIGH);
    }
    
    else if (input == "rg" || input == "gr") {
      digitalWrite(ledPins[0], HIGH);
      digitalWrite(ledPins[1], HIGH);
    }
    else if (input == "rb" || input == "br") {
      digitalWrite(ledPins[0], HIGH);
      digitalWrite(ledPins[2], HIGH);
    }
    else if (input == "gb" || input == "bg") {
      digitalWrite(ledPins[1], HIGH);
      digitalWrite(ledPins[2], HIGH);
    }
    else {
      allColors();
    }
  }
}

void allColors() {
  //WHITE
  for (int i = 0; i < sizeof(ledPins) / sizeof(ledPins[0]); i++) {
    digitalWrite(ledPins[i], HIGH);
  }
  delay(100);
  for (int i = 0; i < sizeof(ledPins) / sizeof(ledPins[0]); i++) {
    digitalWrite(ledPins[i], LOW);
  }
  delay(100);

  //RED, GREEN, BLUE
  for (int i = 0; i < sizeof(ledPins) / sizeof(ledPins[0]); i++) {
    digitalWrite(ledPins[i], HIGH);
    delay(100);
    digitalWrite(ledPins[i], LOW);
    delay(100);
  }

  //RED + GREEN index 0 and index 1
  for (int i = 0; i < 2; i++) {
    digitalWrite(ledPins[i], HIGH);
  }
  delay(100);
  for (int i = 0; i < 2; i++) {
    digitalWrite(ledPins[i], LOW);
  }
  delay(100);

  //RED BLUE index 0 and index 2
  for (int i = 0; i < 3; i += 2) {
    digitalWrite(ledPins[i], HIGH);
  }
  delay(100);
  for (int i = 0; i < 3; i += 2) {
    digitalWrite(ledPins[i], LOW);
  }
  delay(100);

  // GREEN + BLUE index 1 and index 2  
  for (int i = 1; i < 3; i++) {
    digitalWrite(ledPins[i], HIGH);
  }
  delay(100);

  for (int i = 1; i < 3; i++) {
    digitalWrite(ledPins[i], LOW);
  }
  delay(100);
}
~~~
<!-- ![](../image/38.png) 
![](../image/39.png) 
![](../image/40.png) 
![](../image/41.png)  -->
## IV.	ຜົນຂອງການທົດລອງ
ຜົນການທົດລອງການສາມາດສະຫລຸບໄດ້ວ່າ ການເຮັດວຽກຂອງດອກໄຟ LED ນັ້ນໄດ້ມີການສະແດງຜົນຕາມທີ່ເຮົາຕ້ອງ,ໂດຍມັນຈະມີການຮຸ້ງ-ດັບສະຫລັບກັນ 1 ວິນາທີ. ໂດຍຫລັງມັນຈະເຮັດວຽກແລ້ວຈະມີການວົນຊ້ຳ(loop)ໄປເລື້ອຍໆຈົນກສ່າເຮົາສັ່ງຈຸດການເຮັດວຽກມັນ.
[Go to Next Page](lab4.md)
[Back to Last Page](lab2.md)