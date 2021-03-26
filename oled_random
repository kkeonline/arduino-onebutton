#include <OneButton.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128 // OLED display width, in pixels
#define SCREEN_HEIGHT 32 // OLED display height, in pixels
#define SCREEN_ADDRESS 0x3C ///< See datasheet for Address; 0x3D for 128x64, 0x3C for 128x32
#define OLED_RESET 4

/* 
 * Connecting
 * Pin 11 - Push Switch
 * Pin 13 - Builtin LED
 * A4 - OLED SDA
 * A5 - OLED SCL
 */
#define SW_PIN 11
#define LED_PIN 13
#define LOOP_DELAY 10
#define MODES 8
#define SEED_MAX 30
#define SHUFFLE_DELAY 80
#define RANDOM_DELAY 120
#define TOP_ROW 6

char* myChar[] = { "/", "-", "\\", "|", "/", "-", "\\", "|" };
int seed = 0;
int mode = 0;
int smode = 1;

OneButton button(SW_PIN, true);
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

void shuffle() {
  int c1 = 64;
  for (int j = 0; j < 7; j++) {
    for (int i = 0; i < 4; i++) {
      display.clearDisplay();
      display.setCursor(c1, TOP_ROW);
      display.print(myChar[i]);
      display.display();
      delay(SHUFFLE_DELAY);
    }
  }
}

void shuffle2(int a, int b) {
  int c1 = 40;
  int c2 = 88;
  for (int j = 0; j < 5; j++) {
    for (int i = 0; i < 4; i++) {
      display.clearDisplay();
      display.setCursor(c1, TOP_ROW);
      display.print(myChar[i + 1]);
      display.setCursor(c2, TOP_ROW);
      display.print(myChar[i]);
      display.display();
      delay(SHUFFLE_DELAY);
    }
  }
  delay(RANDOM_DELAY);
  for (int j = 0; j < 2; j++) {
    for (int i = 0; i < 4; i++) {
      display.clearDisplay();
      display.setCursor(c1, TOP_ROW);
      display.print(a);
      display.setCursor(c2, TOP_ROW);
      display.print(myChar[i]);
      display.display();
      delay(SHUFFLE_DELAY);
    }
  }
  delay(RANDOM_DELAY);
  display.clearDisplay();
  display.setCursor(c1, TOP_ROW);
  display.print(a);
  display.setCursor(c2, TOP_ROW);
  display.print(b);
  display.display();
}

void shuffle3(int a, int b, int c) {
  int c1 = 30;
  int c2 = 62;
  int c3 = 94;
  for (int j = 0; j < 5; j++) {
    for (int i = 0; i < 4; i++) {
      display.clearDisplay();
      display.setCursor(c1, TOP_ROW);
      display.print(myChar[i + 2]);
      display.setCursor(c2, TOP_ROW);
      display.print(myChar[i + 1]);
      display.setCursor(c3, TOP_ROW);
      display.print(myChar[i]);
      display.display();
      delay(SHUFFLE_DELAY);
    }
  }
  delay(RANDOM_DELAY);
  for (int i = 0; i < 6; i++) {
    display.clearDisplay();
    display.setCursor(c1, TOP_ROW);
    display.print(a);
    display.setCursor(c2, TOP_ROW);
    display.print(myChar[i + 1]);
    display.setCursor(c3, TOP_ROW);
    display.print(myChar[i]);
    display.display();
    delay(SHUFFLE_DELAY);
  }
  delay(RANDOM_DELAY);
  for (int i = 2; i < 8; i++) {
    display.clearDisplay();
    display.setCursor(c1, TOP_ROW);
    display.print(a);
    display.setCursor(c2, TOP_ROW);
    display.print(b);
    display.setCursor(c3, TOP_ROW);
    display.print(myChar[i]);
    display.display();
    delay(SHUFFLE_DELAY);
  }
  delay(RANDOM_DELAY);
  display.clearDisplay();
  display.setCursor(c1, TOP_ROW);
  display.print(a);
  display.setCursor(c2, TOP_ROW);
  display.print(b);
  display.setCursor(c3, TOP_ROW);
  display.print(c);
  display.display();
}

