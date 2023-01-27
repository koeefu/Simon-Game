#include "pitches.h"
const int speaker = 11;
const int start = 20; // pin of starting button
const int quit = 21;  // pin of quiting button
int noteDurations = 500;
//NOTE_C4 yellow 6 262
//NOTE_D4 red 7 294
//NOTE_E4 green 8 330
//NOTE_F4 blue 9 349
int noteC4 = 262;
int noteD4 = 294;
int noteE4 = 330;
int noteF4 = 349;
int notes[] = {noteC4, noteD4, noteE4, noteF4};
int gameCounter = 0;
int simonOutput[5];
int playerInput[5];
int note;
int buttonPressed = 0;
int speakerMode = 1; //in this mode, speaker plays random notes and LEDs flash
int playerMode = 2; //in this mode, player inputs notes
int checkMode = 3; //in this mode, comparing the two arrays (speaker and player)
int endMode = 4; //in this mode, loop ends
int winMode = 5;
int currentMode;
void setup() {
pinMode(9, INPUT);    // set the pushbutton pin to be an input BLUE
pinMode(8, INPUT);    // set the pushbutton pin to be an input GREEN
pinMode(7, INPUT);    // set the pushbutton pin to be an input RED
pinMode(6, INPUT);    // set the pushbutton pin to be an input YELLOW
pinMode(2, OUTPUT);   // set the yellow LED pin to be an output GREEN
pinMode(3, OUTPUT);   // set the red LED pin to be an output YELLOW
pinMode(4, OUTPUT);   // set the yellow LED pin to be an output BLUE
pinMode(5, OUTPUT);   // set the red LED pin to be an output RED
pinMode(speaker, OUTPUT);
//simonTone();
Serial.begin(9600);
}
void loop() {
//different modes to make the loop happen
if (digitalRead(start) == HIGH) {
// give player some time to react, you can change the delay time
  delay(50);
  currentMode = speakerMode;
}
if (digitalRead(quit) == HIGH) {
// give player some time to react, you can change the delay time
  noTone(speaker);
  delay(50);
  Serial.println("endddd");
  currentMode = endMode;
  noTone(speaker);
  //Serial.println("endddd");
}
if (currentMode == speakerMode) {
  Serial.println("IAMSPEAKER");
  delay(500);
  simonTone();
  delay(500); // give player some time to react, you can change the delay time
  currentMode = playerMode;
} else if (currentMode == playerMode) {
  playerTone();
 } else if (currentMode == checkMode) {
  int playerDo = check();
  if (playerDo == true){
    if (gameCounter < 4) {
      currentMode = speakerMode;
      gameCounter ++;
    } else if (gameCounter == 4) {
      currentMode = winMode;
      gameCounter = 0;
    }
  } else
    {currentMode = endMode;}
} else if (currentMode == endMode) {
  end();
} else if (currentMode == winMode) {
  win();
}

void simonTone() {
for (int i = 0; i < 5; i++) {
int x = random(0, 4);
 note = notes[x];
tone(speaker, note, 1000); //make speaker play
delay(80);
digitalWrite(x + 2, HIGH); //make LED work
delay(500);
digitalWrite(x + 2, LOW);
simonOutput[i] = note;
}
noTone(speaker);
}
// the function about player inputing notes
void playerTone() {
if (digitalRead(6) == HIGH) {
  tone(speaker, notes[0], noteDurations);
  playerInput[buttonPressed] = NOTE_C4;
  buttonPressed ++;
  digitalWrite(2, HIGH);
  delay(500);
  digitalWrite(2, LOW);
  digitalWrite(3, LOW);
  digitalWrite(4, LOW);
  digitalWrite(5, LOW);
} else if (digitalRead(7) == HIGH) {
  tone(speaker, notes[1], noteDurations);
  playerInput[buttonPressed] = NOTE_D4;
  buttonPressed ++;
  digitalWrite(3, HIGH);
  delay(500);
  digitalWrite(2, LOW);
  digitalWrite(3, LOW);
  digitalWrite(4, LOW);
  digitalWrite(5, LOW);
} else if (digitalRead(8) == HIGH) {
  tone(speaker, notes[2], noteDurations);
  playerInput[buttonPressed] = NOTE_E4;
  buttonPressed ++;
  digitalWrite(4, HIGH);
  delay(500);
  digitalWrite(2, LOW);
  digitalWrite(3, LOW);
  digitalWrite(4, LOW);
  digitalWrite(5, LOW);
} else if (digitalRead(9) == HIGH) {
  tone(speaker, notes[3], noteDurations);
  playerInput[buttonPressed] = NOTE_F4;
  buttonPressed ++;
  digitalWrite(5, HIGH);
  delay(500);
  digitalWrite(2, LOW);
  digitalWrite(3, LOW);
  digitalWrite(4, LOW);
  digitalWrite(5, LOW);
}  else {
  digitalWrite(2, LOW);
  digitalWrite(3, LOW);
  digitalWrite(4, LOW);
  digitalWrite(5, LOW);
  noTone(11);
}
if (buttonPressed == 5) {
  currentMode = checkMode;
  buttonPressed = 0;
}
delay(10);
}
//function about comparing elements in two arrays
bool check() {
bool playerDo = true;
 for (int i = 0; i < 5; i ++) {
 if (simonOutput[i] != playerInput[i]) {
    playerDo = false; 
    break;
  }
}
if (playerDo == true) {
  answerTrue();
  currentMode == speakerMode;
  Serial.println("true");
} else if (playerDo == false) {
  answerFalse();
  Serial.println("false");
}
return playerDo;
}
void answerTrue() {
//play the LED in a way we like
}
void answerFalse() {
//play the LED in a way we like
tone(speaker, 392 , noteDurations);
delay(noteDurations);
tone(speaker, 370 , noteDurations);
delay(noteDurations);
tone(speaker, 349 , noteDurations);
delay(noteDurations);
tone(speaker, 330 , noteDurations);
delay(noteDurations);
tone(speaker, 331 , noteDurations);
delay(noteDurations);
noTone(speaker);
}
void end() {
//noTone(speaker);
tone(speaker, 392 , noteDurations);
delay(noteDurations);
tone(speaker, 370 , noteDurations);
delay(noteDurations);
tone(speaker, 349 , noteDurations);
delay(noteDurations);
tone(speaker, 330 , noteDurations);
delay(noteDurations);
tone(speaker, 331 , noteDurations);
delay(noteDurations);
noTone(speaker);
while (digitalRead (20) != HIGH) {};
currentMode = playerMode;
}


void win() {
//noTone(speaker);
tone(speaker, 740 , noteDurations);
delay(noteDurations);
tone(speaker, 784 , noteDurations);
delay(noteDurations);
tone(speaker, 349 , noteDurations);
delay(noteDurations);
tone(speaker, 330 , noteDurations);
delay(noteDurations);
tone(speaker, 831 , noteDurations);
delay(noteDurations);
noTone(speaker);


while (digitalRead (20) != HIGH) {};
currentMode = playerMode;
}
