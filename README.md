# DopaDriver: Project Description

Desired features of the project:

- Smallest Possible Footprint
- Can drive DC motors as well as BLDCs
- System Condition Monitoring:
    - Over Current Protection
    - Over Voltage Protection
    - Under Voltage Protection
    - Over Temperature Protection
    - Reverse Polarity Protection
- Driving via PWM
- High Current(for Drone applications)
- Super Capacitor Output and Normal Capacitor Output
- Up to 6S, with high current capabilities.

The objective is to design a highly compact motor driver that is versatile enough to efficiently drive both DC and BLDC motors, ideal for drone applications requiring high currents. This motor driver will incorporate state-of-the-art system condition monitoring and protection features, alongside advanced control techniques—particularly incorporating Sinusoidal Pulse Width Modulation (SPWM) for harmonics reduction, which is critical for enhancing the performance and efficiency of BLDC motors.

### Key Features and Specifications:

- **Versatile Compatibility:** Capable of driving DC and BLDC motors, making it suitable for a wide range of drone applications.
- **System Condition Monitoring:**
    - **Over Current Protection:** To prevent damage from excessive currents.
    - **Over and Under Voltage Protection:** Ensures the driver operates within safe voltage levels.
    - **Over Temperature Protection:** Monitors system temperature to avoid overheating.
    - **Reverse Polarity Protection:** Guards against incorrect battery installation.
- **Advanced Control Techniques:** Utilizes SPWM for driving BLDC motors, which reduces harmonics, decreases torque ripple, and improves overall motor efficiency and performance. This method involves modulating the PWM in such a manner that the voltage waveform approximates a sinusoidal shape, leading to smoother operation and less noise.
- **PWM Driving:** Employs PWM signals for efficient speed and torque control of the motors, now enhanced with SPWM technique for BLDC motors to ensure quieter operation, reduced vibration, and improved efficiency.
- **High Current Capability:** Designed to cater to drone applications that demand high current, ensuring robust performance even under demanding conditions.
- **Energy Storage Options:** Features both supercapacitor and normal capacitor buffers to manage high surge currents effectively, providing a stable power supply during rapid acceleration or deceleration phases.
- **Voltage Range Adaptability:** Supports up to a 6S LiPo battery configuration, catering to high current applications without compromising on safety and reliability.

### Design Goals:

- **Minimal Footprint:** Despite the integration of advanced features and high current capabilities, the design aims for the smallest possible size to fit compact drones, optimizing space without sacrificing performance.
- **Harmonics Reduction:** Through the integration of SPWM control, the project emphasizes reducing electrical noise and improving motor efficiency, which is vital for the longevity and reliability of both the motors and the driver.
- **High Performance under Dynamic Conditions:** Ensures that the motor driver can handle high current demands swiftly and efficiently, making it ideal for drones that require quick responses and high maneuverability.

### Modus Operandi

1. **Initial Detection Phase:**
    - Upon power-up or through a user-triggered event, the motor driver enters detection mode.
    - The driver momentarily injects a low current into the motor windings and measures the response, which differs between DC and BLDC motors.
2. **Detecting Back EMF for BLDC Motors:**
    - For BLDC motors, injecting a current into one phase and measuring the induced Back EMF (Electromotive Force) in the open phases can confirm the presence of a BLDC motor.
    - The characteristic waveform of the Back EMF, which varies with rotor position, confirms that a 3-phase motor is connected.
    - An algorithm can analyze the presence or absence of Back EMF, its phase relationship, and its amplitude to ensure accurate detection.
3. **DC Motor Detection:**
    - If no Back EMF is detected, or if the response does not match the expected pattern for a BLDC motor, the system can assume a DC motor is connected.
    - For DC motors, applying a small test voltage and measuring the resulting current flow can confirm the presence of a DC motor. The system should expect a direct relationship between applied voltage and current, without the phase shift characteristic of BLDC motors.

### Configuration Post-Detection

1. **For BLDC Motors:**
    - Once a BLDC motor is detected, all three half-bridges are activated, and the driver switches to using SPWM control for smooth and efficient operation.
    - The control algorithm adjusts to maintain optimum efficiency, performance, and harmonics reduction based on the real-time analysis of the motor's behavior.
2. **For DC Motors:**
    - If a DC motor is detected, the driver configures two of the half-bridges to operate in an H-bridge configuration, suitable for driving DC motors. This enables control over the direction and speed of the DC motor through PWM.
    - The system can dynamically adjust PWM parameters to optimize performance and efficiency for the detected DC motor.

### Safety and Protections

- Regardless of the motor type, protection features (overcurrent, overvoltage, undervoltage, overtemperature, and reverse polarity protection) remain active to ensure safe operation.
- Implement a timeout for the detection phase to prevent overstressing the motor with prolonged detection signals.
- Advanced features, like real-time monitoring and adaptive control, should be compatible with both motor types to enhance performance and protection.
