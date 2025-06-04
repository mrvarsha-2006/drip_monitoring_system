# Smart Intravenous Drip Infusion Monitoring System

Greetings everybody!  This system uses **ESP32**, **load cell**, and **Blynk IoT** to automate IV fluid monitoring in hospitals.  It's intended to lessen the burden of nurses and avoid backflow problems by offering **remote access**, **alerts**, and **real-time fluid level tracking**.

---

## 📌 Features

- 📶 Real-time IV fluid monitoring using load cell & HX711
- 📲 Blynk IoT integration for remote access via smartphone/web
- 🔔 Audio alerts using a buzzer when levels fall below 50% and 10%
- 📨 Email alerts for nurses when the IV is nearly empty
- 🖥️ LCD showing live fluid weight and percentage

---

## 🧰 Hardware Used

- ESP32 microcontroller
- Load Cell
- HX711 Load Cell Amplifier
- IV Bag
- LCD with I2C module
- Buzzer
- Power Supply

---

## 💻 Software Used

- **Arduino IDE** – for coding and uploading to ESP32
- **Blynk IoT** – for creating dashboard & sending notifications

---

## 🛠️ Setup Instructions

### 1. Hardware Connections
- Connect **Load Cell** to **HX711**, and then to ESP32
- Connect **LCD** with I2C to ESP32
- Connect **Buzzer** to a GPIO pin (example: pin 14)

### 2. Software Configuration
- Open Arduino IDE and install these libraries:
  - `Blynk`
  - `HX711`
  - `LiquidCrystal_I2C`
- Replace `WiFi SSID`, `Password`, and `Blynk Auth Token` in the code

### 3. Upload the Code
- Use the USB cable to connect the ESP32 to your laptop
- Upload the code from Arduino IDE to the ESP32

### 4. Blynk IoT Dashboard
- Go to [https://blynk.cloud](https://blynk.cloud)
- Create a **Template** and assign **Virtual Pins** (V0, V1, V2)
- Set up **email notification** in the "Events" section

---

## 🚀 How It Works

1. Load cell continuously reads IV fluid weight.
2. ESP32 processes the data, calculates the percentage left.
3. Info is displayed on LCD and sent to the Blynk dashboard.
4. Alerts are triggered:
   - 50% → short buzzer sound + email alert
   - 10% → continuous buzzer + critical email

---

## 📊 Results

- Monitored IV fluid weight with 95%+ accuracy
- Real-time updates shown on LCD and Blynk web/app
- Alerts successfully sent during low fluid conditions

---

## 🔮 Future Improvements

- Monitor multiple IV bags using a multiplexer
- Mobile app with patient-specific alerts
- Data logging and analytics
- Add battery backup and SMS alerts
- Use machine learning to predict fluid depletion time

---

## 👩‍🔬 Authors

- **Varsha M R** 
- **Janani S** 

Project done as part of **Mini-project(23BM453)** at **Mepco Schlenk Engineering College**, May 2025.

---

## 📚 References

1. Deepa K et al., IoT Based Drip Infusion Monitoring System – IEEE, 2022  
2. Natapol Phetsuk et al., IV Drip Monitoring Device – RI2C, 2021  
3. Ananya Madhav et al., IoT-Based IV Monitoring – COMSNETS, 2021

---

