## I. Install Docker [It is already installed on the classroom machines!]
Follow the instructions for your operating system to install Docker:
* [Windows](https://docs.docker.com/docker-for-windows/) (For Windows 10 Home Edition, [see here](https://pcda17.github.io/tutorials/Docker_install_Windows))
* [Mac](https://docs.docker.com/docker-for-mac/)

### Troubleshooting installing on Windows 10
Docker has a known bug with the virtual private network code they are using which “randomly” prevents some peoples’ configurations from doing proper DNS lookups in Windows 10 installs when the Docker DNS settings are set to “automatic”. To potentially resolve this issue, some users report that going into the Docker settings under network and selecting DNS Server - fixed: 8.8.8.8 may make it work. In the Windows 10 version of Docker, right-click on Docker in the taskbar and choose settings – in the dialog that appears; “Network” is an option on the left navigation bar and the option appears there.

## II. Download the Docker Image

1. Open a new terminal window (Mac) or command prompt (Windows).

2. Run (or copy and paste) the following command to download the latest version of the Docker image. Be sure to hit 'return'! Be warned: this step takes the longest. Depending on your system, it could take up to 15 minutes. 

```
docker pull hipstas/dv
```

## III. Start Docker

Enter the following commands in the terminal to kill an existing SpokenWeb container (if applicable), then run the Docker container. You will have to hit 'return' twice. [These commands are explained in more detail below.]

```
docker rm -f dv
docker run --name dv -ti -p 8889:8889 --volume ~/Desktop/sharedfolder/:/sharedfolder/ hipstas/dv bash
``` 
