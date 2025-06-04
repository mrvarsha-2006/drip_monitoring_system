#CODE

#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include "HX711.h"

// Pin configuration
#define LOADCELL_DOUT_PIN  23
#define LOADCELL_SCK_PIN   19
#define BUZZER_PIN  27  // Pin for the buzzer

// Calibration factor (to convert raw HX711 value to grams)
float calibration_factor = 1.0;

// Known reference weight in grams for calibration
const float known_weight = 500.0; // 500 grams real weight

HX711 scale;

// Initialize the LCD (address 0x27, 16 chars, 2 lines)
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  Serial.begin(115200);
  lcd.init();
  lcd.backlight();
  lcd.clear();

  // Initialize HX711 load cell
  scale.begin(LOADCELL_DOUT_PIN, LOADCELL_SCK_PIN);

  // Initialize buzzer pin
  pinMode(BUZZER_PIN, OUTPUT);
  digitalWrite(BUZZER_PIN, LOW); // Buzzer off initially

  lcd.print("Calibrating...");
  Serial.println("Starting calibration...");

  // Remove any weight (or tare) for zero offset
  scale.tare();

  delay(1000);

  // Read average raw value for zero offset
  long zero_offset = scale.read_average(20);
  Serial.print("Zero offset raw value: ");
  Serial.println(zero_offset);

  // Ask user to place the known weight (500g) on the load cell
  lcd.clear();
  lcd.print("Place 500g weight");
  Serial.println("Place 500g weight on the scale");
  delay(5000); // time to place weight

  // Read average raw value with known weight
  long raw_with_weight = scale.read_average(20);
  Serial.print("Raw with 500g weight: ");
  Serial.println(raw_with_weight);

  // Calculate calibration factor
  calibration_factor = (float)(raw_with_weight - zero_offset) / known_weight;
  Serial.print("Calibration factor: ");
  Serial.println(calibration_factor, 6);

  lcd.clear();
  lcd.print("Calibration Done");
  delay(2000);
  lcd.clear();
}

void loop() {
  // Read raw value and apply calibration
  long raw_value = scale.read_average(10);

  // Convert raw to grams using calibration factor
  float weight = (float)raw_value / calibration_factor;

  // Clamp negative weights to zero
  if(weight < 0) weight = 0;

  // Display weight on LCD
  lcd.setCursor(0, 0);
  lcd.print("Weight (g):      "); // Clear previous value
  lcd.setCursor(12, 0);
  lcd.print(weight, 2); // Display weight with 2 decimals

  // Check if weight is below threshold and sound the buzzer
  if (weight <= 210.0) { // Adjust threshold for buzzer alarm
    digitalWrite(BUZZER_PIN, HIGH);  // Turn buzzer on
    lcd.setCursor(0, 1);
    lcd.print("INSUFFICIENT FLUID "); // Display alarm message
    lcd.setCursor(0, 2);
    lcd.print("LEVEL              "); // Clear line - second line for alarms if LCD has two lines, else omit this line
  } else {
    digitalWrite(BUZZER_PIN, LOW);   // Turn buzzer off
    lcd.setCursor(0, 1);
    lcd.print("                ");  // Clear alarm line
  }

  // Print weight to Serial for monitoring
  Serial.print("Weight (g): ");
  Serial.println(weight, 2);

  delay(500);
}
