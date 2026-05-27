# Riot Games Leaderboard App

A containerized web application that provides real-time competitive leaderboards for popular Riot Games titles. Built with **Flask** and deployed via **Google Cloud Run**, this project demonstrates seamless integration with the **Riot Games API** and robust cloud deployment workflows.

## 🚀 Key Features

- **Live Data Integration**: Fetches real-time competitive data directly from the Riot Games API.
- **Multi-Game Support**:
  - **Valorant**: Displays the top 100 players with rank, gamertag, rank rating (RR), and total wins.
  - **League of Legends**: Shows Challenger-tier players with rank, summoner name, league points (LP), and wins.
- **Cloud-Native Architecture**: Fully containerized using Docker and optimized for serverless deployment on Google Cloud Run.
- **Responsive Web Interface**: Built with Bootstrap for a clean, accessible viewing experience across devices.

## 🛠️ Tech Stack

- **Backend**: Python, Flask
- **API**: Riot Games API (Requests)
- **Containerization**: Docker
- **Cloud Platform**: Google Cloud Platform (Cloud Build, Cloud Run, Artifact Registry)
- **Frontend**: Bootstrap 5, Jinja2 Templates
- **Testing**: Pytest

## 🏗️ Architecture Overview

The application follows a modern serverless pattern:
1.  **Flask** handles routing and API orchestration.
2.  **Docker** packages the application and its dependencies into a portable image.
3.  **Google Cloud Build** automates the image construction.
4.  **Google Cloud Run** provides a scalable, serverless environment to host the container.

## 📋 Prerequisites

- Python 3.9+
- Docker (optional for local development)
- A [Riot Games Developer Account](https://developer.riotgames.com/) and API Key.
- A Google Cloud Platform account with a project enabled.

## ⚙️ Local Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/daniel1wnl/riotLeaderboards-cloudRun.git
   cd riotLeaderboards-cloudRun
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set environment variables:**
   ```bash
   export API_KEY=your_riot_api_key
   export ACT_ID=your_valorant_act_id
   ```

5. **Run the app:**
   ```bash
   python3 app.py
   ```

## ☁️ Deployment to Google Cloud Run

### 1. Build the Container Image
Using Google Cloud Build to create and store your image in the Container Registry:
```bash
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/riot-leaderboard --timeout=900
```

### 2. Deploy to Cloud Run
Deploy the image to a serverless service, injecting the required API credentials as environment variables:
```bash
gcloud run deploy riot-leaderboard \
  --image gcr.io/${GOOGLE_CLOUD_PROJECT}/riot-leaderboard \
  --service-account [YOUR_SERVICE_ACCOUNT_NAME]@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com \
  --set-env-vars API_KEY=[YOUR_API_KEY],ACT_ID=[VALORANT_ACT_ID] \
  --allow-unauthenticated
```

*Note: You can find the current Valorant Act ID via the [Riot API status endpoint](https://na.api.riotgames.com/val/status/v1/platform-data).*

## 🧪 Testing

The project uses `pytest` for endpoint validation. To run the tests:
```bash
pytest
```

## 📸 Previews

### Valorant Leaderboard
![Valorant App Preview](imgs/appVal.png)

### League of Legends Leaderboard
![League App Preview](imgs/appLoL.png)

## 👤 Author

**Daniel Gregorio-Torres**
- [GitHub](https://github.com/daniel1wnl)
- [LinkedIn](https://www.linkedin.com/in/danielgregoriotorres/)
