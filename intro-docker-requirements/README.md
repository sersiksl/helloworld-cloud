# How do I set-up Docker?
## Install Docker on Mac
Docker for Mac offers a Mac native application that installs in /Applications. It creates symlinks (symbolic links) in /usr/local/bin for docker and docker-compose to the Mac versions of the commands in the application bundle.

The Docker for Mac bundle installs:
* Docker Engine
* Docker CLI Client
* Docker Compose
* Docker Machine

Download and install: [https://docs.docker.com/docker-for-mac/install/](https://docs.docker.com/docker-for-mac/install/)

## Install Docker on Windows 10
Docker for Windows runs on 64-bit Windows 10 Pro, Enterprise, and Education; 1511 November update, Build 10586 or later. Docker plans to support more versions of Windows 10 in the future.

Download and install: [https://docs.docker.com/docker-for-windows/install/](https://docs.docker.com/docker-for-windows/install/)

### Have you previously installed Docker Toolbox, Docker Machine, or VirtualBox? (if not, just ignore this section)
Docker for Windows now requires Microsoft’s Hyper-V. Once enabled, VirtualBox will no longer be able to run virtual machines (your VM images will still remain). You can still use docker-machine to manage remote hosts.

You have the option to import the default VM after installing Docker for Windows from the Settings menu in the System Tray.

Docker for Windows enables Hyper-V if necessary; this requires a reboot.