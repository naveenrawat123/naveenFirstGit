# Physical AI Engineering

This repository contains architecture docs, diagrams, and code for physical AI systems:
- One Robot project (water utilities, pipeline inspection & rehab)
- Edge compute stack (robot probe → truck PC → cloud)
- AI/ML models (YOLO-RGB, YOLO-IR) for segmentation
- Digital Twin + PACP reporting

## Architecture Diagram (Mermaid)
```mermaid
graph TD
 subgraph Robot_Probe
   A1[RGB Camera]
   A2[IR Camera]
   A3[IMU]
   A4[Cable Encoder]
   A5[Motors & Cutter]
   A6[Health Sensors]
 end

 subgraph DK_Aries_Interface
   B1[Power Supply]
   B2[Tether Comms: Ethernet/Serial/CAN]
 end

 subgraph Truck_PC
   C1[Ingestion & Time Sync]
   C2[YOLO-RGB Model]
   C3[YOLO-IR Model]
   C4[Fusion Engine]
   C5[Overlay Generator]
   C6[Operator GUI: AugCut]
   C7[Health & Diagnostics]
   C8[Recording & Upload]
 end

 subgraph Cloud_Portal
   D1[Ingest API]
   D2[Data Lake Storage]
   D3[PACP Coding AI]
   D4[Rehab Rules Engine]
   D5[Digital Twin Builder]
   D6[Customer Reports/Portal]
 end

 A1 & A2 & A3 & A4 & A5 & A6 --> B2
 B2 --> C1
 C1 --> C2 & C3
 C2 & C3 --> C4 --> C5 --> C6
 C1 --> C7
 C1 --> C8 --> D1
 D1 --> D2 --> D3 --> D4 --> D5 --> D6

