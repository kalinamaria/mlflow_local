FROM python:3.9.14-slim-buster

# Install utils (currently commented out)
# RUN apt-get update && \
#     yes | unminimize && \
#     apt-get -y install \
#         sudo \
#         curl \
#         unzip \
#         wget \
#     apt-get -qq clean && \
#     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
#     mkdir ~/scripts

# Copy over requirements.txt and .env files
COPY ./.env ./requirements.txt /opt/mlflow_tracker/

# Install python libraries from requirements.txt
RUN pip3 install -r /opt/rabbitmq_consumer/requirements.txt

# Create the mlflow_tracker user so we don't run as root
RUN useradd -ms /bin/bash mlflow_tracker

# Change to our working directory
WORKDIR /opt/mlflow_tracker/

# Switch to our rabbitmq_consumer user
USER mlflow_tracker

# TODO: startup command
CMD ["python3", "./test_consume.py"]