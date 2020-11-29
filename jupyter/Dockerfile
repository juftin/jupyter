FROM jupyter/all-spark-notebook:latest

MAINTAINER Justin Flannery "juftin@juftin.com"

COPY requirements.txt /home/jovyan/requirements.txt

RUN conda install --quiet --yes --file /home/jovyan/requirements.txt && \
    conda clean --all -f -y && \
    rm /home/jovyan/requirements.txt