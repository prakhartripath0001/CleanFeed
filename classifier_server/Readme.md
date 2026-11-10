# Classifier API Server

This Flask app utilizes the Hugging Face Transformers library to classify text into multiple categories. It is intended to be run locally on your machine.

## Prerequisites

Before you can run the app, you need to have the following software installed on your machine:

- Python 3.11 or higher
- pip package manager

## Installation

1. Clone the repository to your local machine:

```bash
git clone https://github.com/nz-m/SocialEcho.git clean-feed
```

2. Navigate to the project directory:

```bash
cd clean-feed/classifier_server
```

3. Install the required Python packages:

```
pip install -r requirements.txt
```

## Usage

To run the app, use the following command:

```
python classifier_api.py
```

This will start the Flask app on `http://localhost:5000`.

**Note:** Before running the app locally, please note that it requires downloading the model files, which have a size of approximately 1.6GB+. These files will be automatically downloaded when you run the app for the first time.

If you prefer to run the app in Docker, build the local image:

```bash
docker build -t clean-feed-classifier .
```

Then run it:

```bash
docker run --rm -p 5000:5000 clean-feed-classifier
```

This will start the app in a Docker container, and you can access it on `http://localhost:5000`.

The app has two endpoints:

- `/`: Returns a simple JSON response to indicate that the app is running.
- `/classify`: Accepts a JSON payload with a `text` field, and returns a JSON response with a list of categories and their scores.

To use the `/classify` endpoint, send a POST request to `http://localhost:5000/classify` with the following JSON payload:

```json
{
  "text" : "Python is a high-level programming language that is widely used for web development, scientific computing, data analysis, artificial intelligence, and more."
}
```

The app will return a JSON response with a list of categories and their scores, sorted by score in descending order:

```json
{
  "response": {
    "categories": [
      {
        "label": "Programming",
        "score": 0.8015680313110352
      },
      {
        "label": "Science and technology",
        "score": 0.05600866675376892
      },
      {
        "label": "Business and entrepreneurship",
        "score": 0.016151048243045807
      },
      ...
    ]
  }
}
```