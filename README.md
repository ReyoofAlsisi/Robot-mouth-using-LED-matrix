# Robot-mouth-using-LED-matrix

I connected an LED matrix to an Arduino to create a robotic mouth. First, I wired the LED matrix to the Arduino by linking each row and column of LEDs to specific pins on the microcontroller, allowing precise control over each individual LED. After setting up the hardware, I wrote Arduino code to manage the LED matrix. The code enables the LED matrix to display animations that simulate mouth movements, such as opening and closing or forming different expressions. This setup allows the robotic mouth to visually convey various emotions and responses, enhancing the robot's interaction and communication capabilities.


Code:

#include <LedControl.h>

int DIN = 11;
int CS = 7;
int CLK = 13;
LedControl lc = LedControl(DIN, CLK, CS, 1); // Initialize for 1 display

void setup() {
  lc.shutdown(0, false);
  lc.setIntensity(0, 8); 
  lc.clearDisplay(0);  
  lc.setScanLimit(0, 7); 
}

void loop() {
  // Display each face expression in sequence

  displayNeutralFace();
  delay(1000); // Hold for 1 second

  displayHappyFace();
  delay(1000); // Hold for 1 second

  displaySadFace();
  delay(1000); // Hold for 1 second
}

// Function to display a neutral face
void displayNeutralFace() {
  byte neutralFace[8] = {
    B00111100, // Row 1: Eyes
    B01000010, // Row 2: Eyes
    B00111100, // Row 3: Empty
    B00000000, // Row 4: Empty
    B11111111, // Row 5: Straight mouth
    B00000000, // Row 6: Empty
    B00000000, // Row 7: Empty
    B00000000  // Row 8: Empty
  };

  for (int i = 0; i < 8; i++) {
    lc.setRow(0, i, neutralFace[i]);
  }
}

// Function to display a happy face
void displayHappyFace() {
  byte happyFace[8] = {
    B00111100, // Row 1: Eyes
    B01000010, // Row 2: Eyes
    B00111100, // Row 3: Empty
    B00000000, // Row 4: Empty
    B00111100, // Row 5: Middle of the smile
    B01000010, // Row 6: Ends of the smile
    B00000000, // Row 7: Empty
    B00000000  // Row 8: Empty
  };

  for (int i = 0; i < 8; i++) {
    lc.setRow(0, i, happyFace[i]);
  }
}

// Function to display a sad face
void displaySadFace() {
  byte sadFace[8] = {
    B00111100, // Row 1: Eyes
    B01000010, // Row 2: Eyes
    B00111100, // Row 3: Empty
    B00000000, // Row 4: Empty
    B01000010, // Row 5: Ends of the frown
    B00111100, // Row 6: Middle of the frown
    B00000000, // Row 7: Empty
    B00000000  // Row 8: Empty
  };

  for (int i = 0; i < 8; i++) {
    lc.setRow(0, i, sadFace[i]);
  }
}
