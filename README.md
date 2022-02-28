# ROS2 workshop
 This is the repository prepared for NTU MAE robotics club ROS workshop

## ROS2 Foxy Installation Instructions
- For the official installation instructions please go to: https://docs.ros.org/en/foxy/Installation/Windows-Install-Binary.html
- The instructions here are simplified version.


### Installing prerequisites
__Before you start, make sure your windows C drive has enough disk space (20 - 50 GB at least)! A lot of software and dependencies will be installed__

#### Chocolatey (package manager):
- Open your windows powershell, and run with administrator
- Execute the following command: 
```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```
- If you don't see any errors, you are ready to use Chocolatey! Type choco or choco -? now, or see Getting Started for usage instructions.
- Reference: https://chocolatey.org/install
#### Python
- Open command prompt, and execute:
```
choco install -y python --version 3.8.3
```
ROS 2 expects the python installation to be available in directory C:\python38. Double check that it is installed there.
__If it is not, recommend to unisntall python and reinstall in the desired folder.__
- To uninstall python: https://www.educative.io/edpresso/how-to-uninstall-python

#### Install Visual C++ Redistributables
```
choco install -y vcredist2013 vcredist140
```
####  Install OpenSSL
- Download the Win64 OpenSSL v1.1.1L OpenSSL installer from: https://slproweb.com/products/Win32OpenSSL.html
(Scroll to the bottom of the page and download Win64 OpenSSL v1.1.1L. Don’t download the Win32 or Light versions.)
- Run the installer with default parameters, as the following commands assume you used the default installation directory.
- Execute following command in the terminal,  sets an environment variable that persists over sessions
```
setx -m OPENSSL_CONF "C:\Program Files\OpenSSL-Win64\bin\openssl.cfg"
```
- append the OpenSSL-Win64 bin folder to your PATH:

clicking the Windows icon, typing “Environment Variables”, then clicking on “Edit the system environment variables”. In the resulting dialog, click “Environment Variables”, then click “Path” on the bottom pane, finally click “Edit” and add the path below:
```C:\Program Files\OpenSSL-Win64\bin```


### Install Visual Studio (Around 8 GB)
- Download [visual studio 2019 community version](https://visualstudio.microsoft.com/zh-hans/thank-you-downloading-visual-studio/?sku=Community&rel=16&src=myvs&utm_medium=microsoft&utm_source=my.visualstudio.com&utm_campaign=download&utm_content=vs+community+2019#install)
- Make sure that the Visual C++ features are installed.
- Make sure that no C++ CMake tools are installed by unselecting them in the list of components to be installed.
- select the __Desktop development with C++__ workflow during the install.

### Install OpenCV
- download a precompiled version of OpenCV 3.4.6 from
https://github.com/ros2/ros2/releases/download/opencv-archives/opencv-3.4.6-vc16.VS2019.zip
- Assuming you unpacked it to C:\opencv, type the following on a Command Prompt (requires Admin privileges):
```setx -m OpenCV_DIR C:\opencv```
- Add the __PATH variable__ in the environment (same procedure as before): ```C:\opencv\x64\vc16\bin```.

### Install dependencies
- cmake:
```
choco install -y cmake
```
- append the CMake bin folder ```C:\Program Files\CMake\bin``` to your PATH.
- Download packages from: https://github.com/ros2/choco-packages/releases/tag/2020-02-24
which are:
    asio.1.12.1.nupkg

    bullet.2.89.0.nupkg

    cunit.2.1.3.nupkg

    eigen-3.3.4.nupkg

    tinyxml-usestl.2.6.2.nupkg

    tinyxml2.6.0.0.nupkg

    log4cxx.0.10.0.nupkg

Once these packages are downloaded, open an administrative shell and execute the following command:
```
choco install -y -s <PATH\TO\DOWNLOADS> asio cunit eigen tinyxml-usestl tinyxml2 log4cxx bullet
```

-  install some python dependencies for command-line tools:
```
python -m pip install -U catkin_pkg cryptography empy ifcfg lark-parser lxml netifaces numpy opencv-python pyparsing pyyaml setuptools rosdistro
```
- RQt dependencies
```
python -m pip install -U pydot PyQt5
```
- To run rqt_graph, you’ll need [Graphviz](https://graphviz.gitlab.io/).
```
choco install graphviz
```