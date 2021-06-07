FROM jupyter/all-spark-notebook:lab-3.0.16

MAINTAINER Justin Flannery "juftin@juftin.com"

COPY --chown=${NB_UID}:${NB_GID} requirements.txt /tmp/

RUN conda install --yes --verbose --file /tmp/requirements.txt

RUN \
    conda clean --all -f -y && \
    fix-permissions ${CONDA_DIR} && \
    fix-permissions /home/${NB_USER} && \
    rm /tmp/requirements.txt

WORKDIR /tmp

RUN conda install -c r r-tidyverse

RUN conda install -c conda-forge nodejs

RUN \
    jupyter contrib nbextension install --user && \
    jupyter nbextensions_configurator enable --user &&\
    jupyter nbextension enable varInspector/main && \
    jupyter nbextension enable autoscroll/main && \
    jupyter nbextension enable code_prettify/code_prettify && \
    jupyter nbextension enable code_prettify/autopep8 && \
    jupyter nbextension enable toc2/main

RUN pip install lckr-jupyterlab-variableinspector sparksql-magic

RUN \
    jupyter labextension install @jupyterlab/git --no-build && \
    jupyter labextension install @jupyterlab/toc --no-build && \
#    jupyter labextension install @jupyterlab/google-drive --no-build && \ # NOT COMPATIBLE WITH JL 3.0
#    jupyter labextension install @jupyterlab/dataregistry-extension --no-build && \ dock# NOT COMPATIBLE WITH JL 3.0
    jupyter labextension install @jupyterlab/debugger --no-build && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager jupyter-leaflet --no-build

RUN jupyter lab build -y && jupyter lab clean -y

RUN \
    npm cache clean --force && \
    rm -rf "/home/${NB_USER}/.cache/yarn" && \
    rm -rf "/home/${NB_USER}/.node-gyp" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

ENV NB_USER="juftin"
ENV JUPYTER_ENABLE_LAB="yes"
ENV RESTARTABLE="yes"
ENV CHOWN_HOME="yes"
ENV GRANT_SUDO="yes"

WORKDIR ${HOME}

CMD ["start.sh", "jupyter", "lab"]

