#FROM apache/airflow:2.6.1
FROM apache/airflow:2.6.2-python3.8
USER root

ENV AIRFLOW_UID=50000
ENV AIRFLOW_GID=50000
ENV AIRFLOW_HOME=/opt/airflow
ENV GOOGLE_APPLICATION_CREDENTIALS=${AIRFLOW_HOME}/config/ServiceKey_GoogleCloud.json

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        unzip \
        wget \
        vim \
        curl \
        python3-pip \
        python3-dev

RUN sudo apt-get install apt-transport-https ca-certificates gnupg 
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list 
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - 
RUN sudo apt-get update && sudo apt-get install google-cloud-cli 

# Create airflow group
RUN groupadd -g ${AIRFLOW_GID} airflow

# Add airflow user to sudoers
RUN usermod -aG sudo airflow

# Change password to airflow
RUN echo "airflow:airflow" | chpasswd 

# Grant sudo permissions to the airflow user
RUN echo "airflow ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Grant permissions to the airflow user
RUN chown -R airflow: ${AIRFLOW_HOME} 

# Create test folder /opt/airflow/tests and airflow.cfg file in /opt/airflow/airflow.cfg
RUN mkdir -p ${AIRFLOW_HOME}/tests
RUN touch ${AIRFLOW_HOME}/airflow.cfg

USER airflow
RUN pip install --upgrade pip

# adds python packages/ Airflow Provider package from providers.txt from PyPI to the image
# adds apache-spark airflow-providers which requires both java and python package from PyPI.
COPY providers.txt /
RUN pip install --no-cache-dir "apache-airflow==${AIRFLOW_VERSION}" -r /providers.txt

# adds python packages Dependencies from dependencies.txt from PyPI to the image
COPY dependencies.txt /
RUN pip install "apache-airflow==${AIRFLOW_VERSION}" -r /dependencies.txt

# Set the default directory where CMD will execute
WORKDIR ${AIRFLOW_HOME}

# Set the default command to execute
# when creating a new container
# i.e. using CherryPy to serve Airflow's UI
CMD ["webserver"]