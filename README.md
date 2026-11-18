# Animaciones OLED en ESP32-C3 (SSD1306 128x64)

Dos bocetos de Arduino que reproducen animaciones fotograma a fotograma en una pantalla OLED de 128x64 píxeles con controlador SSD1306 por I2C. Puedes ver el código y usarlo en tus proyectos.

| Carpeta | Archivo | Fotogramas | Velocidad |
|---|---|---|---|
| `SonrisitaS_prueba2/` | `SonrisitaS_prueba2.ino` | 1589 | 30 FPS |
| `ComotevasasiPrueba4/` | `ComotevasasiPrueba4.ino` | 1009 | 30 FPS |

## Materiales

- Placa ESP32-C3 (por ejemplo ESP32-C3 SuperMini o un DevKit con ESP32-C3)
- Pantalla OLED 0.96" de 128x64 con controlador SSD1306 e interfaz I2C (dirección `0x3C`)
- 4 cables dupont
- Cable USB para programar la placa

## Conexiones

| Pantalla OLED | ESP32-C3 |
|---|---|
| VCC | 3V3 |
| GND | GND |
| SDA | GPIO 5 |
| SCL | GPIO 6 |

Los pines están definidos en el código (`PIN_SDA 5` y `PIN_SCL 6`). Si los cambias, cambia también estas conexiones.

Notas:

- Si tu pantalla no responde, prueba con la dirección `0x3D` cambiando `OLED_ADDR` en el código.
- Si el monitor serie muestra `ERROR: SSD1306 no encontrado`, revisa que SDA y SCL no estén invertidos.

## Cómo subirlo

1. Instala el [Arduino IDE](https://www.arduino.cc/en/software) (versión 2.x).
2. Agrega el soporte para ESP32: en *Archivo → Preferencias*, en "URLs adicionales del gestor de tarjetas", pega `https://espressif.github.io/arduino-esp32/package_esp32_index.json`. Luego, en *Herramientas → Placa → Gestor de tarjetas*, instala **esp32** de Espressif Systems.
3. Instala las librerías desde *Herramientas → Administrar bibliotecas*:
   - **Adafruit GFX Library**
   - **Adafruit SSD1306**
4. Selecciona la placa **ESP32C3 Dev Module** (*Herramientas → Placa*).
5. Importante: en *Herramientas → Partition Scheme*, elige **Huge APP (3MB No OTA/1MB SPIFFS)**. Las animaciones ocupan más de 1 MB de memoria flash y no caben en el esquema por defecto.
6. Abre el archivo `.ino` de la animación que quieras, selecciona el puerto de tu placa y pulsa **Subir**.
7. Para ver los fotogramas y los FPS reales, abre el *Monitor serie* a **115200 baudios**.

## Ajustes

Al inicio de cada `.ino` hay opciones que puedes cambiar:

| Constante | Valor por defecto | Función |
|---|---|---|
| `TARGET_FPS` | `30` | Velocidad de reproducción objetivo |
| `DROP_FRAMES` | `1` | Salta fotogramas si el microcontrolador va atrasado |
| `INVERT_COLORS` | `0` | Invierte blanco y negro |
| `DEBUG_FPS` | `1` | Muestra información y FPS por el monitor serie |
| `OLED_ADDR` | `0x3C` | Dirección I2C de la pantalla |
| `I2C_CLOCK` | `800000UL` | Velocidad del bus I2C |

## Agradecimientos

Gracias a **lenkenane** por ver el código.
