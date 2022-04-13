# Classification of Myocardial Blood Flow Based on Dynamic Contrast Enhanced Magnetic Resonance Imaging Using Hierarchical Bayesian Models: Data and Code
## Data
There are four sets of data are included here. These four sets of data are corresponding to the data used in the paper. In particular, the results of Serial 28 have been shown in the main text and the results of Seirals 25 - 27 have been shown in the online supplimentary matirial.

There are two types of data in this study. One is the original data which is saved in the file with filename extension ''.IMA''. Both image information and MRI parameters are saved in these files. The other is the contouring data which is saved in the file with filename extension ''.con''. This file is a text type file which contains the information of the contour. The contours are manually obtained by a software named ''QMASS, Medis Medical Image'' (https://medisimaging.com/medis-suite-mr/).

## Code
The code of the algorithm illustrated in the paper has been written in Python. There are two parts of codes, i.e. data reading codes and main codes. The data reading codes are written in the file with name ''datareading.py''. These codes can be used to read the ''.IMA'' and ''.con'' data. Given right directories of the ''.IMA'' and ''.con'' files and the heart location (The four vertices of the rectangle that contains the image of the heart), key information such as image matrix and contour coordinates can be extracted. Details can be further found in the main codes part.

The main codes can be separated into different parts for different functions. Each part is marked by annotation. The usages of different parts are illustrated as follows:

### Library

Introduce necessary libraries for the algorithm

### Read Data

Use ''datareading.py'' to read the data given data directories and heart location (parameter ''cutesize'' in the code).

### basic info for analysis

Here are some explanations of the parameters:

#### Parameter ''parameter_28_2'' represents the end time point of the baseline pre calculated. ''28'' indicates the data index and ''2'' indicates the mid slice index (1 denotes Basal slice, 2 denotes mid slice and 3 denote apical slice).
#### Parameter ''bm_df_28_2'' represents the dataframe type of the myocardial tissues for serial 28, mid slice. Each row of the dataframe shows one piexl. There are three columns showing X coordinate, Y coordinate and signal intensity.
#### Parameter ''data_slice_28_2_mc'' represents motion corrected image matrix for serial 28, mid slice.
#### Parameter ''p_en_x_2'' represents X coordinate for endocardium for the mid slice. Parameter ''p_ep_y_2'' represents Y coordinate for epicardium for the mid slice. Other similar parameters named according to the same naming convention。
#### Parameter ''bp_2'' denotes blood pool signal for mid slice.
#### Parameter ''myo_2'' denotes myocardial signal for mid slice.

### show images

Visualize images given endocardial contour, epicardial contour and blood pool location.

### baseline estimation

Estimate baseline end point for the blood pool.

### Fermi estimation

Using Fermi method to estimate the myocardial blood flow (MBF).

### estabilish dataframe

Estabilsh a dataframe that contains MBF values and Fermi parameetrs. Specifically, each rwo of the dataframe denotes a pixel. Columns show information X coordinate, Y coordinate, MBF, Fermi parameter A, Fermi parameter $\tau$ and Fermi parameter $\omega$ and estiamted variance of the Fermi estimation.

### MBF map using Fermi

Plot Fermi estimated MBF map.

### GMM

Using Gaussian mixture model to classify the Fermi estimated MBF into two classes (healthy tissue and lesion). Put the label into the established dataframe and plot the classification map.

### MCMC random walk setting

Fermi parameters are sampled using Metropolis-Hasting algorithm with Gaussian random walk proposal. Set the variance of the random walk and put it into the dataframe.

### HBM function given Gamma prior

HBM method using Gamma prior

### HBM function given log Gaussian prior

HBM method using log Gaussian prior

### process HBM given log Gaussian prior (Gamma prior is annotated)

Process the HBM method using log Gaussian prior given hyperparameters.

### results analysis

The HBM methods will retrun all sampling results. The codes in this part show some analysis to the sampling results.

