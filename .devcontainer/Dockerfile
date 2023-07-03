FROM mcr.microsoft.com/devcontainers/anaconda:3

# Copy environment.yml (if found) to a temp location so we update the environment. Also
# copy "noop.txt" so the COPY instruction does not fail if no environment.yml exists.
COPY requirements*.txt environment.yml* .devcontainer/noop.txt /tmp/conda-tmp/

RUN if [ -f "/tmp/conda-tmp/environment.yml" ]; then umask 0002 && /opt/conda/bin/conda env update -n base -f /tmp/conda-tmp/environment.yml; fi \
    && if [ -f "/tmp/conda-tmp/requirements.txt" ]; then pip install -r /tmp/conda-tmp/requirements.txt --no-cache-dir; fi \
    && if [ -f "/tmp/conda-tmp/requirements-local.txt" ]; then pip install -r /tmp/conda-tmp/requirements-local.txt --upgrade --no-cache-dir; fi \
    && pip install torch torchvision torchaudio bitsandbytes --no-cache-dir \
    && rm -rf /tmp/conda-tmp \
    && rm -rf /root/.cache/pip

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
