# single-master-serial-controller-with-ack-interrupt


## Overview
This project implements a simplified single-master, single-slave serial communication controller using Verilog-2001.  
The design follows I2C-style timing concepts such as START/STOP conditions and ACK handling, but is intentionally limited to a fixed single-slave, write-only system.

The project focuses on FSM-based RTL design, correct open-drain bus behavior, clock division, ACK/NACK detection, and interrupt generation.

---

## Features
- Single master, single slave architecture
- 8-bit data transmission (MSB first)
- I2C-style START and STOP conditions
- Slave-driven ACK on the 9th clock cycle
- Error detection on missing ACK (NACK)
- Interrupt generation on transaction completion or error
- FSM-based control logic
- Synthesizable Verilog-2001 RTL

---

## Design Description
- The controller operates from a high-frequency system clock.
- A clock divider generates the serial clock (SCL).
- Data on SDA is driven when SCL is low and sampled when SCL is high.
- During the 9th clock cycle, the master releases SDA and the slave pulls it low to indicate ACK.
- If ACK is detected, the transaction completes successfully; otherwise, an error is flagged.
- An interrupt signal is asserted for one clock cycle on transaction completion or error detection.

---

## File Structure
rtl/
└── serial_master.v # Master controller RTL
tb/
└── tb_serial_master.v # Testbench with behavioral slave and ACK model

---

## Simulation and Verification
The design is verified using a Verilog testbench that includes:
- Behavioral single-slave model
- Open-drain SDA bus modeling using pull-up
- ACK generation on the 9th clock
- Monitoring of DONE, ERROR, and INTERRUPT signals



