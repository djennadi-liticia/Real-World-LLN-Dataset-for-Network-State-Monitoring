# DATA
# Real-World LLN Dataset for Network State

## Overview

This repository provides real-world datasets collected from an indoor IoT deployment, used to study network-state evolution in Low-power and Lossy Networks (LLNs).

The data include both **link-state** (RSSI) and **node-state** (energy consumption) metrics.

---

## Deployment Description

The datasets were collected from two experimental IoT deployments:

- **Dataset 1**: 5 Zolertia sensor nodes  
- **Dataset 2**: 9 Zolertia sensor nodes  

The reported data correspond to an approximately **two-week period** in indoor office environments.

### Network Characteristics

- **Hardware**: Zolertia RE-Mote Revision B  
- **Operating System**: Contiki-NG  
- **Communication protocol**: Zigbee  
- **Routing protocol**: RPL (default configuration)  
- **Application traffic**: periodic sensing  
- **Payload size**: 5 bytes  
- **Sending period**: every 5 minutes  
- **Monitoring interval**: 1 minute  

---

## Deployment Schematics

The following figures illustrate the physical deployment of the sensor nodes:

- `deployment_dataset1.png`
- `deployment_dataset2.png`

These schematics show node placement and help interpret spatial and environmental effects on RSSI and energy consumption.

---

## Data Collection

Each sensor node generates monitoring logs using a `printf`-based mechanism.

A Raspberry Pi is connected to each node to:

- capture logs,
- store data,
- ensure synchronization.

Each record is generated approximately **every minute** and includes:

- timestamp
- neighboring nodes
- RSSI values
- energy consumption

Energy consumption is computed from the time spent in:

- transmission (TX)
- reception (RX)
- CPU active mode
- low-power mode (LPM)

---

## Data Format

Each dataset is provided as a structured file (e.g., CSV) with the following columns:

| Column               | Description |
|----------------------|-------------|
| `timestamp`          | Time of the measurement (1-minute resolution) |
| `neighbor_id`        | Identifier of the neighboring node |
| `rssi`               | Received Signal Strength Indicator (link quality) |
| `energy_consumption` | Energy consumed during the previous interval (in mJ) |

### Notes

- Each row represents a **node-neighbor interaction at a given timestamp**.
- RSSI values describe **link-state dynamics**.
- Energy consumption describes **node-state evolution**.
