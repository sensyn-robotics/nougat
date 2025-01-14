FROM pytorch/pytorch:2.5.1-cuda12.4-cudnn9-devel
# replace CUDA version to your CUDA version.
# You can check your CUDA version with below.
# nvcc -V
# then check nvidia cuda container to find your version.
# pip install pytorch fails, so will use pipx, but it still failed. So I use pytroch docker image.
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    apt-get install -y --no-install-recommends curl ca-certificates

ADD https://astral.sh/uv/install.sh /uv-installer.sh
RUN sh /uv-installer.sh && rm /uv-installer.sh
ENV PATH="/root/.local/bin/:$PATH"

RUN mkdir -p /workspace
WORKDIR /workspace
COPY . /workspace

RUN uv init
RUN uv add huggingface-hub==0.17.3 fastapi uvicorn[standard] fsspec[http]==2023.1.0 --no-cache-dir
RUN uv add https://files.pythonhosted.org/packages/f7/29/13965af254e3373bceae8fb9a0e6ea0d0e571171b80d6646932131d6439b/setuptools-69.5.1-py3-none-any.whl

RUN uv run python setup.py install

EXPOSE 8503

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8503"]
# Run this using 'docker run -it -d -p <YOUR PORT>:8503 --gpus all <IMAGE NAME>
