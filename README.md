## Word-level Adversarial Examples in Convolutional Neural Networks for Sentence Classification

This repository holds the **Word-level Adversarial Examples** codes and models for the papers 
**HotFlip: White-Box Adversarial Examples for Text Classification**

[[Arxiv Preprint](https://arxiv.org/abs/1712.06751)]
[[ACL 2018](https://www.aclweb.org/anthology/P18-2006)]

This repository includes robustness improvements using adversarial training improvement. 

Some examples generated from CNN are able to trick both CNN and BLSTM. please have a look at  ``examples.txt``, with the first column as its label, the second as its confidence, the third as the sentence. ``examples_turker.txt`` are examples given to [Amazon Mechanical Turk](https://www.mturk.com/mturk/welcome) and they annoted the adversarial and original examples share the same meanings.
### Requirements
Code is written in Python (2.7) and requires Theano (0.9), NLTK.

Using the pre-trained `word2vec` vectors will also require downloading the binary file from
https://code.google.com/p/word2vec/


### Data Preprocessing
To process the raw data, please refer to [https://github.com/AnyiRao/SentDataPre](https://github.com/AnyiRao/SentDataPre)

set ``word2vec`` path points to the word2vec binary file (i.e. `GoogleNews-vectors-negative300.bin` file). 

### Different Versions of Codes
``add_one_word.py`` Only one word flip 

``add_two_word.py`` Allow two word flip 

``add_one_word_sub.py`` Only one word flip using gradient subtraction.

``change_labels.py`` Only one word flip with labels change

``use_pretrained_gene_testset.py`` Use pretrained model to generate adversarial test set and test accuracy (with confidence) on it. 

``conv_net_sentence.py`` As same as Kim's CNN

* **lstm**
The adversarial examples generated from CNN are able to attack a BLSTM.

	``sst2_lstm.py`` Train a BLSTM model

	``use_pretrained_model.py`` Use adversarial examples from CNN (e.g. ``sst2_0.4_two_examples.txt``) to attack pretrained BLSTM model.
 
### Running the models (CPU)
Example commands:

```
THEANO_FLAGS=mode=FAST_RUN,device=cpu,floatX=float32 python conv_net_sentence.py -nonstatic -rand
THEANO_FLAGS=mode=FAST_RUN,device=cpu,floatX=float32 python conv_net_sentence.py -static -word2vec
THEANO_FLAGS=mode=FAST_RUN,device=cpu,floatX=float32 python conv_net_sentence.py -nonstatic -word2vec
```

This will run the CNN-rand, CNN-static, and CNN-nonstatic models respectively.

### Using the GPU
GPU will result in a good 10x to 20x speed-up, so it is highly recommended. 
To use the GPU, simply change `device=cpu` to `device=gpu` (or whichever gpu you are using).
For example:
```
THEANO_FLAGS=mode=FAST_RUN,device=gpu,floatX=float32 python conv_net_sentence.py -nonstatic -word2vec
```

### Citation

If you use this repository in your researh, please cite:

	@inproceedings{ebrahimi2018hotflip,
	  title={HotFlip: White-Box Adversarial Examples for Text Classification},
	  author={Ebrahimi, Javid and Rao, Anyi and Lowd, Daniel and Dou, Dejing},
	  booktitle={Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics (Volume 2: Short Papers)},
	  pages={31--36},
	  year={2018}
	}
