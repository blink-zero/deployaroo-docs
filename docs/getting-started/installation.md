# Deployaroo Installation Guide

## Prerequisites

- Git
- Python 3.x
- pip (Python package manager)
- Docker (optional, for containerized deployment)

## Installation Steps

### 1. Clone the Repository

```sh
git clone https://github.com/your-repo/deployaroo.git
cd deployaroo
```

### 2. Generate Encryption and Secret Keys

```sh
pip install cryptography
python3 ./generate_encryption_key.py
```

Run the script twice to generate two different keys:
- Use one for `SECRET_KEY`
- Use the other for `ENCRYPTION_KEY`

Remember these keys for the installation method you choose.

## Installation Options

Choose one of the following installation methods:

### A. Docker Run

1. **Build the Docker Image**:
   ```sh
   docker build -t deployaroo .
   ```

2. **Run the Docker Container**:
   ```sh
   docker run -d \
     --name deployaroo-app \
     --restart always \
     -p 8000:8000 \
     -e SECRET_KEY='your_secret_key' \
     -e ENCRYPTION_KEY='your_encryption_key' \
     -e APP_ADMIN_USER='administrator' \
     -e APP_ADMIN_PASSWORD='password' \
     deployaroo \
     gunicorn -w 10 -b :8000 run:app --timeout 3600
   ```

3. **Access the Application**:
   Open your browser and navigate to `http://<IP>:8000`.

### B. Docker Compose

1. **Create or modify docker-compose.yml**:
   ```yaml
   version: '3'
   services:
     app:
       container_name: deployaroo-app
       restart: always
       build: .
       ports:
         - "8000:8000"
       environment:
         SECRET_KEY: 'your_secret_key'
         ENCRYPTION_KEY: 'your_encryption_key'
         APP_ADMIN_USER: 'administrator'
         APP_ADMIN_PASSWORD: 'password'
       volumes:
         - ./deployaroo-data/logs:/home/project/app/logs
         - ./deployaroo-data/backups:/home/project/app/apps/backups
       command: gunicorn -w 10 -b :8000 run:app --timeout 3600

     nginx:
       container_name: deployaroo-nginx
       restart: always
       image: "nginx:latest"
       ports:
         - "80:80"
       volumes:
         - ./nginx:/etc/nginx/conf.d
       depends_on:
         - app
   ```

2. **Deploy**:
   ```sh
   docker-compose up --build -d
   ```

3. **Access the Application**:
   Open your browser and navigate to `http://<IP>:80`.

### C. General Linux

1. **Set Environment Variables**:
   ```sh
   export SECRET_KEY='your_generated_secret_key'
   export ENCRYPTION_KEY='your_generated_encryption_key'
   ```
   
   Alternatively, update these values in `./apps/config.py`:
   ```python
   default_secret_key = 'your_generated_secret_key'
   default_encryption_key = 'your_generated_encryption_key'
   ```

2. **Install Dependencies**:
   ```sh
   pip install -r requirements.txt
   ```

3. **Run the Application**:
   ```sh
   python3 app.py
   ```

4. **Access the Application**:
   Open your browser and navigate to `http://localhost:5000`.

---

## Next Step

To get started with Deployaroo, please refer to the [Initial Setup Guide](../initial-setup).
