# Footleg Robotics LED Matrix Driver HAT
Documentation and code for the LED Matrix HUB75 triple channel driver HAT

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
