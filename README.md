# cm_course_tmp
This is a temporary repository for providing installation instructions of notebooks for the Coastal Modelling course.

## Download and initial setup instructions
Download the course material [here](https://filesender.surf.nl/?s=download&token=ad4c484b-0e7e-41fd-b95a-b2cb87d13ff1).
Afterwards, extract the package at a location of your choice (e.g. C:\Users\name\cm_course\...)

Now open the config.py file (...\cm_course\notebooks\config.py) and provide the new paths for the configuration files (*.mdu & *.mdw) and D-Hydro installation (*.dll). 

## Installation instructions
To run these notebooks locally on your (Windows) machine we use [Anaconda](https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Windows-x86_64.exe) to manage our Python installation. We will also use pip to install some other libraries.

After installing Anaconda, launch `Anaconda Prompt`.

To create a new environment, find the environment.yml file that was part of the downloaded package and run:
```
> conda env create -f environment.yml
```

Now activate the environment and start jupyter notebook
```
> conda activate cm_course_env
> jupyter notebook
```
Within the Jupyter environment, search and open the Jupyter Notebook (...\cm_course\notebooks\excercise.ipynb).

## Using this Notebook
Once opened, click the "Run all Cells" button (⏩). The raw code will be hided on default.

### Model setup
The model consists out of a 2D D-Flow and D-Waves domain. The left-hand side of the domain is onshore, right-hand side is offshore and the upper and bottom sides are the lateral boundaries. The boundary conditions, i.e. the water levels and wave conditions, are primarly enforced on the offshore boundary, and thus travel from right to left. Both domains have base resolution of approximately 20x20m, but becomes coarser towards the lateral and offshore boundaries. A schematized bathymetry is used based on a [Bruun profile](https://textbooks.open.tudelft.nl/plugins/generic/pdfJsViewer/pdf.js/web/viewer.html?file=https%3A%2F%2Ftextbooks.open.tudelft.nl%2Ftextbooks%2Fcatalog%2Fdownload%2F37%2F92%2F383%3Finline%3D1#a8), combined with a 1D Gaussian shaped feature that can be added to mimic the presence of a breaker bar. 

### Running the model
With this Notebook, you will be able to run and intervene with a 2DH morphostatic D-Hydro (D-Flow and D-Waves) model. The initialization and execution of the model are performed with BMI (Basic Modelling Interface; https://csdms.colorado.edu/wiki/BMI). The main advantage of running this model using BMI, next to the easy implementation in a Python environment, is the possibility to exchange information from and to the model during simulation. This allows us to plot and update model information, for instance the bed levels, while the simulation is running. 

To run the model, after initialization (⏩), press the "Run model" button. You'll see that the default number of timesteps is set to 15. These are not D-Flow timesteps (= 6 s), but the timesteps after which the models exchange information with eachother and with the notebook. This exchange timestep is set at 300 seconds, but can be changed in the config.py file. A certain spin-up time is required for the water levels and currents to settle after initialization. The default of 15 timesteps and 300 seconds exchange intervals (= 4500 seconds) has been found to be a proper spin-up time for now. You can check this yourself by analyzing the intermediate model results. 

### Plotting
The main focus of this exercise is around the centre transect in the domain. The 1D line plots show a cross-shore representation of the bed level, water level, wave height, (cross-shore) current velocity and resulting sediment transport rates.  Main purpose of 2D to get an idea of the instabilities.... The plot limits, either ylim or colorlim, can be dynamically adjust with the provided sliders under **Plot limits**

### Changing model parameters
Two options



