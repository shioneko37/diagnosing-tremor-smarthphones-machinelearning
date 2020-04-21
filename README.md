# diagnosing-tremor-smarthphones-machinelearning
Code for project: 'Machine Learning for Classifying Tremor Using Smartphone Accelerometers and Clinical Features'

## Introduction:
These programs are used to analyze accelerometer recordings from tremor patients (**Part 1**), and then uses unsupervised (**Part 2**) and supervised machine learning techniques (**Part 3**) to either cluster the data or train supervised machine learning classifiers using this data, respectively.

## Requirements:
The following must be installed to run all required programs:
- Python 3.7 or above (https://www.python.org/downloads/release/python-377/)
- scikit-learn (https://scikit-learn.org/stable/install.html)
- matplotlib (https://matplotlib.org/users/installing.html)
- UMAP (https://umap-learn.readthedocs.io/en/latest/)

The following files must be downloaded:
- all ".py" python program files in this repository must be downloaded
- the accelerometer recording files must be downloaded from the following link in order to run the code in Part 1, and the folder structure must be maintained as is in this compressed file: https://www.dropbox.com/s/256m6vzgr3jarns/AccelerometerRecordings.zip?dl=0
- the metadata files (**data_metadata_updated.csv** and **data_metadata_cincinatti.csv**) containing all basic non-identifying patient data must be downloaded from this repository in order to run the code in Part 1
- the .csv files containing the training data/features (which can also be obtained by running the code in Part 1) to be used for Part 2 and Part 3 must downloaded from the following link: 

## Part 1 - Analyzing Accelerometer Tremor Recordinds:
**Note:** To go directly to training machine learning classifiers using features (both time-series and frequency power-spectra metrics) obtained through analyzing tremor acceletometer recordings, skip to **part 2** below.

### Overview: 
**Program file name: tremor_accelerometerdata_analysis.py**
This program takes the raw accelerometer data for of tremor in patients who had recordings conducted (both time series and frequency-power spectrum data) and analyzes them to produce metrics that can be compared across tremor groups (i.e. PD, ET, DT and controls). This program uses a metadata file containing the list of all patients studied (including non-identifying info e.g. initials, clinician-assigned diagnosis, age, etc) and stores this information. Using the stored basic ID info, the program then opens corresponding tremor recording files (4 per patient, each corresponding to one of the 4 recording positions) and conducts both time-series and frequency-power spectrum analysis. 

These analyses are conducted using the functions 'timeseries_analysis' and 'freq_analysis respectively', which are called in the main body of code and take as input a given tremor recording .csv file. The analysis metrics obtained from processing all the recording data are then stored in a single .csv file containing the list of all patients (i.e. initials) and all of the analysis metrics obtained for each patient in corresponding columns. Statistical analysis can then be done using this final output file to compare the values of metrics across each tremor group as a whole (conducted in SPSS for this project).

The final output file containing all analysis features for each patient can also be used as input features for machine learning algorithms (see README file for mor details).

**Program file name: **tremor_analysis_cincinatti.py**
Similar to tremor_accelerometerdata_analysis.py, this program analyzes recordings made specifically in cincinatti, and applies the same analysis as in tremor_accelerometerdata_analysis.py.

### Configuration:
#### Folder Directory Structure:
The file **tremor_accelerometerdata_analysis.py** must be saved in the same folder that the metadata file and the date-folders of the accelerometer recording files are stored in (see next paragraph). All recording files must be stored locally on the user's machine, in the same folder directory structure as downloaded.

Specifically, each of the 4 tremor recording .csv files per patient are stored in their own respective folders corresponding to each of the recording positions (i.e. 'bat', 'kin', 'out' & 'rest'). These four folders are stored in a patient's own folder, named according to their initials (e.g. 'DG'). Each of these patient-folders are stored in a 'date' folder corresponding to the date the patient was recorded in the format month-space-day-space-year (e.g. 'may 14 2015').

#### Modification of PATH:
In **tremor_accelerometerdata_analysis.py**, the PATH variable refers to the folder path where this file, the required input .csv metadata file (the metadata file containing the list of all patient data (patient initials/labels, age, sex etc)) and the tremor accelerometer data files for each patient are stored. The user must set PATH according to where this file and the required .csv files are stored on their computer. 
This similary applies to **tremor_analysis_cincinatti.py** as well.

## Part 2 - Unsupersived Clustering Analysis:
### Overview:
The programs in part 2 use as features the metrics obtained from analyzing the accelerometer recordings in part 1 (above). Firstly, unsupervised machine learning methods are used to cluster tremor data (program #1, #2). Next, supervised machine learning classifiers are trained and tested on the tremor data (program #3, #.

### Program #1 - tremor_clustering.py:
#### Description:
This program uses unsupervised machine learning techniques to cluster data agnostically without using their known labels, and only uses known labels to color-code the data when being displayed for the user. Specifically, the Uniform Manifold Approximation and Projection for Dimension Reduction (UMAP) is used (https://arxiv.org/abs/1802.03426), but also other methods such as t-SNE (https://scikit-learn.org/stable/modules/generated/sklearn.manifold.TSNE.html) can be used as well in this code.

The data features used for clustering analysis can be chosen by the user, and include accelerometer data alone, accelerometer data alone but only for patients who had clinical data, combined accelerometer and clinical data, and the use of control (non-tremor) data amongst these groups.

#### Configuration:
The data features used are imported from the following .csv files, which must be downloaded to the user's machine and located in the same folder:
- AllAnalysisData_training1.csv
- AllAnalysisData_training_sameAsClinical.csv
- AllAnalysisData_training_sameAsClinical_+clinicalVars.csv
- AllAnalysisData_training1_+controls_noExtras.csv
- AllAnalysisData_training1_+controls_noExtras.csv
- AllAnalysisData_training1_+controls.csv
- AllAnalysisData_training1_+controls_noET.csv

The PATH variable refers to where the above listed data-feature .csv files are stored, and the user must set PATH according to where these files are stored on their machine.

### Program #2 - tremor_clustering_clinicalData.py:
#### Description:
This program uses unsupervised machine learning techniques to cluster data agnostically using clinical data as features and without using their known labels, and only uses known labels to color-code the data when being displayed for the user. Specifically, the Uniform Manifold Approximation and Projection for Dimension Reduction (UMAP) is used (https://arxiv.org/abs/1802.03426), but also other methods such as t-SNE (https://scikit-learn.org/stable/modules/generated/sklearn.manifold.TSNE.html) can be used as well in this code

The data features used for clustering analysis can be chosen by the user, and includes features from clinical data alone (see Configuration below).

#### Configuration:
The data features used (i.e. clinical data) are imported from the following .csv file, which must be downloaded to the user's machine:
- tremor_clinical_spreadsheet_forAnalysis.csv

The PATH variable refers to where the above listed data-feature .csv file is stored, and the user must set PATH according to where the file is stored on their machine.

## Part 3 - Supervised Machine Learning Classifiers:


## Maintainers:
Current maintainers:
- Dr. Arjun Balachandar (http://linkedin.com/in/arjunbalachandar)
