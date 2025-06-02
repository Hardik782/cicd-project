# Flask CI/CD Pipeline with GitHub Actions and AWS EC2

This project demonstrates a simple Flask web application that is automatically deployed to an AWS EC2 instance using GitHub Actions as the CI/CD pipeline.

## Technology Stack

- **Python 3**
- **Flask**
- **GitHub Actions**
- **Gunicorn** (WSGI server)
- **Nginx** (reverse proxy)
- **AWS EC2** (Ubuntu)

## Project Features

- Flask app running a basic HTTP route
- Code linting using flake8
- Automated testing using pytest
- GitHub Actions pipeline that runs on every push to main branch
- SSH-based deployment to AWS EC2
- Gunicorn used to serve the Flask app
- Nginx configured to reverse proxy to Gunicorn

## Project Structure

```
├── app.py                          # Main Flask application
├── test_app.py                     # Unit test for the app
├── requirements.txt                # Python dependencies
├── .github/workflows/python-app.yml # GitHub Actions workflow
└── README.md                       # This file
```

## Instructions to Run Locally

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-name>
   ```

2. Create a Python virtual environment:
   ```bash
   python3 -m venv venv
   ```

3. Activate the environment:
   ```bash
   # On Linux/Mac
   source venv/bin/activate
   
   # On Windows
   venv\Scripts\activate
   ```

4. Install dependencies using pip:
   ```bash
   pip install -r requirements.txt
   ```

5. Run the app:
   ```bash
   python app.py
   ```

## To Run Linter and Tests Locally

- **Check code style:**
  ```bash
  flake8 .
  ```

- **Run tests:**
  ```bash
  pytest
  ```

## CI/CD Behavior

On push to main branch:

1. Run flake8 and pytest
2. If both succeed, connect to EC2 using SSH
3. Pull the latest code from GitHub
4. Install dependencies
5. Restart the Gunicorn server

## EC2 Setup Summary

- Ubuntu EC2 instance with Python, Git, Gunicorn, and Nginx installed
- Flask app cloned from GitHub
- Gunicorn runs on port 8000
- Nginx listens on port 80 and forwards requests to Gunicorn
- EC2 security group allows inbound traffic on ports 22 and 80

## GitHub Repository Secrets Required

Configure the following secrets in your GitHub repository settings:

- **`EC2_HOST`**: Public IP or DNS of your EC2 instance
- **`EC2_USER`**: SSH username, typically "ubuntu"
- **`EC2_KEY`**: Your EC2 private key
- **`EC2_PATH`**: Absolute path on the EC2 instance where the app should be deployed

## Accessing the Deployed App

Open a browser and go to:
```
http://<your-ec2-public-ip>
```

---
