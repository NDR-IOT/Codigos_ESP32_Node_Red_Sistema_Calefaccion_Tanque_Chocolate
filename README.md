# Sistema de Calefacción - Tanque de Chocolate

Sistema mecatrónico que mantiene el chocolate a una temperatura de 44°C ± 1 °C, el agua viene de un tanque pulmón donde calienta a 48°C ± 1 °C. Controlado por un ESP32 con PID + SSR, y supervisado desde Node-RED vía MQTT.

## 📁 Contenido del repositorio

- `Codigo_ESP32` → firmware del ESP32 (Arduino IDE, `.ino`)
- `Codigo_Node_Red` → flujo del dashboard (Node-RED, importar como JSON)

## 🔧 Hardware

| Componente | Cantidad | Pin ESP32 |
|---|---|---|
| ESP32 DevKit C v4 | 1 | — |
| DS18B20 (pulmón) | 1 | GPIO 32 |
| DS18B20 (encamisado) | 1 | GPIO 33 |
| HC-SR04 (nivel) | 1 | TRIG 19, ECHO 18 |
| Relé niquelina (SSR) | 1 | GPIO 25 |
| Relé válvula | 1 | GPIO 26 |
| Relé agitador | 1 | GPIO 27 |
| Bomba (PWM) | 1 | GPIO 4 |
| OLED SSD1306 | 1 | SDA 13, SCL 14 |
| Buzzer | 1 | GPIO 5 |
| LEDs indicadores | 5 | 2, 15, 21, 16, 17 |

## 🚀 Cómo usarlo

### 1. Cargar el ESP32
1. Abre `Codigo_ESP32` en Arduino IDE.
2. Modifica `WIFI_SSID` y `WIFI_PASS` con tus credenciales reales.
3. Instala las librerías: `PubSubClient`, `OneWire`, `DallasTemperature`,
   `ArduinoJson`, `Adafruit SSD1306`, `Adafruit GFX`.
4. Selecciona la placa "ESP32 Dev Module" y carga.

### 2. Importar el flujo de Node-RED
1. Instala `node-red-dashboard`:
   ```bash
   cd ~/.node-red
   npm install node-red-dashboard@3.6.6

Abre Node-RED → menú → Import.
Pega el contenido de Codigo_Node_Red o súbelo como archivo.
Deploy.
Abre http://localhost:1880/ui.

📡 Topics MQTT
choco_tanque/telemetria → ESP32 → Node-RED

choco_tanque/alertas → ESP32 → Node-RED

choco_tanque/comandos → Node-RED → ESP32

Broker por defecto: broker.hivemq.com:1883 (público).
