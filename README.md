# IoT Smart Aquarium Models

Our IoT application is a Smart Aquaculture Water Quality Monitoring and Control 
System. This system will: 
 
- Monitor water temperature, pH, and turbidity in real-time. 
- Provide automated alerts when parameters deviate from optimal ranges for aquatic life. 
- Predict future water quality trends using machine learning which can enable proactive maintenance. 
- Integrate with actuators to control heaters, aerators, and filtration systems for temperature, oxygen, and clarity management. However, this integration may need to incorporate simulated data from those sensors for use in this project. 
- The primary users are aquaculture operators, researchers, and environmental agencies seeking to optimize water quality, ensure sustainability, and prevent adverse conditions in aquaculture systems.

This IoT application fits into the Industrial IoT sector, specifically within the aquaculture industry. It focuses on enhancing water quality monitoring and management for improved productivity and sustainability in aquaculture operations.

## Dashboard
We currently have [a live dashboard on Tableau Public](https://public.tableau.com/app/profile/omar.sagoo/viz/SmartAquariumTurbidityReadings/Dashboard1#1). The dashboard displays our findings with Turbidity and Temperature, It also shows our models predicted values.

## Dataset
The dataset used for this project is from the study, ["Real-time evaluation of water quality 
for aquaculture applications"](https://www.sciencedirect.com/science/article/pii/S2352340920313391#bib0001).

You can find the dataset stored in this repo, however it comes from the [Mendeley Data Repository](https://data.mendeley.com/datasets/34rczh25kc/4)

Each dataset (30 cm and 60 cm depths) contains 9,623 observations, resulting in a total of 19,246 observations across the two datasets. 

The data was collected using an IoT-based water quality monitoring system for aquaculture. Sensors were deployed at two depths (30 cm and 60 cm) in a controlled aquaculture environment to measure key parameters at regular intervals. The system recorded real-time data relevant to water quality assessment and aquaculture management.

### Features

This table lists the old feature names and their corresponding new names used in the dataset:

#### 30cm data set

| Old Feature Name | New Feature Name      | Description                                                                               |
|-------------------|-----------------------|-----------------------------------------------------------------------------|
| Date and Time              | Datetime           |  The timestamp of the sensor reading.                                         |
| Temperature (°C)         | Temperature     | Water temperature at 30 cm depth. Measured in Celcius             |
| pH                                | pH                     | Acidity or alkalinity of the water.                                      |
| Turbidity (NTU)           | Turbidity          | Water clarity, measured in nephelometric turbidity units.            |

#### 60cm data set

| Old Feature Name | New Feature Name      | Description                                                                               |
|-------------------|-----------------------|-----------------------------------------------------------------------------|
| Date and Time                  | Datetime        |  The timestamp of the sensor reading.                                        |
| Temperature (°C)             | Temperature   | Water temperature at 60 cm depth. Measured in Celcius           |
| Turbidity (NTU)               | Turbidity        | Water clarity, measured in nephelometric turbidity units.          |

## Cloning this repository:

If you would like to clone this repository and actively develop new features for this, here are the steps to clone this to your local machine and get started.

```bash
$ cd <some>/<dir>/
$ git clone https://github.com/omarsagoo/iot-smart-aquarium.git
$ cd ./iot-smart-aquarium
```

## Prerequisites: 

### Python Version
For this project we are using Python version 3.10.15, conda automatically will install and set the correct python version for the project so there is nothing that needs to be done.

### 1. Install Miniconda

If you are already using Anaconda or any other conda distribution, feel free to skip this step.

Miniconda is a minimal installer for `conda`, which we will use for managing environments and dependencies in this project. Follow these steps to install Miniconda or go [here](https://docs.anaconda.com/miniconda/install/) to reference the documentation: 

1. Open your terminal and run the following commands:
```bash
   $ mkdir -p ~/miniconda3

   <!-- If using Apple Silicon chip M1/M2/M3 -->
   $ curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o ~/miniconda3/miniconda.sh
   <!-- If using intel chip -->
   $ curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh -o ~/miniconda3/miniconda.sh

   $ bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
   $ rm ~/miniconda3/miniconda.sh
```

2. After installing and removing the installer, refresh your terminal by either closing and reopening or running the following command.
```bash
$ source ~/miniconda3/bin/activate
```

3. Initialize conda on all available shells.
```bash
$ conda init --all
```

You know conda is installed and working if you see (base) in your terminal. Next, we want to actually use the correct environments and packages.

### 2. Install Make

Make is a build automation tool that executes commands defined in a Makefile to streamline tasks like compiling code, setting up environments, and running scripts. [more information here](https://formulae.brew.sh/formula/make)

#### Installation

`make` is often pre-installed on Unix-based systems (macOS and Linux). To check if it's installed, open a terminal and type:
```bash
make -v
```

If it is not installed, simply use brew:
```bash
$ brew install make
```

#### Available Commands

The following commands are available in this project’s `Makefile`:

- **Set up the environment**:

    This will create the environment from the environment.yml file in the root directory of the project.

    ```bash
      $ make create
    ```

- **Update the environment**:

    This will update the environment from the environment.yml file in the root directory of the project. Useful if pulling in new changes that have updated the environment.yml file.

    ```bash
      $ make update
    ```

- **Remove the environment**:

    This will remove the environment from your shell. You will need to recreate and reinstall the environment with the setup command above.

    ```bash
    $ make clean
    ```

- **Activate the environment**:

    This will activate the environment in your shell. Keep in mind that make will not be able to actually activate the environment, this command will just tell you what conda command you need to run in order to start the environment.

    Please make sure to activate the environment before you start any development, we want to ensure that all packages that we use are the same for each of us.

    ```bash
    $ make activate
    ```

    Command you actually need to run in your terminal:
    ```bash
    $ conda activate iot-smart-aquarium
    ```

- **Deactivate the environment**:

    This will Deactivate the environment in your shell.

    ```bash
    $ make deactivate
    ```

- **run jupyter notebook**:

    This command will run jupyter notebook from within the conda environment. This is important so that we can make sure the package versions are the same for all of us! Please make sure that you have activated your environment before you run the notebook.

    ```bash
    $ make notebook
    ```

- **Export packages to env file**:

    This command will export any packages you install with either `conda install ` or `pip install` to the environment.yml file. This is important because if you add any packages we want to make sure that everyones machine knows to install it.

    ```bash
    $ make freeze
    ```

- **Verify conda environment**:

    This command will list all of your conda envs, the environment with the asterick next to it is the currently activated one. Ensure it is correct.

    ```bash
    $ make verify
    ```


#### Example workflows:

To simplify knowing which commands you need to run and when you can follow these instructions:

- **First time running, no env installed**:

    In the scenario where you just cloned this repo, or this is your first time using conda. These are the commands you will run to set up your environment.

    ```bash
    <!-- Make sure that conda is initialized -->
    $ conda init --all

    <!-- Next create the env from the env file in the root directory. -->
    $ make create

    <!-- After the environment was successfully created, activate the environment. -->
    $ conda activate iot-smart-aquarium

    <!-- verify the conda environment -->
    $ make verify

    <!-- verify the python version you are using. This should automatically be updated to the correct version 3.10.15 when you enter the environment. -->
    $ python --version

    <!-- Run jupyter notebook and have some fun! -->
    $ make notebook
    ```

- **Installing a new package**:

    While we are developing, we are going to need to install certain packages that we can utilize. Here is a sample workflow for installing packages. The first thing we do is verify the conda environment we are in to ensure that only the required packages get saved to the environment. We do not want to save all of the python packages that are saved onto our system to the `environment.yml` file. 

    Another thing to note is that if the package is not found in the conda distribution of packages you will get a `PackagesNotFoundError`. This is okay, just use pip instead of conda to install that specific package. Conda thankfully adds them to the environment properly.

    ```bash
    <!-- verify the conda environment -->
    $ make verify

    <!-- Install the package using conda -->
    $ conda install <package_name>

    <!-- If the package is not found in the conda channels, install the package with pip. -->
    $ pip install <package_name>

    <!-- If removing a package. -->
    $ conda remove <package_name>
    $ pip remove <package_name>

    <!-- Export the package names and versions that you downloaded to the environment.yml file -->
    make freeze
    ```

- **Daily commands to run before starting development**:

    Here is a sample workflow for the commands to run before starting development on any given day. We want to first pull all the changes from github into our local repository, 

    ```brew
    <!-- Pull changes from git -->
    $ git pull origin main

    <!-- Update env based off of the env file. It is best to deactivate the conda env before you do this step-->
    $ conda deactivate
    $ make update
    $ conda activate iot-smart-aquarium

    $ make notebook
    ```

- **Daily commands to run after finishing development**:

    Here is a sample workflow for the commands to run after finishing development for any given day.

    ```brew
    $ conda deactivate

    <!-- If you updated any of the existing packages, freeze to the environment.yml file. -->
    $ make freeze

    <!-- Commit changes to git -->
    $ git add .
    $ git commit -m "This is my commit message!"
    $ git push origin <branch_name>
    ```
## Directory Structure
```
iot-smart-aquarium/
    ├── data/
      ├── 30cm.xlsx
      └── 60cm.xlsx
    ├── notebooks/
      └──  iot-smart-aquarium.ipynb
    ├── proposal/
      └── Team 7 Proposal AAI-530.pdf
    ├── .gitignore
    ├── README.md
    ├── LICENSE
    ├── Makefile
    └── environment.yml
```

### data
This directory holds the 30cm and 60cm datasets. 

### notebooks
This directory holds all of the relevant information for the notebooks. 

### proposal
This directory holds our project proposal saved as a PDF. It explains our contributions and intial information regarding our reasoning behind this project.

### environment.yml
This is our conda file that stores all of our dependencies, including python version and package versions.

### Makefile
This makefile defines some custom commands that we can use to help ensure our environments are the same across all of our machines.

### README.md
This has basic information regarding creating and setting up the project for replicability, as well as our reasoning behind the project yourself. You are reading this in the README.

## Contributors
<table>
  <tr>
    <td>
        <a href="https://github.com/achakraborty2024.png">
          <img src="https://github.com/achakraborty2024.png" width="100" height="100" alt="Arup Chakraborty"/><br />
          <sub><b>Arup Chakraborty</b></sub>
        </a>
      </td>
      <td>
        <a href="https://github.com/Marquiseo-usd.png">
          <img src="https://github.com/Marquiseo-usd.png" width="100" height="100" alt="Marquise Oliver"/><br />
          <sub><b>Marquise Oliver</b></sub>
        </a>
      </td>
     <td>
      <a href="https://github.com/omarsagoo.png">
        <img src="https://github.com/omarsagoo.png" width="100" height="100" alt="Omar Sagoo"/><br />
        <sub><b>Omar Sagoo</b></sub>
      </a>
    </td>
  </tr>
</table>
