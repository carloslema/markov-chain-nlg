# markov-chain-nlg
A simple Markov Chain text generator developed in Node.JS.


## installation
Download the code repository & run npm install from the command line. This will install all dependencies & allow usage of the generator.

## usage
The code can be used either on its own (by running server.js) or as an additional module for another app (using main.js).

### Server.js
The simpler method to use the code is to run server.js. This is the default for npm start.

### main.js
If you would like to run the app without a server, then it's possible to do so by requiring main.js.
This will export a variety of functions, described below, which can then be used to generate text.

## DOCS

### train
  Usage: chain.train (data: Array of String, shouldBackoff: boolean)
  
  Purpose: Trains the Markov Chain. The data should be various sentences the chain should be trained on. This must be called at least once before any text can be generated.
  
  Arguments:
  
    data: The data to train the generator on. More data will provide more accurate results.
    
    shouldBackoff: A flag to determine if the generator should perform a backing off process or not. See BACKING OFF, which will be described in detail later.
    
  Returns: None; work will be done in the chain's data.

### trainTxt
  Usage: chain.trainTxt (filepath: String, split: String)
  
  Purpose: Trains the Markov Chain Generator on data from a file. Split should be some value to split the text on; by default, will split on new lines.
  
  Arguments:
  
    filepath: A path to the file to use for training.
  
    split: A character/characters to split the file data on. Defaults to '\n'
  
  Returns: None; work will be done in the chain's data.
  
### generate
  Usage: chain.generate() : String
  
  Purpose: Generates a new line of text.
  
  Arguments: None
  
  Returns: A string representing the sequence of words that was generated.

### Backing Off
  By default, the Markov Chain generator will determine the next word to be generated based on the previous 5 words generated. For example, if the current sequence is "This is an example result of the Markov", then the next word will be determined based on the sequence "example result of the Markov".
  
  This generates more accurate results, but can often lead to copy-and-paste results - if only a single option can be found for the sequence, then it will choose that option. This is mediated by the Backing Off process, which will generate instead based off the last 4 words, last 3 words, ..., until a number of selections can be found.
  
  In short, backing off will generate less accurate results but with a variety of results; not backing off will provide more accurate results at the risk of few variations.
  
