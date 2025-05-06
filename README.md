
---

# 🚗 Smart Parking Digital Twin

This project implements a **Digital Twin** of a smart parking system using [FIWARE](https://www.fiware.org/), providing real-time simulation, data monitoring, and visualization capabilities.

---

## 📌 Table of Contents

* [Project Overview](#project-overview)
* [Architecture](#architecture)
* [Technologies Used](#technologies-used)
* [Data Model](#data-model)
* [Setup Instructions](#setup-instructions)
* [Running the Application](#running-the-application)
* [Visualizations](#visualizations)
* [Screenshots](#screenshots)

---

## 📖 Project Overview

This Digital Twin simulates and monitors a smart parking spot, allowing real-time status updates and integrating with context-aware platforms. It demonstrates how virtual representations of physical systems can be managed, tracked, and visualized.

---

## 🏗️ Architecture

The solution consists of the following main components:

* **Orion Context Broker** – Manages context information (parking spot status).
* **Draco (Cygnus)** – Persists context changes into a database (e.g., MySQL).
* **Flask Listener** – Handles notifications via a REST API.
* **MongoDB / MySQL** – Backend storage.
* **Visualization Layer (Planned)** – Web interface or dashboard to visualize parking data.

**Communication is handled using HTTP and NGSI v2 protocol.**

---

## 💡 Technologies Used

* **FIWARE Orion Context Broker**
* **Draco / Cygnus for data persistence**
* **MongoDB / MySQL**
* **Python + Flask (Listener)**
* **Docker / Docker Compose**
* *(Planned)* Visualization with BOLT.New or Grafana

---

## 🧾 Data Model

The core entity is a `ParkingSpot`, represented in NGSI v2 format:

```json
{
  "id": "urn:ngsi-ld:ParkingSpot:001",
  "type": "ParkingSpot",
  "status": {
    "type": "Text",
    "value": "free"
  }
}
```

This model can be extended to include location, timestamp, sensor info, etc.

---

## 🛠️ Setup Instructions

1. **Clone the Repository**

   ```bash
   git clone https://github.com/your-username/smart-parking-digital-twin.git
   cd smart-parking-digital-twin
   ```

2. **Edit IP Placeholders**

   Replace `<YOUR_VM_IP>` in the config or subscription files with your VM's actual IP address.

3. **Start the System**

   Using Docker Compose:

   ```bash
   docker-compose up -d
   ```

---

## 🚀 Running the Application

* **Orion Context Broker**
  Accessible at: `http://<YOUR_VM_IP>:1026`

* **Flask Listener (Notification Receiver)**
  Accessible at: `http://<YOUR_VM_IP>:5000/notify`

* **Subscription Setup**
  Make sure to subscribe using your actual IP:

  ```json
  {
    "notification": {
      "http": {
        "url": "http://<YOUR_VM_IP>:5000/notify"
      }
    }
  }
  ```

* **Entity Update (example)**:

  ```bash
  curl -X PATCH "http://<YOUR_VM_IP>:1026/v2/entities/urn:ngsi-ld:ParkingSpot:001/attrs" \
       -H "Content-Type: application/json" \
       -d '{"status": {"type": "Text", "value": "occupied"}}'
  ```

---

## 📊 Visualizations

This project will soon include a web dashboard using [BOLT.New](https://bolt.new/) or a similar lightweight frontend tool to visualize the status of each parking spot.

---

## 📸 Screenshots

*To be added after frontend integration*

---

## 📃 License

This project is licensed under the MIT License.

---


