# Classification of 12-lead ECGs: the PhysioNet/Computing in Cardiology Challenge 2020, by Yap Jun Hong (Nemo)

## Section 1: Why is this project important?

### Part 1.1: What is an ECG?

ECG is short for an "**E**lectro**c**ardio**g**ram", a tool frequently used by doctors to measure the strength and flow of electrical currents in the heart. Abnormalities in these electrical signals correspond to disease symptoms that doctors can recognise and address. The most common type of ECG used is a '12-lead ECG', which can be thought of as viewing the electrical signal flow in the heart from 12 different angles or viewpoints. The 12-lead ECG is measured by sticking electrodes on the limbs, for a vertical view, and on the chest, for a horizontal view. The 12-lead ECG gives information such as:

- Strength of the generated electrical signal
- Direction of the flow of the electrical signal through the heart

A reading from a healthy patient is called 'Sinus Rhythm'.

### Part 1.2: How can machine learning help doctors with reading ECG data?

Manually interpreting an ECG requires years of training on the job and in medical school. Manual interpretation is also time-consuming; doctors may make mistakes over the course of a day as they tire out. Using machine learning methods to automatically interpret ECG data can help increase the chances of noticing mistakes. In emergency situations, automatic interpretation can also be used in areas and emergencies without sufficiently skilled doctors. However, the overall goal of automatic interpretation is to assist doctors in coming to conclusions about abnormalities in the ECG.

### Part 1.4: The PhysioNet/Computing in Cardiology Challenge 2020

The PhysioNet/Computing in Cardiology Challenge 2020 put together a collection of ECG datasets from a variety of sources. One reason for making this dataset is because assembled datasets in the past were small and homogenous. The combined dataset has 111 diagnoses in total. Teams were challenged to build classification systems for identifying 27 of these 111 diagnoses, representing common cases, cases were clinically interesting, or more likely to be recognisable from ECG recordings.

**Note that project was done in Jan-Feb 2021, after the challenge was over.** Interested readers can read 'Classification of 12-lead ECGs: the PhysioNet/Computing in Cardiology Challenge 2020' by Alday et al. describing the challenge.

## Section 2: Datasets used

### Part 2.1: Dataset sources

The combined datasets are from 5 different sources. Out of these 5, 2 were used purely as training data, 2 were split into training, validation, and test sets, and 1 was included only as test data. Training and clinical ECG diagnoses (labels) were made publicly available, but validation and test data are hidden. There is no way to access the validation and test data outside of submitting projects to the Challenge administrators as there are no plans to release the validation and test data in the future.

A summary of the datasets used is shown in the table below, extracted from 'Classification of 12-lead ECGs: the PhysioNet/Computing in Cardiology Challenge 2020' paper. Explanation of the datasets follow below, extracted from the same paper.

|**Database**|**Total Patients**|**Recordings in Training Set**|**Recordings in Validation Set**|**Recordings in Test Set**|**Total Recordings**|
|---|---|---|---|---|---|
|CPSC|9458|10330|1463|1463|13256|
|INCART|32|74|0|0|74|
|PTB|19175|22353|0|0|22353|
|G12EC|15742|10344|5167|5167|20678|
|Undisclosed|Unknown|0|0|10000|10000|
|Total|Unknown|43101|6630|16630|66361|

1. **China Physiological Signal Challenge 2018 (CPSC2018), CPSC:** This source has 3 databases, the original public training dataset (CPSC), an unused dataset (CPSC-Extra), and the test dataset (the hidden CPSC set) from the CPSC2018. CPSC and CPSC-Extra datasets were shared as training sets. The hidden CPSC was split into validation and test set for the 2020 challenge.

2. **St. Petersburg Institute of Cardiological Technics (INCART), INCART:** This dataset was shared as a training set.

3. **PTB and PTB-XL, PTB:** This source includes two public databases, the PTB Diagnostic ECG Database and the PTB-XL Database, both of which are large publicly available ECG datasets. These datasets were shared as training sets.

4. **Georgia 12-lead ECG Challenge (G12EC) Database, Emory University, Atlanta, Georgia, USA, G12EC:** A new database, representing a large population from the Southeastern United States. This is split between training, validation, and test sets. The validation and test set comprised the hidden G12EC set.

5. **Undisclosed, Undisclosed:** This is a dataset from an undisclosed American institution that is geographically distinct from the other dataset sources. This dataset has never been and may never be posted publicly. This is used as a test set for the challenge.

### Part 2.2: Dataset variables

This part talks about general properties of the datasets as a whole.

1. The ECG recordings were obtained in a hospital or clinical setting. 

