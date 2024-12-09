FROM python:3.11.7-slim


# Install required packages
WORKDIR /docker-test

RUN apt-get update && \
    apt-get install -y apt-transport-https software-properties-common build-essential curl && \
    apt-get install -y unixodbc-dev && \
    pip install --upgrade pip && \
    apt-get install -y git

# Copy repository files and install dependencies
COPY . .

RUN pip install -r tests/requirements.txt && \
    pip list

# Install pyodbc to publish results to the DB, used by Grafana Dashboards
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list > /etc/apt/sources.list.d/mssql-release.list && \
    apt-get update && \
    ACCEPT_EULA=Y apt-get install -y msodbcsql17 mssql-tools

# Set Environment variables
ENV LANG C.UTF-8
ENV PATH="/opt/mssql-tools/bin:${PATH}"
