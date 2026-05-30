# SatSnatcher
An automated satellite tracker that mechanically rotates a Yagi antenna array using live orbital data to lock onto LEO satellites. I need a VHF/UHF transceiver to establish two-way radio contact, allowing me to decode telemetry downlinks and transmit commands during active passes.

How it works:
Starting from orbital data, it pinpoints each LEO satellite's location overhead. Then, movement follows - guided by real-time math, the antenna turns precisely to meet its target. Instead of manual control, algorithms handle timing and direction together. As one passes through view, tracking shifts smoothly without pause.
Satellite Position Found
A signal from space, captured by a ground-based machine, feeds into code designed to follow movement. Instead of guessing where things might be, it relies on standardized numeric records called Two-Line Elements. With these figures in hand, the system works out exactly where the object sits above Earth right now. Location shifts moment by moment - this process keeps pace using math tied to the viewer's own spot on the planet.
This location gets transformed by the program into:
Azimuth angle (horizontal direction)
Elevation angle (vertical direction)
Direction depends on these figures. Where the signal comes from hinges upon such settings. Pointing accuracy relies heavily on what numbers are used. The alignment follows directly from chosen parameters. Target position ties closely to each value entered.
Coordinate Transmission
A signal carrying azimuth and elevation data moves from the tracking software to the Raspberry Pi Pico via a USB serial link. The transfer happens continuously, using standard communication protocols built into the interface. Information flows in one direction only, ensuring minimal processing delay on the receiving end. Each value arrives formatted as plain text, ready for immediate use by the microcontroller. Timing aligns closely with sensor updates, maintaining coordination across components.
Example transmitted data:
AZ = 120°
EL = 45°
As the satellite travels overhead, the Pico keeps getting fresh position data. Though movement continues, updates arrive without pause. Even during shifts in trajectory, location signals flow steadily. While paths change, tracking information follows close behind. Despite motion through space, coordinate delivery remains constant.
Microcontroller Processes Data
A signal arrives at the Raspberry Pi Pico carrying position details. From that point onward, it calculates required joint rotations. These values then become timing pulses through modulation techniques. Pulse Width Modulation shapes each output accordingly. The system delivers adjusted electrical cycles instead of raw numbers.
Control of two servos relies on these PWM signals. Movement adjusts based on signal timing. Each servo responds individually. Signals determine position accuracy. Timing precision affects performance directly
Azimuth Servo → controls horizontal rotation
Elevation Servo → controls vertical movement
If needed, limit switches may halt motion when mechanical boundaries are reached.
Antenna moves physically
Rotating the antenna mount, servo motors adjust the Yagi's alignment based on where the satellite is expected to be.
Throughout the satellite pass, the antenna adjusts its direction without pause.
RADIO RECEPTION AND COMMUNICATION
With alignment set, the Yagi antenna boosts signal strength while sharpening its directional focus on the linked VHF or UHF transceiver.
Signals reach orbiting satellites more effectively when they pass overhead. Reception quality increases because alignment supports clearer transmission paths.
System Workflow
Satellite Orbit Data
↓
Tracking Software Figures Out Location
↓
Azimuth Elevation Coordinates Calculated
↓
Coordinates sent over usb serial
↓
Raspberry Pi Pico Gets New Information
↓
PWM Signals Generated
↓
Servos Rotate Antenna
↓
Yagi Antenna Follows Satellite
↓
VHF UHF Transceiver Picks Up Signal
Splitting computation from hardware management makes the setup easier to maintain. Modularity comes naturally when these parts operate independently. Future improvements fit without disrupting existing components. Debugging simplifies since issues stay contained within one area. Expansion becomes straightforward under this structure.
