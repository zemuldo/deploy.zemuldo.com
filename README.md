# compose.zemuldo.com

Compose setup for deploying my website and its services.

## Setup Environment

export `GCP_PROJECT_ID`=*gcp_project_id*
export `MONGOD_DATA_PATH`=*desired_data_path*

## Start Services

`docker-compose up` starts all services in watch mode.

`docker-compose up -d` starts all services in detached mode.

`docker-compose logs -f -t` streams logs for all services while in detached mode.