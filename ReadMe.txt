1.	Data preprocessing
Data investigation and preparation were mostly processed in the Data_Preparation.ipynb. 
From the very first steps it was noticeable the dataset was severely imbalanced: compare the appearance of "Individual Contributor/Staff" 1105 times to "Owner" 4 times. Also, the total number of labels per column was organized in descending order which led to hypothesis that there might be some hierarchical data order, which was not confirmed later by deeper analysis.
To deal with imbalance several techniques were used, first it was oversampling specifically for “Owner” labels. 150 synthetic rows with that minor label were generated and added to final dataset ‘oversampled_dataset.xlsx’. Later on, in model training file, iterative stratified sampling  (from skmultilearn library) and class weights techniques were used to manage dataset imbalance. Iterative stratified sampling works like sklearn’s train_test_split function but for imbalanced dataset offering ability to pick up each label in each split equally.
Tokenizer was BertTokenizer

2.	Model and architecture selection

To my knowledge there are several options to deal with multi-label classification problem, 
like classic ML algorithms or deep learning solutions based on transformer architecture. 
I chose the BERT model because it was straightforward for me. 
Obviously, every task can be done better with implementation of a training pipeline and experiments, but BERT was a good enough choice.

3.	Training and testing the model

As was mentioned above iterative stratified splitting was chosen for appropriate ds splitting. 

Metrics were accuracy, F1 Micro, F1 Macro. Also, I was considering Hamming loss as a suitable one for the MLC problem.

2 training sessions were performed, one on a local machine with CPU (took approx. 15 hours for 10 epochs) and the 
second one is on Google Colab’s GPU. Final submitted solution trained via colab. But, as an interesting fact, 
some training params differ in both cases:

			CPU training	Colab training
Training Batch size
				8	16
Valid Batch size
				4	8
Epochs
				10	8
Learning rate
				1e-05	2e-05


Increased LR and batch size lead to faster training in general.

4.	Interpreting results

Test inference of the trained model on separate test data showed these results:
Test Metrics:
Accuracy = 0.8814
F1 Micro = 0.9160
F1 Macro = 0.8935
	
Which is not perfect at all but good enough for specific case. 
Further work can be done in the field of hyperparameters adjustment, deeper dataset manipulations, 
changing the model, and integration of all of the above in the training pipeline to get the best results out of each experiment.
