# Project1: Word-level language modeling RNN and LSTM Using Pytorch
#### Result:
- Generated Text is:
![alt text](image.png)

- This example trains a multi-layer RNN (Elman, GRU, or LSTM) on a language modeling task.
By default, the training script uses the Wikitext-2 dataset, provided.
The trained model can then be used by the generate script to generate new text.
```bash
python main.py --cuda --epochs 6            # Train a LSTM on Wikitext-2 with CUDA, reaching perplexity of 117.61
python main.py --cuda --epochs 6 --tied     # Train a tied LSTM on Wikitext-2 with CUDA, reaching perplexity of 110.44
python main.py --cuda --tied                # Train a tied LSTM on Wikitext-2 with CUDA for 40 epochs, reaching perplexity of 87.17
python generate.py                          # Generate samples from the trained LSTM model.
```

- The model uses the `nn.RNN` module (and its sister modules `nn.GRU` and `nn.LSTM`) which will automatically use the cuDNN backend if run on CUDA with cuDNN installed. During training, if a keyboard interrupt (Ctrl-C) is received, training is stopped and the current model is evaluated against the test dataset. 

- With these arguments, a variety of models can be tested. As an example, the following arguments produce slower but better models:
```bash
python main.py --cuda --emsize 650 --nhid 650 --dropout 0.5 --epochs 40           # Test perplexity of 80.97
python main.py --cuda --emsize 650 --nhid 650 --dropout 0.5 --epochs 40 --tied    # Test perplexity of 75.96
python main.py --cuda --emsize 1500 --nhid 1500 --dropout 0.65 --epochs 40        # Test perplexity of 77.42
python main.py --cuda --emsize 1500 --nhid 1500 --dropout 0.65 --epochs 40 --tied # Test perplexity of 72.30
```

- Perplexities on PTB are equal or better than
[Recurrent Neural Network Regularization (Zaremba et al. 2014)](https://arxiv.org/pdf/1409.2329.pdf)
and are similar to [Using the Output Embedding to Improve Language Models (Press & Wolf 2016](https://arxiv.org/abs/1608.05859) and [Tying Word Vectors and Word Classifiers: A Loss Framework for Language Modeling (Inan et al. 2016)](https://arxiv.org/pdf/1611.01462.pdf), though both of these papers have improved perplexities by using a form of recurrent dropout [(variational dropout)](http://papers.nips.cc/paper/6241-a-theoretically-grounded-application-of-dropout-in-recurrent-neural-networks).

# Project2: Numpy based RNN Implementation from Scratch and apply Char-level Language Modeling 
#### Result
- Generated Text is:
![alt text](image-1.png)
#### Dataset and Implemetation
- I use (this http://cs.stanford.edu/people/karpathy/shakespeare.txt) shakespeare datset for traing our RNN model and then generate text
- Below is a diagram of the RNN computation that we will implement below. We're plugging characters into the RNN with a 1-hot encoding and expecting it to predict the next character. In this example the training data is the string "hello", so there are 4 letters in the vocabulary: [h,e,l,o].
![alt text](image-2.png)
