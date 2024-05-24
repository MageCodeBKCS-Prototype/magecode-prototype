# MAGECODE PROTOTYPE

## Installation & Running

### Requirements

- Docker & Docker Compose
- Git
- wget

### Setup

1. Clone this repo & its submodule:

```
git clone https://github.com/MageCodeBKCS-Prototype/magecode-prototype.git
cd magecode-prototype
git submodule init
git submodule update --recursive
```

2. Create necessary directories

```
mkdir models upzip_uploaded_code
```

3. Download AI models for machine-generated detection & vulnerabilities detection tasks:
- codebert_cpp.pth
- codebert_py.pth
- codebert_java.pth
- vulnerability_model_4.pth

```
cd models

wget https://github.com/MageCodeBKCS-Prototype/magecode-prototype/releases/download/v0.0.1/codebert_cpp.pth

wget https://github.com/MageCodeBKCS-Prototype/magecode-prototype/releases/download/v0.0.1/codebert_py.pth

wget https://github.com/MageCodeBKCS-Prototype/magecode-prototype/releases/download/v0.0.1/codebert_java.pth

wget https://github.com/MageCodeBKCS-Prototype/magecode-prototype/releases/download/v0.0.1/vulnerability_model_4.pth
```

4. Install codeql

```
cd ..

wget https://github.com/MageCodeBKCS-Prototype/magecode-prototype/releases/download/v0.0.1/codeql.zip

unzip codeql.zip
```

5. Install docker image of Dolos

```
docker pull ghcr.io/dodona-edu/dolos
```

6. Setup environment variables

- For Rails API:

```
cd Api
cp .env.example .env
cp .env.development.example .env.development
cd ..
```

- For Code Processing Service:

```
cd Code-Processing-Service
cp .env.example .env
```
Change following variables if you want:
- RAILS_API_EMAIL
- RAILS_API_PASSWORD
- LANGUAGES
- MODEL_NAMES
- MODEL_PATHS
- DEVICE

You can add/remove supported language and models in **LANGUAGES**, **MODEL_NAMES** and **MODEL_PATHS**.

If your machine has GPUs, change the value of **DEVICE** to **cuda**.

After these steps, repository structure should be as follow:

    ├── Api                       # Rails API
    ├── Code-Processing-Service   # Machine-generated detection & Vulnerabilities detection service
    ├── codeql                    # codeql source files
    ├── models                    # Directory used to store AI models
    ├── upzip_uploaded_code       # Directory used to store unzipped code uploaded by users
    ├── Web-UI                    # Frontend
    ├── .gitignore
    ├── .gitmodules
    ├── docker-compose.yml
    └── README.md

### Running

1. From the root of repository (*magecode-prototype*), running all services as docker containers:
   
```
docker compose up --build
```

This step would take several minutes depending on your machine's strength and network connection.

2. After all containers are up, wait a few minutes for all models to be loaded. Then, access UI by URL: *http://localhost:8080/#/*

3. (***Important***) Create account with EMAIL & PASSWORD exactly the same as variable RAILS_API_EMAIL & RAILS_API_PASSWORD in the .env file of Code-Processing-Service.

4. Log in with the newly created account and start exploring.