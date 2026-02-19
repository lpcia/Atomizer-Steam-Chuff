# Atomizer-Steam-Chuff
Small circuit Using a 5V Humidifier/Atomizer Module to simulate Locomotive Steam Chuff using Track Power
# Complete Steam Chuff Controller Build Instructions
## Components List
555 Timer Circuit:
	•	1× NE555 timer IC
	•	1× 47kΩ resistor (charging resistor)
	•	1× 100kΩ potentiometer (chuff rate control)
	•	1× 10µF electrolytic capacitor (timing capacitor)
	•	1× 1N4148 diodes (asymmetric charge/discharge)
	•	1× 980Ω resistor (MOSFET gate resistor)
	•	1× 10kΩ resistor (MOSFET gate pull-down)
Power Stage:
	•	1× IRLZ44N MOSFET (atomizer switch)
Power Supply:
	•	18-24V AC or DC input
	•	1× Bridge rectifier (if using AC input)
	•	1× LM2596S buck converter module
	•	Bypass capacitors as needed
Load:
	•	5V USB humidifier atomization module (5V, 300mA, 2W)

##Power Supply Setup
	1.	Connect bridge rectifier:
	◦	AC/DC 18-24V input to bridge rectifier input
	◦	Bridge rectifier (+) output to LM2596S input (+)
	◦	Bridge rectifier (-) output to LM2596S input (-)
	2.	Adjust LM2596S buck converter:
	◦	Connect multimeter to LM2596S output
	◦	Adjust potentiometer on LM2596S until output reads 5.0V DC
	◦	This 5V will power both the 555 circuit and the atomizer
	3.	Establish power rails:
	◦	+5V rail = LM2596S output (+)
	◦	Ground rail = LM2596S output (-)
 
###555 Timer Circuit Build
Pin 1 (Ground):
	•	Connect to ground rail
Pin 2 (Trigger):
	•	Jumper wire to Pin 6
Pin 3 (Output):
	•	Connect through 980Ω resistor to IRLZ44N Gate
Pin 4 (Reset):
	•	Connect to +5V rail (keeps 555 running)
Pin 5 (Control Voltage):
	•	Leave unconnected (or add optional 0.01µF capacitor to ground for noise immunity)
Pin 6 (Threshold):
	•	Connect to positive lead of 10µF capacitor
	•	Jumper wire to Pin 2
	•	Connect to pot End 2
Pin 7 (Discharge):
	•	Connect to 47kΩ resistor (other end to +5V)
	•	Connect to pot End 1
	•	Connect to 1N4148 diode cathode (black band)
Pin 8 (VCC):
	•	Connect to +5V rail

###Timing Components Wiring
47kΩ Resistor:
	•	One end to +5V rail
	•	Other end to Pin 7
100kΩ Potentiometer:
	•	End 1 → Pin 7 (and 47kΩ resistor, and diode cathode)
	•	Wiper → 1N4148 diode anode (no black band end)
	•	End 2 → Pin 6/Pin 2 junction (and capacitor positive)
1N4148 Diode:
	•	Cathode (black band) → Pin 7
	•	Anode → Pot wiper
10µF Electrolytic Capacitor:
	•	Positive (+) lead → Pin 6/Pin 2 junction (and pot End 2)
	•	Negative (-) lead → Ground rail

###MOSFET Power Stage
IRLZ44N Connections 
	(viewing MOSFET from front with part number facing you, pins down):
Left pin = Gate Middle pin = Drain Right pin = Source
Gate (left pin):
	•	980Ω resistor from 555 Pin 3
	•	10kΩ pull-down resistor to ground rail
Drain (middle pin):
	•	Atomizer negative (-) wire (black wire on atomizer module)
Source (right pin):
	•	Ground rail
Atomizer Connection
Atomizer module:
	•	Positive (+) red wire → +5V rail
	•	Negative (-) black wire → IRLZ44N Drain (middle pin)

##Complete Wiring Summary
+5V Rail:
├─ 555 Pin 8 (VCC)
├─ 555 Pin 4 (Reset)
├─ 47kΩ resistor → Pin 7
└─ Atomizer (+) red wire

Ground Rail:
├─ 555 Pin 1 (Ground)
├─ 10µF capacitor (-) negative lead
├─ IRLZ44N Source (right pin)
├─ 10kΩ gate pull-down resistor
└─ LM2596S output (-)

555 Pin 3 (Output):
└─ 980Ω resistor → IRLZ44N Gate

555 Pin 7 (Discharge):
├─ 47kΩ resistor to +5V
├─ Pot End 1
└─ 1N4148 cathode (black band)

555 Pins 2 & 6 (Trigger/Threshold):
├─ Jumper between them
├─ 10µF capacitor (+) positive lead
└─ Pot End 2

Pot Wiper:
└─ 1N4148 anode (no band)

IRLZ44N Gate (left pin):
├─ 980Ω from 555 Pin 3
└─ 10kΩ to ground

IRLZ44N Drain (middle pin):
└─ Atomizer (-) black wire

IRLZ44N Source (right pin):
└─ Ground rail

##Testing and Operation
	1.	Before connecting atomizer, test 555 circuit:
	◦	Power up circuit
	◦	Measure 555 Pin 3 with multimeter - should toggle between ~0V and ~3.6V
	◦	Adjust pot - frequency should change
	2.	Test MOSFET switching:
	◦	Measure IRLZ44N Drain voltage
	◦	Should switch between ~0V and ~5V as 555 oscillates
	◦	Pot adjustment should change pulse width
	3.	Connect atomizer:
	◦	Ensure atomizer disc is in water/liquid
	◦	Power up complete circuit
	◦	You should see mist pulses synchronized with 555 timing
	◦	Adjust pot to change chuff rate and duration
	4.	Final adjustment:
	◦	Set pot to desired chuff rate (typically 2-4 chuffs per second for slow locomotive speed)
	◦	Pulse width determines mist intensity per chuff

##Troubleshooting
No mist output:
	•	Verify 5V at atomizer (+) terminal
	•	Check MOSFET is switching (measure Drain voltage)
	•	Ensure atomizer disc is properly submerged
	•	Verify atomizer module is functional (test directly with 5V)
Continuous mist (not pulsing):
	•	Check 555 is oscillating (measure Pin 3)
	•	Verify MOSFET gate connections
	•	Check 10kΩ pull-down resistor is installed
Irregular pulsing:
	•	Check all 555 timing component connections
	•	Verify pot End 2 is connected to Pin 6/2
	•	Check diode orientation (cathode to Pin 7)

Your steam chuff controller is complete!



A few tips for fine-tuning on the layout:
	•	You might want to mark your pot position for different "locomotive speeds"
	•	Consider the atomizer placement in your loco - you want the mist to vent through the stack realistically
	•	Keep an eye on water reservoir levels during operation
	•	DO NOT LET WATER SIT FOR LONG PERIODS OF TIME

