<p align="center">
  <img src="https://github.com/flybrainlab/flybrainlab/raw/master/flylablogo.png" width="50%">
</p>

<p align="center">
  <a href="https://twitter.com/flybrainobs">
        <img src="https://img.shields.io/twitter/follow/flybrainobs.svg?style=social&label=Follow"
             alt="Twitter Follow">
    </a>
    <a href="https://github.com/FlyBrainLab/FlyBrainLab">
        <img src="https://img.shields.io/github/license/FlyBrainLab/FlyBrainLab.svg"
             alt="GitHub license">
    </a>
    <a href="https://github.com/FlyBrainLab/FlyBrainLab">
        <img src="https://img.shields.io/github/last-commit/FlyBrainLab/FlyBrainLab.svg"
             alt="GitHub last commit">
    </a>
</p>
<p align="center">
  <a href="https://github.com/FlyBrainLab/FlyBrainLab/wiki">Wiki</a> | <a href="https://github.com/FlyBrainLab/FlyBrainLab/wiki/Troubleshooting">Troubleshooting</a>
</p>

FlyBrainLab is an interactive computing platform for studying the function of executable circuits constructed from fruit fly brain data. FlyBrainLab is designed with three main capabilities in mind: (i) 3D exploration and visualization of fruit fly brain data, (ii) creation of executable circuits directly from the explored and visualized fly brain data, and (iii) interactive exploration of the functional logic of the devised executable circuits.

FlyBrainLab provides an environment where computational researchers can present configurable, executable neural circuits, and experimental scientists can interactively explore circuit structure and function ultimately leading to biological validation.

