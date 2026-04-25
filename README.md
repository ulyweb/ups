# ⚡ Network Power Infrastructure

![Status](https://img.shields.io/badge/Status-Operational-success?style=for-the-badge&logo=statuspage)
![UPS](https://img.shields.io/badge/UPS-APC_BE600M1-blue?style=for-the-badge&logo=apc)
![Runtime](https://img.shields.io/badge/Est._Runtime-42m-orange?style=for-the-badge&logo=time)

> **Live Dashboard:** [https://yourusername.github.io/repo-name](https://yourusername.github.io/repo-name)

This repository hosts the configuration and monitoring interface for the primary home lab power backup system. The system is managed via **pfSense (NUT)** with an APC Back-UPS BE600M1.

---

## 🔌 Topology Map

```mermaid
graph LR
    %% Nodes
    Grid((("⚡ Utility Grid")))
    UPS[/"🔋 APC BE600M1"\]
    
    subgraph "Rack Unit 1"
        FW["🛡️ VNOPN pfSense<br/>(Master Node)"]
        Modem["🌐 Arris SB8200"]
    end
    
    subgraph "Rack Unit 2"
        Switch["🖧 Cisco 2960-X"]
    end

    %% Connections
    Grid ==>|120V AC| UPS
    UPS ==>|Battery Backup| FW
    UPS ==>|Battery Backup| Modem
    UPS ==>|Battery Backup| Switch
    
    %% Data Link
    UPS -.->|USB Data| FW

    %% Styling
    classDef power fill:#fde047,stroke:#eab308,stroke-width:2px,color:black;
    classDef bat fill:#22c55e,stroke:#166534,stroke-width:2px,color:white;
    classDef device fill:#3b82f6,stroke:#1d4ed8,color:white;
    
    class Grid power;
    class UPS bat;
    class FW,Modem,Switch device;
