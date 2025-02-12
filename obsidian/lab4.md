
# ການທົດລອງຕໍ່ວົງຈອນ Labs  : 4 Buzzer

## I. ຈຸດປະສົງຂອງວົງຈອນການທົດລອງ
Buzzer (ບັຊເຊີຣ໌) ຄື ອຸປະກອນກຳເນີດສຽງ ທີ່ໃຊ້ໃນລະບົບອີເລັກໂທຣນິກ ເພື່ອສ້າງສຽງແຈ້ງເຕືອນ, ສັນຍານ, ຫລືເພື່ອໃຫ້ສຽງປິ່ງປ່ອງຕ່າງໆ. ປະເພດຂອງ Buzzer ມີຄື:
1.	Passive Buzzer (ບັຊເຊີຣ໌ແບບບໍ່ມີວົງຈອນ)
o	ຕ້ອງໃຊ້ສັນຍານຄວາມຖີ່ (PWM) ເພື່ອຄວບຄຸມສຽງ
o	ສາມາດສ້າງສຽງດັງ ແລະ ປ່ຽນຄວາມຖີ່ສຽງໄດ້
2.	Active Buzzer (ບັຊເຊີຣ໌ແບບມີວົງຈອນໃນຕົວ)
o	ໃຫ້ສຽງໄດ້ໂດຍການຈ່າຍໄຟ DC ໃສ່
o	ສຽງຄົງທີ່ ແລະ ບໍ່ສາມາດປ່ຽນຄວາມຖີ່ໄດ້
3.	Buzzer (ບັຊເຊີຣ໌) ໃນໂປຣເຈັກນີ້ຈະເປັນການທີ່ເຮົາຈະເຮັດໃຫ້ມັນສົາງສຽງເປັນໂນດຂອງເພງຊາດລາວຂອງເຮົາ.


___

## II. ອຸປະກອນ

| ຊື່            | ຈຳນວນ |
|---------------|--------|
| Arduino IDE  | 1      |
| Breadboard   | 1      |
| Buzzer         | 1      |

___

## III.	ວົງຈອນແລະcode
![](../image/42.png) 
![](../image/43.jpeg) 

<!-- ![](../image/44.png) 
![](../image/45.png) 
![](../image/46.png) 
![](../image/47.png)  -->
~~~cpp
// Notes frequencies (in Hz) for different pitches
#define NOTE_C2 65
#define NOTE_D2 73
#define NOTE_E2 82
#define NOTE_F2 87
#define NOTE_G2 98
#define NOTE_A2 110
#define NOTE_B2 123

#define NOTE_C3 130
#define NOTE_D3 146
#define NOTE_E3 164
#define NOTE_F3 174
#define NOTE_G3 196
#define NOTE_A3 220
#define NOTE_B3 246

#define NOTE_C4 261
#define NOTE_D4 293
#define NOTE_E4 659
#define NOTE_F4 698
#define NOTE_G4 783
#define NOTE_A4 880
#define NOTE_B4 987


// Melody notes and durations
int melody[] = {
NOTE_D4, NOTE_D4, NOTE_D4, NOTE_C4, 
NOTE_E4, NOTE_D4, NOTE_C2, NOTE_G3,
NOTE_A3, NOTE_B3, NOTE_C4, NOTE_A3,
NOTE_C4, NOTE_B3, NOTE_A3, NOTE_B3,
NOTE_C4, NOTE_B3, NOTE_A3, NOTE_G3,
NOTE_E3, NOTE_D3, NOTE_E3, NOTE_F3,
NOTE_G3, NOTE_E3, NOTE_C3, NOTE_D3, 
NOTE_G2, NOTE_C3, NOTE_D3, NOTE_E3,
NOTE_F3, NOTE_G3, NOTE_F3, NOTE_A3,
NOTE_G3, NOTE_F3, NOTE_E3, NOTE_D3,
NOTE_C3, NOTE_D3, NOTE_E3, NOTE_F3,
NOTE_E3, NOTE_E3, NOTE_D3, NOTE_C3,
NOTE_D3, NOTE_E3, NOTE_G3, NOTE_E3,
NOTE_D3, NOTE_C3, NOTE_C4, NOTE_C4,
NOTE_A3, NOTE_G3, NOTE_A3, NOTE_C4,
NOTE_A3, NOTE_A3, NOTE_D4, NOTE_C4,
NOTE_A3, NOTE_G3, NOTE_E3, NOTE_G3,
NOTE_E3, NOTE_D3, NOTE_C3, NOTE_C3,
NOTE_C3, NOTE_C3, NOTE_C3, NOTE_D3,
NOTE_E3, NOTE_D3, NOTE_C3, NOTE_G3,
NOTE_G3, NOTE_G3, NOTE_G3, NOTE_E3,
NOTE_G3, NOTE_A3, NOTE_B3, NOTE_A3,
NOTE_G3, NOTE_E3, NOTE_A3, NOTE_G3,
NOTE_E3, NOTE_D3, NOTE_C3, NOTE_A2,
NOTE_G2, NOTE_A2, NOTE_C3
};
int noteDurations[] = {
  2, 2, 2, 2, 
  2, 2, 4, 2,
  2, 2, 4, 2, 
  2, 1, 2, 2,
  2, 2, 2, 2,
  4, 2, 2, 2,
  2, 2, 2, 1,
  2, 2, 3, 2,
  2, 1, 2, 2,
  2, 2, 2, 1,
  2, 2, 2, 2,
  2, 2, 3, 2,
  2, 2, 2, 2,
  2, 1, 2, 2,
  2, 3, 3, 2,
  2, 2, 2, 2,
  2, 2, 2, 1,
  3, 2, 2, 3,
  3, 3, 2, 3,
  2, 2, 2, 2,
  2, 1, 2, 2,
  2, 3, 3, 2,
  2, 2, 2, 2,
  2, 2, 2, 2,
  2, 2, 1, 
};

void setup() {
  // No setup needed
}

void loop() {
  // Play each note in the melody
  for (int i = 0; i < 200; i++) {
    int noteDuration = 1000 / noteDurations[i]; // Note duration in milliseconds
    tone(8, melody[i], noteDuration);          // Play the note on pin 8
    delay(noteDuration * 1.3);                 // Pause between notes
    noTone(8);                                 // Stop the tone
  }
  
  delay(2000); // Pause before repeating the melody
}
~~~
## IV.	ຜົນຂອງການທົດລອງ
ຜົນການທົດລອງການສາມາດສະຫລຸບໄດ້ວ່າ: ໂປຣເຈັກນີ້ຈະເປັນການສົ່ງສຽງຕາມຄຳສັ່ງຂອງເຮົາເຊັດຄ່າເອົາໄວ້. ເຊີ່ງໄດ້ມີການເລືອກເປັນໂນດຂອງເພງຊາດລາວ.
[Go to Next Page](lab5.md)
[Back to Last Page](lab3.md)