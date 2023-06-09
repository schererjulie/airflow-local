# Airflow Local: README

# Deploy Airflow Locally

This repo deploys Apache Airflow on your local machine in one simple `make airflow run` command. It’s based on the [Airflow Quick Start](https://airflow.apache.org/docs/apache-airflow/stable/start.html) tutorial and intended for those who want to learn more about how Airflow runs, or if you’re having trouble with the Quick Start and want to use this to try and figure out what’s going wrong (everything’s in the `run-airflow-locally.sh` script)

**Table of Contents**

- [**About the repo**](#about-the-repo)
- [**How to run**](#how-to-run)
- [**Roadmap**](#roadmap)

## About the repo

This repo contains 3 scripts:

1. `run-airflow-locally.sh` ← Use this script to test/run Airflow on your local computer
2. `clean-working-dir.sh` ← Use this script to delete all the .env file and directories created when you ran script #1
3. `release-port-8080.sh` ← If you’re impatient like me and forced Airflow to close, then you can use this script to resolve the “Connection in use” error and release all the pids running on port 8080

## How to run

1. Fork/clone the repo
2. Run the `make airflow run` command

This will:

- create the `/dags`, `/plugins`, and `/logs` folders
- create a `.env` file, add some global variables you’ll need to install Airflow and create a new user, and export those variables in the current shell
- create and activate a virtual environment with Python
- upgrade pip and install Airflow (using the Python interpreter in the venv)
- (finally) run a Airflow instance on your local machine with these commands:

```bash
airflow db init
airflow db upgrade
airflow users create \
  --role $ROLE \
  --username $USER \
  --password $PASSWORD \
  --firstname $FIRST \
  --lastname $LAST \
  --email $EMAIL
airflow webserver --port 8080
airflow scheduler
```

Note: you can also use “all-in-one” `airflow standalone` but I prefer to run each part manually so I understand what’s going on behind the scenes. See the [Airflow Quick Start](https://airflow.apache.org/docs/apache-airflow/stable/start.html) for more info.

Once it's done running, you can access the Airflow UI at [http://localhost:8080](http://localhost:8080). The default username and password are both `admin`.

## **Roadmap**

This is a part of a multi-series project I’m working on where I’m exploring running Airflow in different environments, from testing to dev to production. For more, see [airflow-docker](https://github.com/schererjulie/airflow-docker) and [airflow-kubernetes-eks](https://github.com/schererjulie/airflow-kubernetes-eks).