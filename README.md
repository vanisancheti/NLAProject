# NLAProject

## Files Attached
* <b>Task 1A</b>: NLA_Project_Task1A.ipynb
* <b>Task 1B</b>: FinalTask1B.ipynb
* <b>Report </b>: Team_22.pdf

## Problem Statement

### Task 1A
For each citance (i.e. a citation sentence that references the RP), identify the
spans of text (cited text spans) in the RP that most accurately reflect the citance.

### Task 1B
For each cited text span, identify what facet of the paper it belongs to, from
a predefined set of facets that mainly are:
* Method
* Aim
* Implication
* Results
* Hypothesis

## Task 1A

### Models
* <b> Supervised Model </b> :  For the two given inputs (citing text and the cited text) we considered building two identical networks sharing the same weights and then computing the manhattan distance between them which indicates the similarity between the two inputs.  
Network Architecture :
  * Input Layer
  * Embedding Layer
  * LSTM Layer
  * Fully Connected Layer
  * Manhattan Computation

* <b> UnSupervised Model </b>  :  We performed  semantic search. We used the BERT embeddings for computing the sentence embeddings and then took the cosine similarity between the citing sentence and every sentence of the reference paper. Among the sentences we considered top 3 sentences corresponding to maximum cosine similarity and formed the text span which is the most relevant to the citing sentence.

### Sentence Embeddings
We experimented with different sentence Embeddings
* <b>Glove Embeddings</b> We considered Glove pre-trained word embeddings to compute the sentence embeddings.
For each sentence we computed the average of the embedding of all the word involved and formed a 300 d embedding for each sentence.

* <b>BERT Embeddings</b> Bert embeddings produces word embeddings  that are dynamically computed by the context of the sentence. 
  * Bert-Based-NLI-mean-tokens 
  * SciBert Model 

## Task 1B

### Pipeline
Considering the skewed nature of data, we go with 2-layered classification pipeline. First we classify whether the given instance belong to the method facet or not. Then a multi-class classifier to identify one of the other facets in case it was previously classified as not-Method.


### Features

* <b> Positional features </b> : The sentence position in a paper can inform about the facet the sentence belongs to. We use two features based on the location of the sentence in the reference document:
Sentence position: the position of the sentence in the reference paper.
Section sentence position: the position of the sentence in the section.
* <b> BERT based sentence embeddings </b>: We use BERT to extract features, namely sentence embedding vectors, from the reference sentences. BERT produces word representations that are dynamically informed by the words around them. We encode each reference sentence (identified cited text of the RP) into a vector of size of 768.

### Resampling and Ensemble Techniques

The models we trained using raw skewed data were biased towards method facet. So we tried a few resampling and ensemble techniques, some of them are listed below :
* <b> Oversampling techniques </b>: We used Synthetic Minority Oversampling Technique(SMOTE) to synthesize new examples from the existing examples.
* <b> Undersampling techniques </b> : For this we tried CNN(Condensed Nearest Neighbour) and OSS(One-Sided Selection).
* <b> Ensemble Models </b> : We tried boosting based techniques. We tried RUSBoostClassifier and EasyEnsembleClassifier.


