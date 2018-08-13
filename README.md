# OBD-II Information
This repository will cover the basics of reading and understanding information reguarding OBD-II.   

**WARNING**: Modifying your OBD-II system to a non-certified state is considered a Federal Offense. The information provided is only intended for reading from the OBD-II spec.

- [OBD-II Information](#obd-ii-information)
      - [Definition](#definition)
      - [Hardware](#hardware)
    + [Terminology](#terminology)
      - [Engine/Electronic Control Unit (ECU)](#engine-electronic-control-unit--ecu-)
      - [Diagnostic Trouble Code (DTC)](#diagnostic-trouble-code--dtc-)
        * [Letter Meaning](#letter-meaning)
        * [Difference Between Generic & Manufacturer Specific](#difference-between-generic---manufacturer-specific)
        * [System Application](#system-application)
    + [OBD-II Protocols](#obd-ii-protocols)
      - [SAE J1850 PWM](#sae-j1850-pwm)
      - [SAE J1850 VPW](#sae-j1850-vpw)
      - [ISO 9141-2](#iso-9141-2)
      - [ISO 14230 KWP2000](#iso-14230-kwp2000)
      - [ISO 15765 CAN](#iso-15765-can)

#### Definition
On-Board Diagnostics, or “OBD,” is a computer-based system built into all 1996 and later light-duty vehicles and trucks, as required by the Clean Air Act Amendments of 1990. OBD systems are designed to monitor the performance of some of an engine’s major components including those responsible for controlling emissions.

#### Hardware
Any vehicle manufacture from 1996 or later is required by law to have the OBD-II computer system. You can access this system through the Data Link Connector (DLC). It is a 16 pin connector that can tell you which protocol your car communicates with, depending on which pins are populated in it.  In cars, it will be located under the dash, near the driver’s seat, or in the vicinity of the ashtray – somewhere easily accessible from the driver’s seat without the use of tools to access it (i.e., you don’t need a screw driver to pull off a panel to get to it).

### Terminology

#### Engine/Electronic Control Unit (ECU)
The ECU can refer to a single module or a collection of modules. These are the brains of the vehicle. They monitor and control many functions of the car. These can be standard from the manufacturer, reprogrammable, or have the capability of being daisy-chained for multiple features. Tuning features on the ECU can allow the user to make the engine function at various performance levels and various economy levels. On new cars, these are all typically microcontrollers.

Some of the more common ECU types include:
- **Engine Control Module (ECM)** - This controls the actuators of the engine, affecting things like ignition timing, air to fuel ratios, and idle speeds.
- **Vehicle Control Module (VCM)** - Another module name that controls the engine and vehicle performance.
- **Transmission Control Module (TCM)** - This handles the transmission, including items like transmission fluid temperature, throttle position, and wheel speed.
- **Powertrain Control Module (PCM)** - Typically, a combination of an ECM and a TCM. This controls your powertrain.
- **Electronic Brake Control Module (EBCM)** - This controls and reads data from the anti-lock braking system (ABS).
- **Body Control Module (BCM)** - The module that controls vehicle body features, such as power windows, power seats, etc.

#### Diagnostic Trouble Code (DTC)
These codes are used to describe where an issue is occurring on the vehicle and are defined by SAE (you can find the whole spec here for a cost). These codes, can either be generic or unique to the vehicle manufacturer.

These codes take the following format:  
- The first section is the first character, which is always a letter.
- The second section is the next character, which is a single number, from 0 to 3.
- The third section is the third character, which is a single number from 0 to 9.
- The fourth and last section includes both the fourth and fifth characters together, so it is a pair of numbers, from 00 to 99. These are based on the systems defined in the third digit, and are the specific code failure.

##### Letter Meaning

**Powertrain Codes**

| Code  | Description |
| ------------- | ------------- |
| P0XXX  | Generic  |
| P1XXX  | Manufacturer-Specific  |
| P2XXX  | Generic  |
| P30XXX-P33XXX  | Manufacturer-Specific  |
| P34XXX-P39XXX  | Generic  |

The letter “P” indicates powertrain-related codes such as those involving the engine or the transmission and their sensors. Typically, “P” codes are the only ones that will illuminate the Check Engine Light.

**Body Codes**

| Code  | Description |
| ------------- | ------------- |
| B0XXX  | Generic  |
| B1XXX  | Manufacturer-Specific  |
| B2XXX  | Manufacturer-Specific  |
| B3XXX  | Generic  |

The letter “B” indicates a body code, which means that it relates to a body system such as the airbags.

**Chassis Codes**

| Code  | Description |
| ------------- | ------------- |
| C0XXX  | Generic  |
| C1XXX  | Manufacturer-Specific  |
| C2XXX  | Manufacturer-Specific  |
| C3XXX  | Generic  |

The letter “C” indicates a chassis code, used for systems such as the anti-lock brakes.

**Network Communication Codes**

| Code  | Description |
| ------------- | ------------- |
| U0XXX  | Generic  |
| U1XXX  | Manufacturer-Specific  |
| U2XXX  | Manufacturer-Specific  |
| U3XXX  | Generic  |

The letter “U” indicates network codes which are used for problems like module failures and losses of communication.

- **Note**: Only professional-grade or dealership scan tools are able to diagnose codes outside of powertrain codes.

##### Difference Between Generic & Manufacturer Specific

| Code Type  | Explanation |
| ------------- | ------------- |
| Generic  | Code is defined in the EOBD/OBD-II standard and will be the same for all manufacturers  |
| Manu-Spec  | Manufacturers may bee code is not available within the generic list, they can add their own codes  |

##### System Application
| Code Number | System |
| ------------- | ------------- |
| XX1XX | fuel or air metering system problem, such as an issue with the mass air flow sensor |
| XX2XX | fuel or air metering injection system issues, such as a fuel injector problem |
| XX3XX | ignition-related problem, such as an engine misfire |
| XX4XX | emissions system problems, like a catalytic converter efficiency issue |
| XX5XX | vehicle speed controls and idle control system problems |
| XX6XX | computer output circuit issues, like an internal computer failure |
| XX[7,8,9]XX | transmission-related problems, like pressure faults and sensor failures |

### OBD-II Protocols
There are five different communication protocols available under the OBD-II spec. Like so many things, manufacturers tend to have their preferences and think their protocol is best, hence the variation. Here’s a quick overview of each and a description of the pins used on the DLC for each.

#### SAE J1850 PWM
This signal is Pulse Width Modulation, which runs at 41.6 kbps. This protocol is generally used on Ford vehicles.

| Feature | Description |
| ------------- | ------------- |
| BUS + | Pin 2 |
| BUS - | Pin 10 |
| 12V | Pin 16 |
| GND | Pins 4, 5 |
| Bus State:  | Active when BUS + is pulled HIGH, BUS - is pulled LOW |
| Maximum Signal Voltage: | 5V |
| Minimum Signal Voltage: | 0V |
| Number of bytes: | 12 |
| Bit Timing: | '1' bit - 8uS, '0' bit - 16uS, Start of Frame - 48uS |

#### SAE J1850 VPW
This protocol is Variable Pulse Width, which runs at 10.4 kbps. GM vehicles typically use this version.

| Feature | Description |
| ------------- | ------------- |
| BUS + | Pin 2 |
| 12V | Pin 16 |
| GND | Pins 4, 5 |
| Bus State:  | Bus idles low |
| Maximum Signal Voltage: | +7V |
| Decision Signal Voltage: | +3.5V |
| Minimum Signal Voltage: | 0V |
| Number of bytes: | 12 |
| Bit Timing: | '1' bit -HIGH 64uS, '0' bit -HIGH 128uS, Start of Frame - HIGH 200uS |

#### ISO 9141-2
If you have a Chrysler, European, or Asian vehicle, this is your protocol. It runs at 10.4 kbps and is asynchronous serial communication.

| Feature | Description |
| ------------- | ------------- |
| K Line (bidirectional) | Pin 7 |
| L Line (unidirectional, optional) | Pin 15 |
| 12V | Pin 16 |
| GND | Pins 4, 5 |
| Bus State:  | K Line idles HIGH. Bus is active when driven LOW. |
| Maximum Signal Voltage: | +125V |
| Minimum Signal Voltage: | 0V |
| Number of bytes: | Message: 260, Data: 255 |
| Bit Timing: |UART: 10400bps, 8-N-1 |

#### ISO 14230 KWP2000
This is the Keyword Protocol 2000, another asynchronous serial communication method that also runs at up to 10.4 kbps. This also is used on Chrsyler, European, or Asian vehicles.

| Feature | Description |
| ------------- | ------------- |
| K Line (bidirectional) | Pin 7 |
| L Line (unidirectional, optional) | Pin 15 |
| 12V | Pin 16 |
| GND | Pins 4, 5 |
| Bus State:  | Active when driven LOW. |
| Maximum Signal Voltage: | +125V |
| Minimum Signal Voltage: | 0V |
| Number of bytes: | Data: 255 |
| Bit Timing: |UART: 10400bps, 8-N-1 |

#### ISO 15765 CAN
This protocol has been mandated in all vehicles sold in the US from 2008 and later. However, if you have a European car from 2003 or later, the vehicle may have CAN. It’s a two-wire communication method and can run at up to 1Mbps.


| Feature | Description |
| ------------- | ------------- |
| CAN HIGH (CAN H) | Pin 6 |
| CAN LOW (CAN L) | Pin 14 |
| 12V | Pin 16 |
| GND | Pins 4, 5 |
| Bus State:  | Active when CANH pulled HIGH, CANL pulled LOW. Idle when signals are floating. |
| CANH Signal Voltage: | +3.5V |
| CANL Signal Voltage: | +1.5V |
| Maximum Signal Voltage: | CANH = +4.5V, CANL = +2.25V |
| Minimum Signal Voltage: | CANH = +2.75V, CANL = +0.5V |
| Number of bytes: | L |
| Bit Timing: | 250kbit/sec or 500kbit/sec |