void show(int i, int c = 64) {
  display.clearDisplay();
  display.setCursor(c, 6);
  display.print(i);
  display.display();
}

void showc(String s, int c = 0) {
  display.clearDisplay();
  display.setCursor(c, 6);
  display.print(s);
  display.display();
}

void showtext(int i) {
  switch (i) {
    case 1:
      showc("White 1", 6);
      break;
    case 2:
      showc("Skip", 32);
      break;
    case 3:
      showc("Blue 1", 16);
      break;
    case 4:
      showc("Any 2", 24);
      break;
    case 5:
      showc("Blue 1", 16);
      break;
    case 6:
      showc("Any 3", 24);
      break;
    case 7:
      showc("Any 1", 24);
      break;
    case 8:
      showc("White 1", 6);
      break;
  }
}

void doRandom() {
  int r;
  digitalWrite(LED_PIN, HIGH);
  switch (mode) {
    case 1:
      shuffle();
      delay(RANDOM_DELAY);
      showtext(random(1, 8));
      break;
    case 2:
      shuffle();
      delay(RANDOM_DELAY);
      show(random(2, 5));
      break;
    case 3:
      shuffle();
      delay(RANDOM_DELAY);
      r = random(1, 6);
      if (r == 6) {
        showc("Skip", 32);
      } else {
        show(r);
      }
      break;
    case 4:
      shuffle();
      delay(RANDOM_DELAY);
      show(random(1, 6));
      break;
    case 5:
      shuffle2(random(1, 6), random(1, 6));
      break;
    case 6:
      shuffle3(random(1, 6), random(1, 6), random(1, 6));
      break;
    case 7:
      shuffle();
      delay(RANDOM_DELAY);
      show(random(1, 9));
      break;
    case 8:
      shuffle();
      delay(RANDOM_DELAY);
      show(random(1, 99));
      break;
  }
}

void setMode() {
  smode++;
  if (smode > MODES) {
    smode = 1;
  }
  showMode(smode);
}

void showMode(int i) {
  display.clearDisplay();
  display.setCursor(8, 6);
  display.print("Mode:");
  display.print(i);
  display.display();
}

void doSetMode() {
  display.clearDisplay();
  display.setCursor(32, 6);
  display.print("Set");
  display.display();
  delay(1500);
  display.clearDisplay();
  display.setCursor(16, 6);
  display.print("Ready");
  display.display();
  delay(300);
}

void btnClick() {
  if (mode == 0) {
    setMode();
  } else {
    digitalWrite(LED_PIN, HIGH);
    doRandom();
    seed++;
    if (seed > SEED_MAX) {
        randomSeed(micros());
        seed=0;
    }
    delay(1500);
    digitalWrite(LED_PIN, LOW);
  }
}

void btnLongPress() {
  if (mode == 0) {
    mode = smode;
    doSetMode();
    randomSeed(micros());
    seed = 0;
    digitalWrite(LED_PIN, LOW);
  } else {
    smode = mode;
    mode = 0;
    showMode(smode);
    digitalWrite(LED_PIN, HIGH);
  }
}

void setup() {
  Serial.begin(9600);
  pinMode(LED_PIN, OUTPUT);
  if(!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
    Serial.println(F("SSD1306 allocation failed"));
    for(;;); // Don't proceed, loop forever
  }
  display.display();
  display.setTextColor(WHITE);
  display.setTextWrap(false);
  display.setTextSize(3);
  showMode(smode);
  digitalWrite(LED_PIN, HIGH);
  button.attachClick(btnClick);
  button.attachLongPressStart(btnLongPress);
}

void loop() {
  button.tick();
  delay(LOOP_DELAY);
}
