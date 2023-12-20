
# Onvif Camera Mock

A project to emulate an onvif camera on the network and pass a custom RTSP stream through it.


![Logo](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS6dNR5rxpde3JQVZCfaUiKuewV0QF_7ESA6R8tYiG752kPcO738OnKeOspwsJGOK-8eQ&usqp=CAU)


## Badges

![Shell Script](https://img.shields.io/badge/shell_script-%23121011.svg?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![CMake](https://img.shields.io/badge/CMake-%23008FBA.svg?style=for-the-badge&logo=cmake&logoColor=white)
## Installation

Install git if not already done 

```bash
  sudo apt install git
```
Clone the repository to you local computer
```bash
  sudo git clone https://github.com/IroN404/onvif-camera-mock
```
If not present, install Docker
> On ubuntu 22.04
```bash
  # Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

#Install Docker packages
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Build the container from the root of the cloned repository (./onvif-camera-mock)
```bash
  docker build -t onvif-build -f ./build/Dockerfile.onvif-camera .
```
The build could take from 20 to 30 minutes.

## Deployment

To deploy this project run

```bash
  docker run -it -e INTERFACE=eth0 -p 8554:8554 -p 1000:1000 docker-build
```
If you want to pass a custom mp4 file to the RTSP stream :
```bash
  docker run -it -e INTERFACE=eth0 -e MP4=/home/file.mp4 -p 8554:8554 -p 1000:1000 docker-build
```
> After start you'll need to copy your MP4 file to the container, to do so, note the container id 
>    ```bash
>        docker ps |grep onvif
>    ```
>Then copy 
>    ```bash
>        docker cp <path/to/your/video/file> <container-id>:/home/file.mp4
>    ```
## Usage

You can now see the RTSP stream by using ffmpeg
```bash
apt install ffmpeg
```
The command is 
```bash
ffplay rtsp://localhost:8554/stream1
```
