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

Enter the following commands in the terminal to kill an existing SpokenWeb container (if applicable), then run the Docker container. You will have to hit 'return' twice.

```
docker rm -f dv
docker run --name dv -ti -p 8889:8889 --volume ~/Desktop/sharedfolder/:/sharedfolder/ hipstas/dv bash
``` 
### Docker in more detail
All operating systems are different but we want everyone to use the same kind so we will use Docker. Docker is an application that makes it possible to run a virtual copy of the Linux operating system within your primary OS. We will be using Ubuntu, a version of Linux that is often used to run web servers. Ordinarily, you would launch an Ubuntu server and then install the programs you need, one by one; Docker lets us speed up that process by defining our system's initial configuration in a plain text file, known as a Dockerfile. You can view the Dockerfile we are currently using here.

For more details on how Docker works, [see this overview](https://docs.docker.com/engine/docker-overview/).

1. Open a new terminal window (Mac) or command prompt (Windows).
2. Enter the following command in the terminal window to download the Docker image files we'll be using. This could take several minutes.
```docker pull hipstas/dv```
3. When the download is complete, enter the following command to run the container. This will create a new directory called sharedfolder on your desktop.

```docker run --name dv -ti -p 8887:8887 -v ~/Desktop/sharedfolder/:/sharedfolder/ hipstas/dv```

The command above includes several options:
* The `--name` flag sets the name of our container as `spokenweb`. 
* `-ti` tells Docker that we want to use an interactive terminal.
* `-p` maps port 8887 in our container to port 8887 in our local OS.
* The `-v` option defines a "shared volume" between the container and our local machine, a directory called sharedfolder.
* `hipstas/dv` identifies the image we want to download, which is hosted on the Docker Hub website.
