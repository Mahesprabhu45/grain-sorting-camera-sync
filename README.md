# grain-sorting-camera-sync
Design of a synchronized communication system between front and rear camera modules using LVDS for real-time grain sorting and simultaneous ejector control.
📌 Problem Statement

The front and rear cameras in a vision-based grain sorting system must be synchronized to process the same grain line in real time. The system must transfer 63-bit defect detection data from the front camera to the rear camera within 56 microseconds over a distance of 5 meters. Additionally, all 63 ejectors must be triggered simultaneously to ensure accurate removal of defective grains without timing errors.

⚙️ Technology / Approach Used

A high-speed synchronized communication system is designed using LVDS (Low Voltage Differential Signaling) and SPI-based serial data transfer between the front and rear FPGA systems.

Approach Details
Master–Slave Synchronization
Front camera FPGA acts as Master
Rear camera FPGA acts as Slave
A SYNC signal is used to align both cameras at the start of each line
High-Speed Data Transfer
63-bit ejector data is transmitted using SPI protocol
Communication runs at 40 MHz clock
Total transfer time ≈ 1.5 µs, well within 56 µs constraint
Reliable Communication over Distance
LVDS driver (SN65LVDS31) and receiver (SN65LVDS32) are used
Ensures:
Noise immunity
Low signal distortion
Reliable transmission over 5m Cat6 cable
Data Storage and Parallel Output
Received serial data is stored using 74HC595 shift registers
Multiple registers are cascaded to handle 63-bit output
Decision Logic
Front and rear camera outputs are combined using OR logic
Ensures defect detection from either camera triggers ejection
Simultaneous Ejector Control
A FIRE pulse triggers all outputs at once
Eliminates delay caused by serial transmission
Ensures all 63 ejectors fire simultaneously
Timing Control
FPGA generates:
ON pulse (~0.6 ms)
OFF pulse (~0.5 ms)
Ensures proper ejector operation

A real-time FPGA-based camera synchronization system using LVDS communication to achieve high-speed data transfer and simultaneous multi-channel ejector control.
