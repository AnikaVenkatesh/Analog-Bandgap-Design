# Analog-Bandgap-Design

<img width="1536" height="735" alt="image" src="https://github.com/user-attachments/assets/554123be-ac88-426a-b838-aae639cb829a" />

This repository documents the learning experience from a 10-day Analog Bandgap Design Workshop by VSD Corp. Pvt. Ltd.

# Introduction

<img width="560" height="218" alt="BGR1" src="https://github.com/user-attachments/assets/0d8f909a-47af-4800-9888-bb9b21111cc0" />


A Bandgap Reference (Voltage Reference) is one of the most important building blocks in analog integrated circuit design. It is used to generate a stable reference voltage that remains nearly constant despite variations in supply voltage, temperature, and process parameters. In real-world operating conditions, temperature fluctuations and supply noise are unavoidable, and without a reliable reference, the performance of analog and mixed-signal circuits degrades significantly.

The bandgap reference overcomes these challenges by combining temperature-dependent components in a controlled manner. By adding a PTAT (Proportional To Absolute Temperature) voltage with a CTAT (Complementary To Absolute Temperature) voltage, the overall temperature dependence is minimized. This results in a reference voltage typically close to 1.2 V, which serves as a stable baseline for many on-chip circuits.

# Bandgap Reference Classifications

Bandgap reference circuits can be classified based on their internal architecture. One common approach is the self-biased bandgap reference, where the circuit generates its own bias currents using internal feedback. This architecture is compact and power-efficient, making it suitable for low-power systems and system-on-chip (SoC) applications.

Another widely used architecture is the operational-amplifier-based bandgap reference. In this approach, an op-amp enforces precise voltage or current relationships between circuit nodes, resulting in improved accuracy, better power-supply rejection ratio (PSRR), and enhanced stability. Although this architecture consumes slightly more power and area, it is preferred in precision analog and mixed-signal designs.

**Applications**

- In data converters such as ADCs and DACs, the bandgap reference provides a stable voltage against which analog signals are compared or reconstructed. The accuracy, linearity, and resolution of these converters depend heavily on the quality of the reference voltage, making the bandgap reference a critical component in high-performance data conversion systems. 

- In power management circuits, bandgap references are extensively used in low-dropout regulators (LDOs) and voltage monitoring circuits. The reference voltage defines the regulated output level and ensures reliable operation across varying load conditions and supply fluctuations. A stable bandgap reference directly contributes to efficient and safe power delivery.

- Bandgap references are also essential in integrated systems and sensors. They are used in on-chip temperature sensors, oscillators, and phase-locked loops (PLLs), where stable biasing is required for accurate sensing and frequency generation. Any drift in the reference voltage can lead to timing errors or frequency instability.

- In digital and mixed-signal ICs, bandgap references provide bias voltages and currents for high-speed logic, memory circuits, and I/O interfaces. Consistent biasing across temperature and process corners ensures predictable performance and improves overall system reliability.

- In application-specific domains such as RF systems, portable IoT devices, and industrial electronics, bandgap references play a vital role in maintaining stable operation under wide temperature ranges and low-power constraints. Their ability to deliver a reliable reference voltage makes them indispensable in modern analog and mixed-signal IC design.

**System on Chip (SoC) - "Vref" connected across various blocks**

<img width="718" height="421" alt="image" src="https://github.com/user-attachments/assets/7093bacc-4055-4d1a-9fb6-9870a65164b7" />

# Working Principle

<img width="751" height="490" alt="BGR" src="https://github.com/user-attachments/assets/3ad564a4-cee9-4311-8012-2c1335c9d500" />

<img width="749" height="455" alt="BGR_Principle" src="https://github.com/user-attachments/assets/74b6ac01-3e92-4dc5-a9ac-402b2b780c79" />



Methods to realize voltage references in integrated circuits.

-  Making use of a zener diode that breaks down at a known voltage when reverse biased.

- Making use of the difference in the threshold voltage between an enhancement transistor and a depletion transistor.

- Cancelling the negative temperature dependence of a pn junction with a positive temperature dependence from a PTAT (proportional-to-absolute-temperature) circuit.

