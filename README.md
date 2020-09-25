# AI-based-Poetry-Sonnet-Generation

## Run the main notebook - Sonnet Generation.ipynb
Note: Go to the last cells for examples of outputs

To try for yourself:

1. Download the repo and
2. Create model using the ```create_model()``` function below
3. Load model weights ```model.load_weights('<folder_path>/model_2_wts.h5'```
4. Run the last cell to generate new sonnets


## Solution description
The dataset is first broken into individual sentences and stored in a list

This list is then tokenized to get word index + a zero token (which means null)

For each line (sentence) in the input list-> create a sequence for every word such that it has the token of itself + previous words token in that sentence 
so for a sentence containing n words there will be a nxn matrix for each sentence contining 1 word to n words - 
[0 0 0          0        token_first_word]
[0 0 0 token_first_words token_second_word ] ...

This is done in order to train the neural network so that it predicts the next likely word based on the input sequence of previous word - 
so the last value can be  treated as a the output and the rest of the list as input. in this manner success words are generated based on previous outcome.

Perform one hot encoding on the last column (value to be predicted)

Building the model - 

Simple model - sequential +embedding (dimension = 240 due to lot of vatiaions as input is a language) + bidirectional LSTM + dense layer with softmax activation function + categorical loss function 

Now train the model epochs = 100 (due to presence of unsructured data)
