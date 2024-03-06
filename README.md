# cm_course_tmp
This is a temporary repository for providing installation instructions of notebooks for the Coastal Modelling course.

## Download and Initial Setup Instructions
1. Download the course materials from the provided link: [Download Course Materials](https://filesender.surf.nl/?s=download&token=ad4c484b-0e7e-41fd-b95a-b2cb87d13ff1).
2. Extract the downloaded package to a location of your choice, for example, `C:\Users\your_name\cm_course`.

Next, navigate to the `...\cm_course\notebooks` directory, open the `config.py` file, and update the paths for the configuration files (`*.mdu` & `*.mdw`) and the D-Hydro installation (`*.dll`).

## Installation Instructions
We recommend using [Anaconda](https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Windows-x86_64.exe) to manage your Python installation and pip for installing additional libraries. Follow these steps after installing Anaconda:

1. Open `Anaconda Prompt`.
2. To create a new environment, locate the `environment.yml` file included in the downloaded package and run:

```
> conda env create -f environment.yml
```

3. Activate the newly created environment and launch Jupyter Notebook:

```
> conda activate cm_course_env
> jupyter notebook
```
Within the Jupyter environment, search and open the Jupyter Notebook (...\cm_course\notebooks\excercise.ipynb).

4. In the Jupyter environment, navigate to and open the `exercise.ipynb` notebook located in `...\cm_course\notebooks`.

## Using this Notebook
Once opened, click the "Run all Cells" button (⏩) to execute all cells. The raw code will be hidden by default.

### Model Setup
The model consists of a 2D D-Flow and D-Waves domain. The left-hand side of the domain is onshore, the right-hand side is offshore, and the upper and bottom sides are the lateral boundaries. The boundary conditions, i.e. the water levels and wave conditions, are enforced on the offshore boundary, causing them to travel from right to left. The domain features a base resolution of approximately 20x20m, which becomes coarser towards the lateral and offshore boundaries. A schematized bathymetry is used based on a [Bruun profile](https://textbooks.open.tudelft.nl/plugins/generic/pdfJsViewer/pdf.js/web/viewer.html?file=https%3A%2F%2Ftextbooks.open.tudelft.nl%2Ftextbooks%2Fcatalog%2Fdownload%2F37%2F92%2F383%3Finline%3D1#a8), combined with a 1D Gaussian shaped feature to simulate the presence of a breaker bar.

### Running the Model
This Notebook enables you to run and interact with a D-Hydro (D-Flow and D-Waves) model through the Basic Modelling Interface (BMI; [BMI Documentation](https://csdms.colorado.edu/wiki/BMI)). After initializing the model (⏩), click the "Run model" button to start the simulation. The default number of timesteps is set to 15, which are not the D-Flow timesteps (6 seconds) but are the intervals after which the models exchange information with each other and with the notebook. This exchange interval is set at 300 seconds, but can be modified in the `config.py` file. A certain spin-up time is necessary for the water levels and currents to stabilize after initialization. The default setting of 15 timesteps with 300-second exchange intervals (equivalent to 4500 seconds) is generally adequate for this spin-up. You are encouraged to verify this by analyzing the intermediate model results.

### Plotting
The main focus of this exercise is on the center transect in the domain. The 1D plots provide a cross-shore representation of the bed level, water level, wave height, cross-shore current velocity, and resulting sediment transport rates. These plots are intended to help you understand the interaction between the coastal profile and the breaking of oblique incoming waves, as well as the resulting longshore transport. Additionally, the 2D maps offer a visual inspection tool for assessing the influence of the boundaries and the overall model stability. The slider next to the "Run model" button allows you to examine the model outcomes at different moments in time. The plot limits, whether for the y-axis or colorbar, can be dynamically adjusted using the sliders provided under **Plot limits**.

### Changing Model Parameters
The notebook distinguishes between two types of parameters: BMI-adjustable (under **Model settings**) and not BMI-adjustable (**Configuration settings**):

1. Parameters in the **Model settings** category can be modified while the Notebook is active. For example, after initializing and running the model (including the initial spin-up time), you can add a breaker bar by changing `hbar` to 2 meters. If you press "Run model" afterward, the model will continue the simulation for the set number of timesteps, now including the modified bed level. In this case, the initial spin-up time of 15 timesteps is not required (3-5 should suffice).

2. Parameters in the **Configuration settings** category require restarting the model after changes. If, for instance, the value for wave height is adjusted in its respective cell, this change is saved to the configuration file. The model must be restarted to apply these changes, which is most easily done by rerunning the entire notebook (⏩). The model's initialization will then proceed based on the updated configuration file(s), either `*.mdu` (D-Flow) or `*.mdw` (D-Waves).
