#include <DHT.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// -------------------- DHT Setup --------------------
#define DHTPIN 2          // Data pin connected to D2
#define DHTTYPE DHT22     // DHT 22 sensor

DHT dht(DHTPIN, DHTTYPE);

// -------------------- LCD Setup --------------------
LiquidCrystal_I2C lcd(0x27, 16, 2); 
// If LCD doesn't work, try 0x3F instead of 0x27

void setup() {
  Serial.begin(9600);
  dht.begin();

  lcd.init();      
  lcd.backlight(); 

  lcd.setCursor(0, 0);
  lcd.print("DHT22 Sensor");
  delay(2000);
  lcd.clear();
}

void loop() {

  float humidity = dht.readHumidity();
  float temperature = dht.readTemperature();

  if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Failed to read from DHT sensor!");
    
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Sensor Error");
    delay(2000);
    return;
  }

  // ---- Serial Monitor Output ----
  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.print(" %  |  Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");

  // ---- LCD Output ----
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Hum: ");
  lcd.print(humidity);
  lcd.print(" %");

  lcd.setCursor(0, 1);
  lcd.print("Temp: ");
  lcd.print(temperature);
  lcd.print(" C");

  delay(2000);
}


<img width="872" height="669" alt="image" src="https://github.com/user-attachments/assets/3e2a5a50-977f-42a1-bce5-fdfddc529a2a" />
