# Fagprojekt

## Comment on the work in Git 

The Git commit history is not fully representative of the coding work carried out during the project. We received data from the University Hospital of Zealand that was stored on a secure computer located at DTU. Due to data protection regulations, the data could not be transferred or accessed from other devices. As a result, we had to take turns working on the code directly on this single computer. All code was developed collaboratively and equally by both Amalie and Benedicte.



### EC_EO_classification_models.ipynb
This notebook loads and preprocesses the training data, then trains and evaluates three classifiers: Logistic Regression, Support Vector Machine (SVM) and Random Forest.
For each model, subject-wise accuracies, classification reports, confusion matrices and ROC curves are computed. The best hyperparameters are decided during the cross validation. 
Finally, an ensemble of the three models is trained and evaluated.

### Statistical_tests_rq1.ipynb 
Performs pairwise McNemars tests between the three different classification models and the baselines. Lastly, bootstrapping is used to comoute confidence intervals for the precision of eahc of the three models and the baseline.


### saving_metadata.ipynb

All the mat files are looped through to check if they have at least 19 channels and if age, gender and cpr is present. If these requirements are met, the subject id of that file is appended to a list called records, and the metadata is saved to the csv file called valid_metadata.csv. This leaves 8292 valid files. 

The length of the 8292 files is then checked. If the file is between 10 minutes and 60 minutes, the subject id is appended to the list valid_time_files. 5778 files met the time requirements. The metadata for these 5778 subjects is then added to a new csv file called metadata_time_filtered.csv. 

### Converting_mat_to_set.ipynb

First, each of the .mat files is preprocessed using the same steps as Christian. The each file is converted from a .mat file to a .set file. If the recording was made with more than 19 channels, all channels above 19 were ignored. 

### Ensembling_for_labeling.ipynb

Loads the number of bins, the final model and the final scaler for each classification model from EC_EO_classification_models.ipynb. The model ensemble of the three classifiers is then created and used to predict the label of each epoch. If a file has one or more NaN values, the file is ignored. 
The results are saved in label_predictions.csv, where each line corresponds to one epoch. The file contains the Test subject ID, Epoch number, Label and Probability of that label for each epoch. The number of subjects left is calculated as 4168. The percentage of epochs with label 1  is calculated as a sanity check. 

### mean_alpha_power.ipynb

The file extracts 60 EC epochs per subject. It then calculates the mean absolute and relative power across age for all subjects. Numerous plots including plots with raw data, smoothed confidence intervals, sex-specific alpha power etc. Lstly, the absolute alpha power in the occpital channels is calculated and similar plots are made. 

### RFC.ipynb

Extracts 60 EO epochs per subject and saves in file, top_60_EO_epochs_per_subject.pkl. Extract 60 random epochs per subject and saves in file random_epochs_per_subject.pkl. 

Then trains and evalutes a Random Forest classifier on the three data sets: EC epochs, EO epochs and Random epochs. Each of the models it tested on the same hold out set of 500 subjects. 

Model performance is evaluated and confusion matrices for each model. 

### MLR.ipynb

Uses the files top_60_EO_epochs_per_subject.pkl and random_epochs_per_subject.pckl to ensure the models are trained on the same data sets as in RFC. 

A multinomial model is trained for each of the same data sets as in RFC and evaluated on the same holdout set. 

Model performance is evaluated and confusion matrices for each model. 

Near the end of the file, the absolute mean alpha power for EO and random epochs is calculated and plotted across age. The same is done for the relative power for both conditions. 

### ANOVA.ipynb

Performs two, two-way ANOVA tests. One including the interaction term and one not including the interaction term. 

### Statistical_tests_rq2.ipynb 

Compares each of the 6 models used for age classification with the baseline, which is just always predicting the majority class.

### Ground_truth_plots.ipynb

Calculates the alpha power for each of the subjects in the training set, labeled by Christian. It calculates two alpha values for each subject: one for eyes closed epochs and one for eyes open epochs. The results are plotted. 

### Coherence.ipynb

Calculates real and imaginary coherence for all the subjects and creates different plots based on coherence across age and sex specific coherence. 

### Data_plot.ipynb

Makes two different plots to visualise the lableed data. The first plot visualises the distribution of EC and EO epochs for 8 of the files labeled by Christian. 

The second plot shows the EEG signals for one subject. 
