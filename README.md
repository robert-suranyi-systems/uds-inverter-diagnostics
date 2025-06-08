# UDS-Based Diagnostic Interface for Electric Drive ECU

## Overview
This project simulates diagnostic communication between a PC-based tester and an embedded controller (Arduino) representing an inverter ECU in an electric drive system.

## Relevance to Automotive
Inverter ECUs in electric vehicles expose diagnostics via the Unified Diagnostic Services (UDS) protocol. This system allows testers to access internal variables, set states, and evaluate functional behavior during system validation or end-of-line tests.

## Purpose
The goal is to create a functional and testable mock system that reflects real-world automotive diagnostic workflows.

## UDS Services Implemented
- `0x10` DiagnosticSessionControl
- `0x27` SecurityAccess
- `0x31` RoutineControl (e.g., fan activation)
- `0x14` ClearDiagnosticInformation
- `0x19` ReadDTCInformation
- `0x85` ControlDTCSettings
- `0x22` ReadDataByIdentifier (e.g., motor temperature, bus voltage)
- `0x2E` WriteDataByIdentifier (e.g., drive mode control)

## Technologies Used
- **Arduino (bare-metal)** for UDS service (Server-ECU) simulation
- **Python** for the PC-based diagnostic (Client-tester) tool
- **CAN bus communication** via transceivers

## Communication
CAN bus (MCP2515 + Arduino MEGA)  
Bitrate: 500kbps  
CAN ID scheme: 0x7E0 (Tester), 0x7E8 (ECU response)

## System Architecture
- [System Architecture Diagram](documents/system_architecture.png)

## Functional Requirements & Test Plan
All functional requirements and test cases are documented in:
- [Requirements](documents/requirements.md)
- [Test Cases](tests/test_case_definition.md)

## Diagrams
- **System Architecture** – Physical layout of tool + ECU
- **Use Case Diagram** – Interaction between tester and system
- **State Machine Diagram** – ECU behavior during session transitions

## Repository Structure
uds-inverter-diagnostics                                              <br />
├── documents/                      # All documentation and diagrams  <br />
│   ├── requirements.md                                               <br />
│   ├── state_machine.png                                             <br />
│   ├── system_architecture.png                                       <br />
│   └── use_case_diagram.png                                          <br />
├── server_arduino_ecu/             # Embedded software (server)      <br />
│   ├── uds_server.ino                                                <br />
│   ├── uds_service_handlers.h                                        <br />
│   └── uds_service_handlers.cpp                                      <br />
│   └── README.md                                                     <br />
├── client_pc/                      # Python PC client (tester)       <br />
│   ├── uds_client.py                                                 <br />
│   └── CAN_interface_config.py                                       <br />
│   └── README.md                                                     <br />
├── tests/                          # Manual integration tests        <br />
│   ├── test_case_definition.xlsx                                     <br />
│   ├── logs/                                                         <br />
└── README.md

## Future Improvements
- Add automated test validation scripts
- Connect physical sensors and actuator to mock inverter logic

## Author
Robert – Mechatronics Engineer | System Test Enthusiast | Automotive & Power Electronics
