# Get View
## 1. Docker
* [Install NVIDIA Docker Toolkit](https://docs.omniverse.nvidia.com/isaacsim/latest/installation/install_container.html)
```sh
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list \
  && \
    sudo apt-get update

# Install the NVIDIA Container Toolkit packages
sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker

# Configure the container runtime
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker

# Verify NVIDIA Container Toolkit
docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi
```

* To launch the container:
```sh
./start_container.sh
# It will automatically download the image if you haven't done that before
```

## 2. Isaac Sim
* Execute inside docker terminals
```sh
/isaac-sim/python.sh /home/ubuntu/active_perception/v1/scripts/get_view.py
# and then you will get the output image 
# in /home/ubuntu/active_perception/v1/get_view_output in the docker container
```
