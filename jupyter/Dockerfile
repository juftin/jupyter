FROM jupyter/all-spark-notebook:latest

MAINTAINER Justin Flannery "juftin@juftin.com"

COPY --chown=${NB_UID}:${NB_GID} requirements.txt /tmp/

RUN \
    conda install --yes --file /tmp/requirements.txt && \
    conda clean --all -f -y && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER && \
    rm /tmp/requirements.txt

RUN \
    jupyter labextension install @jupyterlab/git --no-build && \
    jupyter labextension install @jupyterlab/toc --no-build && \
    jupyter labextension install @jupyterlab/google-drive --no-build && \
    # jupyter labextension install @jupyterlab/dataregistry-extension --no-build && \
    jupyter labextension install @jupyterlab/debugger --no-build && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager jupyter-leaflet --no-build && \
    jupyter lab build -y && \
    jupyter lab clean -y && \
    npm cache clean --force && \
    rm -rf "/home/${NB_USER}/.cache/yarn" && \
    rm -rf "/home/${NB_USER}/.node-gyp" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"