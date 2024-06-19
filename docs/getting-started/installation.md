
# Installation

## Clone the Repository

Clone the Deployaroo repository to your machine:

```sh
git clone https://github.com/your-repo/deployaroo.git
cd deployaroo
```

## Generate Encryption and Secret Keys

Install the cryptography library and generate the encryption and secret keys:

```sh
pip install cryptography
sudo chmod +x generate_encryption_key.py
./generate_encryption_key.py
```

Run the script twice and use one key for `SECRET_KEY` and the other for `ENCRYPTION_KEY`.

---

## Installation Options

### Docker Run

1. **Build the Docker Image**:
   ```sh
   docker build -t deployaroo .
   ```

2. **Run the Docker Container**:
   ```
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

---

### Docker Compose

1. **Add Variables to docker-compose.yml**:
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
         SECRET_KEY: 'your_secret_key' # Change this
         ENCRYPTION_KEY: 'your_encryption_key' # Change this
         APP_ADMIN_USER: 'administrator' # Change this
         APP_ADMIN_PASSWORD: 'password' # Change this
       # Volumes are optional
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

---

### General Linux

1. **Install Dependencies**:
   ```sh
   pip install -r requirements.txt
   ```

2. **Configuration**:
   Configure your settings in the `config.yaml` file.

3. **Run the Application**:
   ```sh
   python app.py
   ```

4. **Access the Application**:
   Open your browser and navigate to `http://localhost:5000`.

---

## Next Step

To get started with Deployaroo, please refer to the [Initial Setup Guide](../initial-setup).
