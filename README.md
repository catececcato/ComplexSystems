# Introduction and dataset description

This repository includes a complex systems approach to data analysis. 
The dataset used was collected by the authors in collaboration with another student during experiments conducted at Tilburg University in fall 2022.
The dataset contains EEG data from 40 participants, divided in two conditions. It was a within-participant study, so for each participant data from both conditions are available. Every datafile includes EEG data from 8 channels (Fz, C3, Cz, C4, Pz, PO7, Oz, PO8) collected from a 10 minutes interaction.  The conditions refer to the experimental setup of the study, and will not be discussed in depth in here.

# Data preprocessing
The data was collected through Matlab Simulink, therefore it was initially stored in .mat files. The files have been first converted into .csv and then to .fif to be able to work with the mne module for python. After a first inspection of the data, we noticed that it was very noisy, and we decided it would be better to preprocess it through EEGLAB, to make sure we could get a clear idea of the steps that were applied. 
Our preprocessing pipeline consisted in
1) Loading the data (already notch-filtered at 50 Hz)
2) Applying a bandpass filter of 0.5-30 Hz. We decided to cut out the higher frequencies because muscular movement is often highly reflected in gamma.
3) Changing the sampling rate. This was necessary for the next step. The sampling rate of the headset used was 250, which was changed to 256.
4) Applying Artifact Subspace Reconstruction (ASR) over all channels to reject data. ASR is an effective method for removing artifacts from EEG data. It uses principal component analysis (PCA) to identify and reject data contaminated by artifacts such as eye blinks, eye movements, and muscle activity. During this step, some channels were removed and then automatically reconstructed.


# Power Spectral Density

After these steps, we continued our analysis of the data in python. We calculated power spectral density applying the welch method in order to extract data from the aplha, beta and theta power bands for each participant. These powerbands were needed to calculate the EEG engagement index, which we have used as measure of engagement in the experiments. The data about the EEG engagement index over time was then stored in separate csv files (one for each participant, for each condition) in order to be used for further analysis in R. 

# Modules

## [Module 2 - Temporal Dynamics of the EEG Engagement Index ](Module2.ipynb)
This module investigates the temporal signature as well as stationarity of the EEG Engagement Index over time.
The following questions are adressed: 

- Section 1: What are the temporal signatures of the signal?

- Section 2: Are the signals stationary?

- Section 3: Does autocorrelation, as measured by ACF peaks, change over time?

## [Module x - interesting stuff]

_This material was initially created as part of Travis J. Wiltshire's Complex Systems Methods for Cognitive and Data Scientists course at Tilburg University._

# References
Harris, C.R., Millman, K.J., van der Walt, S.J. et al. Array programming with NumPy. Nature 585, 357–362 (2020). DOI: 10.1038/s41586-020-2649-2. ([Publisher link](https://www.nature.com/articles/s41586-020-2649-2).

Hunter, J. D., "Matplotlib: A 2D Graphics Environment", Computing in Science & Engineering, vol. 9, no. 3, pp. 90-95, 2007.

McKinney, W., & others. (2010). Data structures for statistical computing in python. In Proceedings of the 9th Python in Science Conference (Vol. 445, pp. 51–56).

Seabold, S., & Perktold, J. (2010). statsmodels: Econometric and statistical modeling with python. In 9th Python in Science Conference.

Waskom, M., Botvinnik, Olga, Kane,Drew, Hobson,Paul, Lukauskas,Saulius, Gemperline,David C, … Qalieh, Adel.(2017). mwaskom/seaborn: v0.8.1 (September 2017). Zenodo. https://doi.org/10.5281/zenodo.883859.

Virtanen, P., Gommers, R., Oliphant, T. E., Haberland, M., Reddy, T., Cournapeau, D., … SciPy 1.0 Contributors. (2020). SciPy 1.0: Fundamental Algorithms for Scientific Computing in Python. Nature Methods, 17, 261–272. https://doi.org/10.1038/s41592-019-0686-2.





