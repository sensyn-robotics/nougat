FROM pytorch/pytorch:2.5.1-cuda12.4-cudnn9-devel
# replace CUDA version to your CUDA version.
# You can check your CUDA version with below.
# nvcc -V
# then check nvidia cuda container to find your version.
# pip install pytorch fails, so will use pipx, but it still failed. So I use pytroch docker image.
RUN apt-get update && \
    apt-get install -y python3 python3-pip
RUN pip install huggingface-hub fastapi uvicorn[standard] fsspec[http]==2024.9.0

RUN mkdir -p /workspace
WORKDIR /workspace
COPY . /workspace

RUN python3 setup.py install

EXPOSE 8503

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8503"]
# Run this using 'docker run -it -d -p <YOUR PORT>:8503 --gpus all <IMAGE NAME>
