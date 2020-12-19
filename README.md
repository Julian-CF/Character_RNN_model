# Character prediction RNN to generate sentences based on movie quotes.
This code covers the implementation of a Recurrent neural network to predict the next output characterbased on the textual portion of the Stanford Sentiment Treebank data.  This has been performed by exploring different hyperparameters.  The approach was to try different combinations of hyperparameters in order toget a better intuition on each hyperparameter’s influence on the model’s performance (evaluated with the validation accuracy to avoid overfit issues).  This provided the hyperparameters listed below as well as their respective range of possibilities (based on the intuition gained as explained above) which were then usedwithin a grid search to find our best possible model again evaluated with the validation data set:

#### Recurrent Neural Network Model variants (RNN)
Three models have been explored:  LSTM, GRU and Vanilla RNN.Recurrent Neural Network’s Number of layers and layer sizes1, 2 and 3 RNN layers have been used for hidden sizes of 64, 128, 256 and 512.

#### Multi-Layer Perceptron’s (MLP) Number of layers, layer sizes and activation functions
The last hidden state of the RNN has been either transformed linearly or using a Multi-Layer Perceptron.We tried MLP models with 2 or 3 layers of sizes 64, 128 or 256.

#### Input lengths and batch size
In order for the computation to be reasonably fast, we decided to use batches of 64, 128, 256 and 512 forthe training of the model.  One issue with that was that the sentences data have variable length.  Therefore,two variants were used to keep a consistent input length:  padding and a method joining all the sentencestogether and slicing them evenly.  The issue with padding was that there was a bias towards the paddingelement therefore we used the second option with input lengths of 32, 64 and 128.

#### Optimizer and Learning rate
The Adam and SGD optimizer and learning rates of 0.0001, 0.005, 0.001, 0.005 and 0.01 have been used.

#### Best and final model:

- LSTM.
- 2 layer RNN with hidden sizes of 512.
- A two layer MLP with layer sizes of 256.
- Batche size of 64 and input sequence length of 128
- Adam optimizer with learning rate of 0.001

It is worth noting that the vanilla and GRU have also been added to the code but the best model implementation (LSTM) is found at the end of the code.  

## Results
A code for the training and validation loss plots of and the validation, test and training accuracies with the respective results can also be found.

## Sentence Generation
Finally, 5 sentence generation have been tried. I used the following beginning of sentences to generate its sentence completion using our best model:
- ”Your father ”
- ”Hello, this is the end of books and art ”
- ”I am lacking inspiration”
- ”I believe that”
- ”Welcome to”

The generated sentences can be found in the code. The process was stopping the sentence when the character output was a dot, a question mark, an exclamation mark or when the length of the sentence was becoming larger than 128 since it was our sequence length input used for training.  The latter ensures a hard stop when the model is going to generate infinitely a certain pattern of output. 
