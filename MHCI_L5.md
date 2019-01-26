# Mobile HCI
### Lecture 5 - Constraints
---

### Processing Power

In order to be small, and not consume so much power, mobile devices use weaker processors that PCs.

The key challenge is not always the max speed, but the fact that to extend battery life, we cannot use the processor for long periods.

### Battery Life

Will be a major issue for the foreseeable future. Therefore very important in "stand-by-modes" not to have processes more active than necessary. 

### Memory

There is often limited RAm and slow backing store (top devices now have > 8GB RAM). Mobile devices are resource constrained:
- Use memory efficiently and safely
- Release resources as early as possible
- Cope with out-of-memory and other errors and roll back to a consisten state when they occur

### Data Connection

A key issue is the cost of data transmission:
- Costs money and battery life
- Means a general need to be parsimonious
- Involve user in decisions about when to enable data
- If making an app that overuses data, it will accidentally cost a fortune.

RF Range:
- Cellular networks - Up to 30-45mioes range
- Wifi, 30m range
- Bluetooth, 10m range
- NFC, 10cm range

---

### Built in Sensors

Most mobile devices come with a range of sensors:
- Camera's, Accelerometers, Gyroscopes, Magnetometers etc
- Don't forget the microphone!
- External devices link in Heart Rate sensors
- Virtual sensors like step counters
- Fingerprint sensors
- Face recognition sensing

### Cameras

Some proto mobiles now have **depth sensing**, Google has Project Tango which is working on 3D mapping and motion tracking camera in a mobile phone.

---

### Resistive Touch Screens

1. Polyester Film
2. Upper Resistive Circuit Layer
3. Conductive ITO
4. Lower Resistive Circuit Layer
5. Insulating Dots
6. Glass/Acrylic Substrate
- Touching the overlay surface causes the **(2)** to contact the **(4)**, producing a circuit switch - The touchscreen controller gets the alternating voltages between **(4)** and **(2)** and converts them into the digital X and Y coordinates of the activated area.

### Capacitive Touch Screens

An **imaging processing controller** continuously makes a touch profile from a touch sensor on the outer layer. Controller then resolves touch profile to an actual touch point. The coordinates are fed back to the operating system. 


### User and Environmental Aspects

Have to take into account that users will take their devices into unpredictable circumstances:

- In bright sunlight, you cannot see the screen.
- In cold winters, with gloves on, you cannot use a touch screen (special gloves no available).
- Can be hard to use for people with large fingers, on a moving bus or while walking.
- GPS wont work indoors, or under tree cover
- RF communication can be blocked by building materials or landscape features
- Bluetooth signals can be blocked by the human body.

---

### Conclusions

- Lots of things are more challenging when developing for mobile platforms
- Can be good training for you
    - Forces more discipline, can't get away with lazy coding.
- Impressive apps no good if they drain the battery in a couple hours, or cost a fortune in data...
- Wide range of development platforms
    - More challenging than desktop envirnoment but rapidly improving 
- User and environment provide further constraints & opportunities