Among these methods, the CTAT–PTAT based approach is the most popular and robust for both bipolar and CMOS technologies. The bandgap voltage reference is based on combining the voltage of a forward-biased diode or base-emitter junction, which has a negative temperature coefficient (CTAT), with a voltage that is proportional to absolute temperature (PTAT). The resulting sum produces a reference voltage that is nearly independent of temperature. In a bandgap reference, the PTAT voltage is generated by amplifying the voltage difference between two forward-biased PN junctions (or base-emitter junctions) operating at different current densities. This voltage difference increases linearly with temperature. When this PTAT voltage is added to the CTAT voltage of a single diode-connected junction, the temperature dependencies cancel each other, resulting in a stable reference voltage close to the silicon bandgap voltage.

**Base-emitter voltage as a funcion of collector current and temperature**

<img width="811" height="90" alt="image" src="https://github.com/user-attachments/assets/b4108f5f-592f-4444-ab0b-6be5fee4c4fa" />

**Proportional to Absolute Temperature(PTAT) circuit cancels the temperature coefficient of the Vbe**

<img width="703" height="109" alt="image" src="https://github.com/user-attachments/assets/f692e3e3-3df7-4e42-9f1b-a3add6ea47e8" />

# Design Specifications 

VSD Workshop Requirements:

⦁ Supply voltage = 1.8V

⦁ Temperature: -40 to 125 Deg Cent.

⦁ Power Consumption < 60uW

⦁ Off current < 2uA

⦁ Start-up time < 2us

⦁ Tempco. Of Vref < 50 ppm

**MOSFET**

<img width="812" height="195" alt="image" src="https://github.com/user-attachments/assets/04f42301-f26b-4fbc-928a-7b28ee01637d" />

**BJT**

<img width="629" height="217" alt="image" src="https://github.com/user-attachments/assets/adf3ee3a-710a-475c-8459-2968f3229bf4" />

**RESISTOR**

<img width="664" height="187" alt="image" src="https://github.com/user-attachments/assets/c820a34f-d380-4544-84dc-f97497b25b4f" />

# Design

<img width="263" height="505" alt="Equation" src="https://github.com/user-attachments/assets/31fc6f2b-acb1-4f31-9262-2670eade081f" />


**1. Current Calculation**

Max. power Consumption < 60uW

Max Total Current = 60 uW/1.8V=33.33uA

So, we have chosen 10uA/branch, (3*10=30uA)

Start-up current 1-2 uA

**2. Choosing Number of BJT in parallel in Branch2**

Less number of BJT: require less resistance value but matching hampers

More number of BJT: requires higher resistance value but gives good matching

So a moderate number have chosen (8 BJT) for better layout matching and moderate resistance value.

**3. Calculation of R1**

R1= Vt* ln (8)/I =26 mv *ln(8)/10.7uA=5 KOhm

R1 size: W=1.41um, L=7.8um, Unit res value: 2k Ohm

Number of resistance needed: 2 in series and 2 in parallel (2+2+(2||2))

**4. Calculation of R2**

Current through ref branch:I3=I2=Vt*ln(8)/R1

Voltage across R2: R2I3=R2/R1(Vtln(8))

Slope of VR2= R2/R1 (ln(8)*115uv)/Deg Cent.

Slope of VQ3=-1.6mV/Deg cent

Adding both and equating to zero, R2 will be around 33k Ohm

Number of resistance needed: 16 in series and 2 in parallel (2+2...+2+ (2||2))

**5. SBCM Design (Self-biased Current Mirror)**

**A. PMOS Design in SBCM**

Make both the MP1 and MP2 well in Saturation

To reduce channel length modulation used L=2um

Finally the size is L=2u, W=5u and M=4

**B. NMOS Design in SBCM**

Make both the MN1 and MN2 either in Saturation or in deep sub-threshold

We have made it in deep sub-threshold

To reduce channel length modulation used L=1um

Finally the size is L=1u, W=5u and M=8

## Final Circuit

<img width="822" height="518" alt="finalbgr" src="https://github.com/user-attachments/assets/11873efd-aed2-4a46-b18f-c7a271c74195" />


## Analog Design Flow (Opensource Tools & PDK)

<img width="710" height="727" alt="Screenshot 2026-02-24 000554" src="https://github.com/user-attachments/assets/69d021e7-d2ab-471c-bbe4-d378dd6c448e" />

# Lab Simulations 

**1. CTAT Simulation**

<img width="1366" height="643" alt="Screenshot from 2026-02-25 02-38-24" src="https://github.com/user-attachments/assets/abdc6c0a-d539-4846-9dbb-2eaf74851043" />


**Spice Execution PLot**


<img width="1652" height="871" alt="ctat@2v" src="https://github.com/user-attachments/assets/3f2aed50-08d6-45d5-87c5-5e8ef3227eba" />















