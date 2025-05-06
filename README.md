# digital-twin-parking
Great! Here's a **professional README.md** tailored for your **Parking Digital Twin** project, covering architecture, setup, usage, and screenshots.

---

````markdown
# 🅿️ Parking Digital Twin with FIWARE

This project implements a complete **Digital Twin** for monitoring parking spots using the FIWARE ecosystem. It includes real-time data ingestion, context management, and dashboard visualization.

## 🧠 Context

Urban environments require efficient parking management. This Digital Twin replicates a real-world parking spot virtually, updating its status in real-time and visualizing it through an interactive dashboard.

---

## 🏗️ Architecture

- **Sensor/Simulator**: Sends `status` updates (`occupied` / `free`) to Orion.
- **FIWARE Orion**: Central context broker managing the digital twin state.
- **Draco**: Connects Orion to databases (e.g. MySQL) for historical persistence.
- **MongoDB**: Backing database for Orion.
- **BOLT**: Visualization dashboard for real-time entity monitoring.
- **Flask App**: Receives notifications (via subscription) from Orion.

```mermaid
graph TD;
  Sensor --> Orion;
  Orion --> Flask;
  Orion --> Draco;
  Draco --> MySQL;
  Orion --> BOLT;
````

---

## 🧾 Data Model

Entity: `ParkingSpot`
ID: `urn:ngsi-ld:ParkingSpot:001`
Type: `ParkingSpot`

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

---

## 🐳 Installation (via Docker Compose)

```bash
git clone https://github.com/yourusername/parking-digital-twin.git
cd parking-digital-twin
docker-compose up -d
```

### 📄 `docker-compose.yml` includes:

* `orion`: Context broker
* `mongo`: DB for Orion
* `draco`: Data persistence
* `mysql`: Historical data storage
* `bolt`: Visualization UI
* `flask-app`: Notification listener

---

## 🚀 Running the App

1. Start services:

   ```bash
   docker-compose up -d
   ```

2. Run your Flask app (if not containerized):

   ```bash
   cd parking-twin
   source flask-venv/bin/activate
   python listener.py
   ```

3. Access Orion: [http://localhost:1026/version](http://localhost:1026/version)

4. Access BOLT Dashboard: [http://localhost:3001](http://localhost:3001)

---

## 📡 Subscriptions

Orion is subscribed to your entity changes:

```bash
curl -X POST http://localhost:1026/v2/subscriptions \
-H "Content-Type: application/json" \
-d '{
  "description": "Parking Spot Status Change",
  "subject": {
    "entities": [{"idPattern": ".*", "type": "ParkingSpot"}],
    "condition": { "attrs": ["status"] }
  },
  "notification": {
    "http": { "url": "http://<your-ip>:5000/notify" },
    "attrs": ["status"]
  }
}'
```

> Make sure to replace `<your-ip>` with your actual IP address.

---

## 📊 Visualisation with BOLT

* Login: [http://localhost:3001](http://localhost:3001)
* Default: `admin / admin`
* Add Orion as a data source.
* Create dashboards tracking the `status` attribute of the parking spot.

---

## 📷 Screenshots

> 📌 Add these once your dashboard is running:

* Flask receiving notifications.
* BOLT showing real-time status.
* Subscription list in Orion.

---

## 📚 Tech Stack

* FIWARE Orion Context Broker
* FIWARE Draco
* MongoDB / MySQL
* Flask (Python)
* BOLT (Grafana-based)
* Docker / Docker Compose

---

## 🧑‍💻 Author

**Your Name**
📧 [your.email@example.com](mailto:your.email@example.com)
🔗 [LinkedIn](https://linkedin.com/in/yourprofile)

---

## 📄 License

MIT License

```

---

Would you like me to also generate the `docker-compose.yml` file or create a GitHub repository structure for you?
```