2. Sample frequencies varied from 257 Hz to 1 kHz.

3. Demographic information, including age, sex, and a diagnosis/diagnoses (labels), were included

4. The quality of the diagnoses (i.e. quality of the lables) depended on the clinical or research practices and included labels that were:
 a. machine-generated
 b. over-read by a single cardiologist
 c. adjudicated by multiple cardiologists
 
5. All data were provided in MATLAB and WFDB (WaveFrame DataBase) compatible format. Each ECG recording had a binary MATLAB v4 file for the ECG signal data and an associated text file in WFDB header format describing the recording and patient attributes, including diagnoses.

6. The only modifications made to the data or labels were to:
 a. make them consistent and HIPPA-compliant identifiers for age and sex
 b. Add approximate SNOMED CT codes as the diagnoses for the recordings
 c. Change the amplitude resolution to save the data as integers as required for WFDB format. Saving as integers helps reduce storage size and compute times without degrading the signal, as it only represents a change in the scaling factor for the signal amplitude
 
### Part 2.3: Sample statistics

The table below shows summary statistics for the available training sets.

|**Dataset**|**Number of Recordings**|**Mean Duration (seconds)**|**Mean Age (years)**|**Sex (male/female)**|**Sample Frequency (Hz)**|
|---|---|---|---|---|---|
|CPSC Training|6877|15.9|60.2|54%/46%|500|
|CPSC-Extra Training|3453|15.9|63.7|53%/46%|500|
|INCART|72|1800.0|56.0|54%/46%|257|
|PTB||516|110.8|56.3|73%/27%|1000|
|PTB-XL|21837|10.0|59.8|52%/48%|500|
|G12EC Training|10344|10.0|60.5|54%/46%|500|

### Part 2.4: Diagnoses and SNOMED-CT labels

SNOMED-CT is a standardised way of talking about diagnoses and medical terms.

|**Diagnosis**|**Code**|**Abbreviation**|
|---|---|---|
|1st degree AV block|270492004|IAVB|
|Atrial fibrillation|164889003|AF|
|Atrial flutter|164890007|AFL|
|Bradycardia|426627000|Brady|
|Complete right bundle branch block|713427006|CRBBB|
|Incomplete right bundle branch block|713426002|IRBBB|
|Left anterior fascicular block|445118002|LAnFB|
|Left axis deviation|39732003|LAD|
|Left bundle branch block|164909002|LBBB|
|Low QRS voltages|251146004|LQRSV|
|Nonspecific intraventricular conduction disorder|698252002|NSIVCB|
|Pacing rhythm|10370003|PR|
|Premature atrial contraction|284470004|PAC|
|Premature ventricular contractions|427172004|PVC|
|Prolonged PR interval|164947007|LPR|
|Prolonged QT interval|111975006|LQT|
|Q wave abnormal|164917005|QAb|
|Right axis deviation|47665007|RAD|
|Right bundle branch block|59118001|RBBB|
|Sinus arrhythmia|427393009|SA|
|Sinus bradycardia|426177001|SB|
|Sinus rhythm|426783006|NSR|
|Sinus tachycardia|427084000|STach|
|Supraventricular premature beats|63593006|SVPB|
|T wave abnormal|164934002|TAb|
|T wave inversion|59931005|TInv|
|Ventricular premature beats|17338001|VPB|

## Challenges

1. The ECG data have been taken with different sampling frequencies. Being able to match sampling frequencies without loss of information will be an important aspect of this project.

2. 

## References

1. C.  Ye,  M.  T.  Coimbra,  and  B.  V.  Kumar,  “Arrhythmia  detection  and  classificationusing   morphological   and   dynamic   features   of   ECG   signals”,   in _2010 Annual International  Conference  of  the  IEEE  Engineering  in  Medicine  and  Biology_,  IEEE,2010, pp. 1918–1921.

2. A.  H.  Ribeiro,  M.  H.  Ribeiro,  G.  M.  Paixao,  D.  M.  Oliveira,  P.  R.  Gomes,  J.  A.Canazart,  M.  P.  Ferreira,  C.  R.  Andersson,  P.  W.  Macfarlane,  M.  Wagner  Jr,etal., “Automatic diagnosis of the 12-lead ECG using a deep neural network”, _NatureCommunications_, vol. 11, no. 1, pp. 1–9, 2020.

3. T.-M.  Chen,  C.-H.  Huang,  E.  S.  Shih,  Y.-F.  Hu,  and  M.-J.  Hwang,  “Detection  andclassification of cardiac arrhythmias by a challenge-best deep learning neural networkmodel”, _Iscience_, vol. 23, no. 3, p. 100 886, 2020.