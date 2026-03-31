# Real-World LLN Dataset for Temporal Network State Dynamics in IoT

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

## Deployment Details

The datasets were collected from a real-world deployment conducted in the offices of the **L2TI laboratory, Sorbonne Paris Nord University**.

The deployment area covers approximately **558.19 m²**. The floor plan is represented using a uniform grid, where each cell corresponds to a physical area of **1 m × 1 m**. This representation facilitates the interpretation of spatial relationships between nodes and their impact on link quality.

The deployment schematics provided in this repository illustrate the position of each sensor node within the environment. The identifiers shown in these figures correspond directly to the node IDs used in the dataset.

For each node, the collected measurements are stored in a dedicated file following the naming convention:

`logs_node_id_[node_id].csv`

Each file contains all recorded interactions between the corresponding node and its neighbors over time, including RSSI values and energy consumption measurements.

**Note:** In each file, the node ID is implicit from the filename, while `neighbor_id` indicates the interacting neighboring node.

---

## Deployment Schematics

The following figures illustrate the physical deployment of the sensor nodes:

- `deployment_1.png`
- `deployment_2.png`

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

Each dataset is provided as a structured CSV file with the following columns:

| Column               | Description |
|----------------------|-------------|
| `timestamp`          | Time of the measurement (~1-minute resolution) |
| `neighbor_id`        | Identifier of the neighboring node |
| `rssi`               | Received Signal Strength Indicator (link quality) |
| `energy_consumption` | Energy consumed during the previous interval (in mJ) |

### Notes

- Each row represents a **node-neighbor interaction at a given timestamp**.
- RSSI values describe **link-state dynamics**.
- Energy consumption describes **node-state evolution**.
