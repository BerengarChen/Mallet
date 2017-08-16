Learning the Latent "Look"
======

## Usage
This code provides an implementation of the research paper:
```
Learning the Latent "Look": Unsupervised Discovery of a Style-Coherent Embedding 
Wei-Lin Hsiao, Kristen Grauman
International Conference on Computer Vision (ICCV), 2017
```
See our [project page](http://vision.cs.utexas.edu/projects/StyleEmbedding/) for more detail.

This project is based on [MALLET](https://github.com/mimno/Mallet) polylingual LDA implementation, with a few minor changes:  
We smoothed the topic/word counts to topic/word probabilities.  
For stability, after convergence, we run 100 more samplings to average the learnt topic/word probabilities.


## Installation

To build a Mallet 2.0 development release, you must have the Apache ant build tool installed. From the command prompt, first change to the mallet directory, and then type
`ant`

If `ant` finishes with `"BUILD SUCCESSFUL"`, Mallet is now ready to use.

## Usage

1. Prepare your documents. Every document is a single line in the file, every line is
```
docID language_name word_1 word_2 ...
```
The documents for each language will be in its own file. The Nth document in language 1 is assumed to have the same topic distribution (though a different vocabulary) as the Nth document in language 2, and so on. An example corpus is here. If a language lacks Nth document, just leave if blank as
```
docID language_name 
```
An example corpus can be downloaded [here](mallet.cs.umass.edu/pltm.tar.gz).

2. Import documents for each language. The `token-regex` is the appropriate one to use with our attribute vocabulary.
```
bin/mallet import-file --input <document_filename> --output <sequence_filename> --keep-sequence --token-regex '[\p{L}\p{N}_<>/-]+|[\p{P}]+'
```
3. Train a model.
```
bin/mallet run cc.mallet.topics.PolylingualTopicModel --language-inputs <language1_sequence> <language2_sequence> ... <languageN_sequence> --alpha <alpha_val> --beta <beta_val> --num-topics <number_of_topics> --output-average-doc-topics <theta_save_to_filename> --output-average-topic-keys <topic_top_words_save_to_filename> --output-average-key-probs <phi_save_to_filename>
```

For details about the commands please visit the API documentation and website at: http://mallet.cs.umass.edu/