More details about FlyBrainLab can be found in the following publication:
- Aurel A. Lazar, Tingkai Liu, Mehmet K. Turkcan, and Yiyin Zhou, [FlyBrainLab: Accelerating the Discovery of the Functional Logic of the Fruit Fly Brain in the Connectomic/Synaptomic Era](https://doi.org/10.1101/2020.06.23.168161), bioRxiv, June 2020.

This repository serves as the entry point for FlyBrainLab, where documentation and installation scripts can be found.

### Content
1. [Installation](#1-installation)
  - 1.1 [Installing Only User-side Components](#11-installing-only-user-side-components)
  - 1.2 [Full Installation](#12-full-installation)
  - 1.3 [Docker Image](#13-docker-image)
  - 1.4 [Amazon Machine Image](#14-amazon-machine-image)
2. [Basic Usage](#2-basic-usage)
  - 2.1 [Launching FlyBrainLab](#21-launching-flybrainlab)
  - 2.2 [FlyBrainLab User Interface](#22-flybrainlab-user-interface)
  - 2.3 [Configuring Backend Servers](#23-configuring-backend-servers)
  - 2.4 [Getting Started Tutorials](#24-getting-started-tutorials)
3. [Troubleshooting](#3-troubleshooting)

## 1. Installation

FlyBrainLab consists of backend components and user-side components. There are a few options for installation.
1. [**Installing only User-side Components**](#11-installing-only-user-side-components): provides instructions for installing a copy of all FlyBrainLab user-side components that, by default, connect to backend servers hosted by the Fruit Fly Brain Observatory Team. If you only need to visualize and explore the biological data, this will be the fastest way to install. However, the public backend servers do not provide capabilities for executing neural circuits on GPUs using [Neurokernel](https://neurokernel.github.io). It may also be helpful to visit [BrainMapsViz](http://www.fruitflybrain.org/#/brainmapsviz) where you can directly interact with the NeuroNLP web application without any installation.
1. [**Full Installation**](#12-full-installation): provides instructions for installing both the user-side and backend components on the same machine. By default, FlyBrainLab will connect to the backend servers locally hosted.
1. [**Docker Image**](#13-docker-image): We maintain [this Docker image] with a full FlyBrainLab installation. If you are set up with Docker with GPU support, this will be the easiest way to try FlyBrainLab that runs locally.
1. [**Amazon Machine Image**](#14-amazon-machine-image): We also maintain AMI [`ami-039ef13d01c0e8e2f`](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#LaunchInstanceWizard:ami=ami-039ef13d01c0e8e2f) that has the FlyBrainLab fully installed. It is helpful in case you do not have a machine with NVIDIA GPU handy, but still want to try out the full installation.


### 1.1 Installing Only User-side Components

#### System Requirement

- Supported OS (64-bit): Linux, Windows and macOS.
- Minimum 2GB disk space.
- [conda](https://docs.conda.io/en/latest/): See its [Installation Instructions](https://docs.conda.io/projects/conda/en/latest/user-guide/install/).

Additional requirement for macOS:
- Xcode Command Line Tools: use the following command to install:
```zsh
xcode-select --install
```
If you encounter error:
```
Can’t install the software because it is not currently available from the Software Update server.
```
you can download the installer directly at https://developer.apple.com/download/more/ (Apple ID Login required), and select the latest stable version. If you encounter further error, you can try installing Xcode and then the Command Line Tools again.

#### Installing the Latest Release Version

Download the installation script for your OS to an empty folder where you want your FlyBrainLab installation to reside,
- Linux: [`fbl_installer_linux.sh`](https://raw.githubusercontent.com/FlyBrainLab/FlyBrainLab/master/fbl_installer_ubuntu.sh)
- Windows: [`fbl_installer.cmd`](https://raw.githubusercontent.com/FlyBrainLab/FlyBrainLab/master/fbl_installer_mac.sh)
- macOS: [`fbl_installer_mac.sh`](https://raw.githubusercontent.com/FlyBrainLab/FlyBrainLab/master/fbl_installer.cmd)

In terminal or command line, go to the folder and execute the following commands line by line (you can change `flybrainlab` to a different name of your choice for the environment name):

##### Linux:
```bash
conda create -n flybrainlab python=3.7 -c conda-forge -y
conda activate flybrainlab
sh fbl_installer_linux.sh
```

##### Windows:
```bash
conda create -n flybrainlab python=3.7 -c conda-forge -y
activate flybrainlab
fbl_installer.cmd
```

##### macOS:
```bash
conda create -n flybrainlab python=3.7 -c conda-forge -y
conda activate flybrainlab
sh fbl_installer_mac.sh
```

After the script finishes, go to [Launching FlyBrainLab from User-side Only Installation](#launching-flybrainlab-from-user-side-only-installation).

#### Build from Source Step-by-step
If you want to use the latest development code instead of the release, you can build FlyBrainLab using the following command line code:
```bash
# create anaconda environment called flybrainlab with appropriate packages installed
conda create -n flybrainlab python=3.7 nodejs scipy pandas cookiecutter git yarn -c conda-forge -y
# activate the flybrainlab environment just created
# if you have conda<4.4, you may need to use `source activate flybrainlab` instead
conda activate flybrainlab
# Install additional package into the environment
pip install jupyter jupyterlab>=2.2.8
pip install txaio twisted autobahn crochet service_identity autobahn-sync matplotlib h5py seaborn fastcluster networkx msgpack msgpack-numpy
# If on Windows, execute the following:
pip install pypiwin32

# Create a preferred installation directory and go into that directory, For example:
# mkdir ~/MyFBL
# cd ~/MyFBL

# Clone packages into your preferred directory (~/MyFBL) in the example above
git clone https://github.com/FlyBrainLab/Neuroballad.git
git clone https://github.com/FlyBrainLab/FBLClient.git
git clone https://github.com/FlyBrainLab/NeuroMynerva.git

# Install all relevant packages
cd ./Neuroballad
python setup.py develop
cd ../FBLClient
python setup.py develop
cd ../NeuroMynerva
jlpm
jlpm run build

# Execute this if you are a user
jupyter labextension install .
jupyter lab build
jupyter lab

# Execute this if you are a developer
jupyter labextension link .
jupyter lab --watch
```
You may be prompted. On Windows, you will only need to write "activate neuromynerva" instead of "source activate neuromynerva".

After the script finishes, go to [Launching FlyBrainLab from User-side Only Installation](#launching-flybrainlab-from-user-side-only-installation).

### 1.2 Full Installation

#### System Requirement

- Supported OS (64-bit): Ubuntu 16.04 or later.
- CUDA enabled GPU and [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit).
- Minimum 30GB disk space, preferrably on SSD (including 3 default databases).
- The following ubuntu packages:
`wget default-jre curl build-essential tar apt-transport-https tmux`.
- [conda](https://docs.conda.io/en/latest/): See its [Installation Instructions](https://docs.conda.io/projects/conda/en/latest/user-guide/install/).

#### Installing from Script

Download the installation script [`fbl_full_installation_ubuntu.sh`](https://raw.githubusercontent.com/FlyBrainLab/FlyBrainLab/master/fbl_full_installation_ubuntu.sh).

Uncomment the following code in the script if you have not installed all required Ubuntu packages (requires sudo privilege):
```bash
#echo "Installing prerequisites"
#sudo apt update
#sudo apt install -y wget default-jre curl build-essential tar apt-transport-https tmux
```

Then edit the following lines:
```bash
# existing directories
CUDA_ROOT=/usr/local/cuda # root directory where you installed cuda

# To be installed
FFBO_ENV=ffbo # conda environment for main fbl
NLP_ENV=ffbo_legacy # additional conda environment for NLP
FFBO_DIR=$HOME/ffbo # directory to store local repositories
ORIENTDB_ROOT=$HOME/orientdb # root directory where you want to install OrientDB
FFBO_PORT=8081 # main port number of the FFBO processor, make sure to use an uncommon port that will not be used by other program.
```

Then run the script in `bash`:
```bash
bash fbl_full_installation_ubuntu.sh
```

If installation fails, and you want to reinstall, please remove the previous (perhaps partial) installation.

To cleanly remove the FlyBrainLab full installation:
```bash
rm -rf $FFBO_DIR
rm -rf $ORIENTDB_ROOT
rm -rf ~/.ffbo
conda env remove -n $FFBO_ENV
conda env remove -n $NLP_ENV
```
where the environment variables should match the ones during installation.

If installation complete without error, please go to
[Launching FlyBrainLab from Full Installation](#launching-flybrainlab-from-full-installation).


### 1.3 Docker Image

#### System Requirement

- Supported OS: Linux, Windows (via Windows Subsystem for Linux 2 using [Microsoft Windows Insider Program](https://insider.windows.com/en-us/getting-started#install) Build version 20145 or higher).
- CUDA enabled GPU (NVIDIA driver must be installed. For WSL2, get NVIDIA driver [here](https://developer.nvidia.com/cuda/wsl). See also [here](https://docs.nvidia.com/cuda/wsl-user-guide/index.html) for enabling CUDA on WSL2).
- [Docker CE](https://docs.docker.com/engine/install/ubuntu/) 19.03 or higher.
- [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-docker).
- Minimum 30GB disk space, preferrably on SSD (including 3 default databases).

#### Pull Docker Image

Pull the [FlyBrainLab Docker Image](https://hub.docker.com/r/fruitflybrain/fbl):
```
docker pull fruitflybrain/fbl:latest
```

Download NeuroArch Databases to a folder, for example, `~/databases`.
You can use the [`download_datasets.sh`](raw.githubusercontent.com/FlyBrainLab/run_scripts/main/flybrainlab/download_datasets.sh) script,
or follow the steps below.

- FlyCircuit and Janelia Medulla 7 column datasets

https://drive.google.com/file/d/1Nbo0C55X52OeYJtYVzB-52mo7I7H4UCc/view?usp=sharing (~350 MB, decompress to 2GB)

You can also download the data directly using `wget` (in Linux):

```
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1Nbo0C55X52OeYJtYVzB-52mo7I7H4UCc' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1Nbo0C55X52OeYJtYVzB-52mo7I7H4UCc" -O flycircuit.tar.gz && rm -rf /tmp/cookies.txt
```

- Hemibrain dataset:

https://drive.google.com/file/d/1puvabvKGFBchKiD56cjlu3MFNQ-Soam1/view?usp=sharing (~3GB, decompress to ~18GB)

You can also download the data directly using `wget` (in Linux):

```
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1puvabvKGFBchKiD56cjlu3MFNQ-Soam1' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1puvabvKGFBchKiD56cjlu3MFNQ-Soam1" -O hemibrain.tar.gz && rm -rf /tmp/cookies.txt
```

- Larva L1EM CNS dataset:

https://drive.google.com/file/d/1U4TfYXzhN7siQtwupDDmgW7sOBRXmQrL/view?usp=sharing (~40MB, decompress to ~400MB)

You can also download the data directly using `wget` (in Linux):

```
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1U4TfYXzhN7siQtwupDDmgW7sOBRXmQrL' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1U4TfYXzhN7siQtwupDDmgW7sOBRXmQrL" -O l1em.tar.gz && rm -rf /tmp/cookies.txt
```

Decompress the downloaded datasets.

For usage, see [Launching FlyBrainLab from FlyBrainLab Docker Image](#launching-flybrainlab-from-flybrainlab-docker-image).


### 1.4 Amazon Machine image

We provide an Amazon Machine Image (AMI) that has the FlyBrainLab Docker Image built in and meets all its requirements. The AMI ID is `ami-039ef13d01c0e8e2f` in `us-east-1` region. It must be launched using a GPU instance (a Tesla GPU is recommended).
You can launch a GPU instance directly using the following link:

https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#LaunchInstanceWizard:ami=ami-039ef13d01c0e8e2f

Once an instance is launched, first update the docker image by
```bash
docker pull fruitflybrain/fbl:Latest
```

Then it can be used the same way as the Docker Image installation.
For usage, see [Launching FlyBrainLab from FlyBrainLab Docker Image](#launching-flybrainlab-from-flybrainlab-docker-image).
Note that all default databases are stored in `~/databases`.

## 2. Basic Usage

### 2.1 Launching FlyBrainLab

#### Launching FlyBrainLab from User-side Only Installation

```bash
conda activate FlyBrainLab
jupyter lab
```

Default port is 8888. Go to browser with url: `localhost:8888`, and refer to [FlyBrainLab User Interface](#22-flybrainlab-user-interface).

#### Launching FlyBrainLab from Full Installation

```bash
$FFBO_DIR/bin/start.sh
````
where `$FFBO_DIR` is the directory you configured to install FlyBrainLab in.

Default port is 8888. Go to browser with url: `localhost:8888`, and refer to [FlyBrainLab User Interface](#22-flybrainlab-user-interface).

#### Launching FlyBrainLab from FlyBrainLab Docker Image

Assuming all GPUs will be available to the docker container,
```bash
docker run --name fbl --gpus all -p 9999:8888 -v $database/hemibrain:/opt/orientdb/databases/hemibrain -v $database/flycircuit:/opt/orientdb/databases/flycircuit -v $database/l1em:/opt/orientdb/databases/l1em -it fruitflybrain/fbl:latest
```

Go to browser with url: `localhost:9999`. Note that the default jupyter notebook port in the Docker container is `8888` and is mapped to `9999` on host machine. Then refer to [FlyBrainLab User Interface](#22-flybrainlab-user-interface).

For advanced usage of the Docker image, please refer to the [FlyBrainLab Docker Image Page](https://hub.docker.com/r/fruitflybrain/fbl).

### 2.2 FlyBrainLab User Interface

Once FlyBrainLab is launched, you will find in the browser a typical JupyterLab interface, with an additional selection of FlyBrainLab buttons, as shown here:

<p align="center">
  <img src="https://github.com/FlyBrainLab/Tutorials/raw/master/tutorials/osn_ephys_tutorial/images/osn_1.png" width="80%">
</p>

Click on the `Create FBL Workspace` button and choose a dataset to work with. By default, you will find the [Hemibrain](https://www.janelia.org/project-team/flyem/hemibrain), the [FlyCircuit](http://flycircuit.tw) and the [L1EM Larva](https://l1em.catmaid.virtualflybrain.org/) datasets.

This will open the main FlyBrainLab user interface, as shown in the following figure (positions of the windows can be arbitrarily rearranged):

<p align="center">
  <img src="http://www.bionet.ee.columbia.edu/images/FBL_ui.jpg" width="80%">
</p>

If you encounter a popup window showing error, you may need to check if the configuration of servers is correct. See [Configuring Backend Servers](#23-configuring-backend-servers).

In order for a opened notebook to interact with the NeuroNLP and NeuroGFX windows, please select the kernel correspoding to the kernal used by the NeuroNLP window (e.g. `Untitled.ipynb` in the following figure).

<p align="center">
  <img src="https://github.com/FlyBrainLab/Tutorials/raw/master/tutorials/osn_ephys_tutorial/images/osn_2.png" width="80%">
</p>


### 2.3 Configuring Backend Servers

Please read https://github.com/FlyBrainLab/FlyBrainLab/wiki/Installation for instructions on adding/changing servers.

### 2.4 Getting Started Tutorials

Several tutorials are available in the form of notebooks.
They are available in the [Tutorials](https://github.com/FlyBrainLab/Tutorials) repository.


## 3. Troubleshooting

Please see the wiki page for [Troubleshooting](https://github.com/FlyBrainLab/FlyBrainLab/wiki/Troubleshooting).

You can also report bugs and get help in this [Issue Tracker](https://github.com/FlyBrainLab/FlyBrainLab/issues).

## Citing FlyBrainLab

To cite FlyBrainLab:
```
@article {Lazar2020.06.23.168161,
	author = {Lazar, Aurel A. and Liu, Tingkai and Turkcan, Mehmet Kerem and Zhou, Yiyin},
	title = {FlyBrainLab: Accelerating the Discovery of the Functional Logic of the Drosophila Brain in the Connectomic/Synaptomic Era},
	year = {2020},
	doi = {10.1101/2020.06.23.168161},
	publisher = {Cold Spring Harbor Laboratory},
	journal = {bioRxiv}
}
```

## Reference Documentations

Coming Soon!
