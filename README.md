# ROS2 workshop
 This is the repository prepared for NTU MAE robotics club ROS workshop

## ROS2 Installation

It is highly recommended to install ROS/ROS2 on Ubuntu 20.04 Instead of Windows. 

## ROS2 Foxy Installation Instructions (For Windows)
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
- Since it takes a lot of space, maybe you can skip this step. If it causes any problems, then can go back and install it (I haven't test it yet, you can tell me if it works without visual studio)
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
Don't worry if you encountered any problems here. 


- RQt dependencies
```
python -m pip install -U pydot PyQt5
```
- To run rqt_graph, you’ll need [Graphviz](https://graphviz.gitlab.io/).
```
choco install graphviz
```

- Install developer tools
```
pip install -U vcstool
```
test it by run ```vcs```
- Install colcon, curl
```
pip install -U colcon-common-extensions
choco install -y curl
```

possible error here: 
```
ERROR: resampy 0.2.2 requires scipy>=0.13, which is not installed.
ERROR: pooch 1.5.2 requires requests, which is not installed.
ERROR: librosa 0.8.1 requires decorator>=3.0.0, which is not installed.
ERROR: librosa 0.8.1 requires joblib>=0.14, which is not installed.
ERROR: librosa 0.8.1 requires scikit-learn!=0.19.0,>=0.14.0, which is not installed.
ERROR: librosa 0.8.1 requires scipy>=1.0.0, which is not installed.
```
Don't worry about it, just proceed to next
- Install dependencies
```
python -m pip install -U setuptools pip

pip install -U catkin_pkg cryptography EmPy ifcfg lark-parser lxml numpy pyparsing pyyaml

pip install -U pytest pytest-mock coverage mock

choco install -y cppcheck

pip install -U flake8 flake8-blind-except flake8-builtins flake8-class-newline flake8-comprehensions flake8-deprecated flake8-docstrings flake8-import-order flake8-quotes mypy==0.761 pep8 pydocstyle
```
- install xmllint
    - Download the 64 bit binary archives of [libxml2](https://www.zlatkovic.com/pub/libxml/64bit/)
    and also iconv and zlib
    - Unpack all archives into e.g. C:\xmllint
    - Add C:\xmllint\bin to the PATH.
    - you may need 7 zip to unpack the package: https://7-zip.en.softonic.com/download?utm_source=SEM&utm_medium=paid&utm_campaign=EN_UK_DSA&gclid=Cj0KCQiA3-yQBhD3ARIsAHuHT66ciu7Y6SZ8tRLwFWgsfQdOmsQzqEeZlqicIbdF4JQYgbs_dhcMLoYaAg0dEALw_wcB

- Install Qt5 (Optional, necessary for __Rviz__, around 6GB)
    - Download (Qt Online Installer for Windows. (select try Qt section)): https://www.qt.io/download
    - Run the installer and install Qt5.
    - set the Qt5_DIR environment variable in the cmd.exe where you intend to build so that CMake can find it:
```
set Qt5_DIR=C:\Qt\5.15.0\msvc2019_64
```

only required if you are building rviz, but it comes with our default set of sources, so if you don’t know, then assume you are building it.


We recommend you install it to the default location of C:\Qt, but if you choose somewhere else, make sure to update the paths below accordingly. When selecting components to install, the only thing you absolutely need for Foxy and later is the appropriate MSVC 64-bit component under the Qt -> Qt 5.15.0 tree. We’re using 5.15.0 as of the writing of this document and that’s what we recommend since that’s all we test on Windows, but later version will probably work too. 


## Get the ROS2 Source code
- First setup a development folder, for example `C:\dev\ros2_foxy`:
```
md \dev\ros2_foxy\src
cd \dev\ros2_foxy
```
- Get the __ros2.repos__ file which defines the repositories to clone from:
```
# CMD
curl -sk https://raw.githubusercontent.com/ros2/ros2/foxy/ros2.repos -o ros2.repos

# PowerShell
curl https://raw.githubusercontent.com/ros2/ros2/foxy/ros2.repos -o ros2.repos
```
Powershell means you are using powershell. Default is using command line (terminal)

- use __vcs__ to import the repositories listed in the ros2.repos file:
```
# CMD
vcs import src < ros2.repos

# PowerShell
vcs import --input ros2.repos src
```

### Build the ROS2 source code on windows
- Open Visual Studio Command Prompt: search __x64 Native Tools Command Prompt for VS 2019__, as Administrator 
- To build the `\dev\ros2_foxy` folder tree:
```
colcon build --merge-install
```

### Environment setup
Start a command shell and source the ROS 2 setup file to set up the workspace:
```
call C:\dev\ros2_foxy\install\local_setup.bat
```
It is normal that the previous command, if nothing else went wrong, outputs “The system cannot find the path specified.” exactly once.

### Test and run
Note that the first time you run any executable you will have to allow access to the network through a Windows Firewall popup
(this is optional)
```
colcon test --merge-install
```
Note: `--merge-install should only be used if it was also used in the build step.`

Then you can get a summary by:
```
colcon test-result
```

### Running some examples for testing
To run the examples, first open a clean new cmd.exe and set up the workspace by sourcing the local_setup.bat file. Then, run a C++ __talker__:
(navigate to your workspace first)
```
call install\local_setup.bat
ros2 run demo_nodes_cpp talker
```

In a separate shell you can do the same, but instead run a Python __listener__:
```
call install\local_setup.bat
ros2 run demo_nodes_py listener
```