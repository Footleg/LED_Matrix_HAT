# Footleg Robotics LED Matrix Driver HAT

Drive up to 3 chains of HUB75 type RGB LED Matrix panels in parallel with the LED matrix driver HAT from Footleg Robotics.

Supports HUB75 panels with the E address line (64 x 64 RGB LEDs).
Drives the LED panels with 5V logic for reliable signals.
Running all 3 channels requires all the GPIO pins on the Raspberry Pi. Alternatively, 2 channels can be used for driving LED panels, leaving the I2C and SPI pins available to connect additional devices, via JSH-PH connectors on the HAT. Channel 3 can be disabled with a solder jumper in case the level shifter interferes with I2C.
Supports panels which use Pin 4 or Pin 8 for the E address line (selected via a solder jumper). For panels which do not have an E address line these can both be set to GND, freeing up the GPIO 15 pin on the Pi (broken out to an RxD header on the HAT).
The board provides 3.3V power for I2C and SPI devices (max 1A) via a linear regulator powered off the 5V supply.
The Raspberry Pi can be powered through a 5V power input header on the HAT, via an ideal diode to protect from back powering if the Pi is also connected to power directly.

The recommended library for driving LED Matrix Panels on a Raspberry Pi is the <https://github.com/hzeller/rpi-rgb-led-matrix> library by Henner Zeller.
You will need to add a custom hardware mapping for the Footleg Robotics LED matrix driver HAT into the hardware-mapping.c code file before compiling the libray. The struc to add into this file is included below (or take the complete updated source file from the src folder in this repository).

```
  /*
   * Custom hardware mapping used by the 3 channel LED Matrix driver HAT 
   * from Footleg Robotics.
   */
  {
    .name          = "footleg-robotics",

    .output_enable = GPIO_BIT(18),
    .clock         = GPIO_BIT(17),
    .strobe        = GPIO_BIT(4),

    /* Address lines */
    .a             = GPIO_BIT(22),
    .b             = GPIO_BIT(23),
    .c             = GPIO_BIT(24),
    .d             = GPIO_BIT(25),
    .e             = GPIO_BIT(15),  /* RxD kept free unless 1:64 */

    /* Parallel chain 0, RGB for both sub-panels */
    .p0_r1         = GPIO_BIT(26),
    .p0_g1         = GPIO_BIT(27),  /* Not on RPi1, Rev1; use "regular-pi1" instead */
    .p0_b1         = GPIO_BIT(14),  /* masks TxD */
    .p0_r2         = GPIO_BIT(8),   /* masks: SPI0_CE0   */
    .p0_g2         = GPIO_BIT(16),
    .p0_b2         = GPIO_BIT(21),

    /* All the following are only available with 40 GPIP pins, on A+/B+/Pi2,3 */
    /* Chain 1 */
    .p1_r1         = GPIO_BIT(12),
    .p1_g1         = GPIO_BIT(5),
    .p1_b1         = GPIO_BIT(6),
    .p1_r2         = GPIO_BIT(19),
    .p1_g2         = GPIO_BIT(13),
    .p1_b2         = GPIO_BIT(20),

    /* Chain 2 */
    .p2_r1         = GPIO_BIT(11),  /* masks: SPI0_SCKL when parallel=3 */
    .p2_g1         = GPIO_BIT(2),   /* masks SCL when parallel=3 */
    .p2_b1         = GPIO_BIT(3),   /* masks SDA when parallel=3 */
    .p2_r2         = GPIO_BIT(7),   /* masks: SPI0_CE1 when parallel=3, also mapped to SPI0 CS */
    .p2_g2         = GPIO_BIT(9),   /* masks: SPI0_MISO when parallel=3 */
    .p2_b2         = GPIO_BIT(10),  /* masks: SPI0_MOSI when parallel=3 */
  },

```

You can find more example animations to try on your panels in my RGB Animations Library project at <https://github.com/Footleg/RGBMatrixAnimations>
