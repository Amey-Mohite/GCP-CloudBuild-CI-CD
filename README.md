# 🚀 Demo Flask App with BigQuery Integration and Cloud Build CI/CD

This is a minimal Flask application that loads data from a CSV file in a Google Cloud Storage (GCS) bucket into a BigQuery table. The app is containerized using Docker and deployed to Google Cloud Run using Cloud Build with automated testing.

---

## 📁 Repository Structure

* `main.py`: Flask app that triggers a BigQuery load job from GCS.
* `requirements.txt`: Python dependencies.
* `Dockerfile`: Image definition for the Flask app.
* `cloudbuild.yaml`: CI/CD pipeline for building, testing, and deploying the app.
* `test_main.py`: Unit tests for the main endpoint using `pytest` and `unittest.mock`.

---

## 🛠 Features

* Deployable REST API endpoint using Flask
* Reads data from GCS and loads it into BigQuery
* Automatically containerized and deployed via Cloud Build
* Includes unit tests with mocked BigQuery client
* Deployed to Google Cloud Run

---

## 🚚 Data Flow

1. Request to `/` endpoint triggers:
2. CSV file (`us-states.csv`) loaded from GCS bucket `gs://mlop/`
3. Data is written into BigQuery table `mlproject-465617.test_schema.us_states`
4. Response returns the number of rows in the BigQuery table

---

## 🧪 Local Development & Testing

### Install dependencies

```bash
pip install -r requirements.txt
```

### Run tests

```bash
pytest test_main.py
```

### Run locally

```bash
export PORT=5052
python main.py
```

---

## 📦 Build & Deploy with Cloud Build

### Trigger build manually

```bash
gcloud builds submit --region=us-central1 --substitutions=_COMMIT_SHA=dev --config=cloudbuild.yaml
```

### `cloudbuild.yaml` Steps

1. **Build Docker image** from `Dockerfile`
2. **Push image** to Google Container Registry
3. **Run unit tests** inside container
4. **Deploy to Cloud Run** with the built image

---

## 🌐 Cloud Run Endpoint

Once deployed, your app will be accessible at:

```
https://<your-cloud-run-url>/
```

---

## 📊 BigQuery Table Used

* **Project**: `mlproject-465617`
* **Dataset**: `test_schema`
* **Table**: `us_states`

---

## 📝 License

MIT License — free to use, modify, and distribute.
