2 scripts, 6 functions, 1 MAT-file
See filetree.png for graphical representation of file dependencies.
!(filetree.png)

## WORDINFO
Get target words and prepare related information

## BESTSTRATEGY
Investigates an automated strategy for solving Wordle, using only target words and playing on "hard mode"

## PLAYWORDLE
Play one game of Wordle with given target word

`[success,numguess,guesses,scores] = playwordle(target,possiblewords,D,lettercount,probs)`

**Inputs:**
- `target` (scalar string) - target word 
- `possiblewords` ([n 1] string vector) - list of all words to use for guessing 
- `D` ([n n] matrix) - feedback for each pair of target and guess words, represented as a numeric scalar 0:242 equivalent to a 5-digit number in base-3 
- `lettercount` ([n 26] matrix) - number of each letter contained in each guess word 
- `probs` ([n 5] matrix) - probability of each letter appearing at that location in each word (based on letter distributions)

**Outputs:**
- `success` (logical) - whether the target word was successfully guessed 
- `numguesses` (scalar) - number of guesses made 
- `guesses` (string vector) - words guessed; empty strings represent guesses not used (puzzle solved) 
- `scores` (vector) - scores (feedback) given for each guess as a vector of 0/1/2 (grey/yellow/green) 


## WORDLESCORE
Wordle score for guessed word against target

`s = wordlescore(target,guess,scalar)`

Inputs are target word (string or char), guessed word (string or char), flag for output format (logical). If `scalar` is false (default), the output is a 5-element vector of 0 (grey), 1 (yellow), or 2 (green). If `scalar` is true, the output is in the form of a single scalar value given by treating the 5-element vector as the digits of a number in base-3. The output scalar value is therefore an integer in the range 0:242.


## RANKWORDS
Assign a score to each potential word to guess, based on the matrix of guess-target feedback

`val = rankwords(D)`

Input is matrix of values, `D(j,k)`, that represent feedback for each pair of target word `j` and guess word `k`. Feedback is represented as a numeric scalar 0:242, equivalent to a 5-digit number in base-3, where 0 = gray, 1 = yellow, 2 = green.

## DRAWWORDLE
Render words in the style of Wordle

`drawwordle(words,scores)`

Inputs:
- `words` ([n 1] string vector or [n 5] char array) 
- `scores` ([n 5] matrix) - 0 = grey, 1 = yellow, 2 = green. Use -1 to show unscored words (black text on white box) 

## WORDWHEEL
Creates a wheel visualization of all second guesses, organized by first-word feedback

`wordwheel(guess2)`
Input is a table of all second guesses. Variables are `Score` (1-by-5 vectors), `Guess` (string), `Count` (scalars), and `Wins` (scalars). `Score` is the feedback for the first word; `Count` is the number of times this response is observed (across all 2315 possible target words); `Wins` is the number of times the solver successfully solves the puzzle with this opening; `Guess` is the algorithm's choice for the second guess.

## VECDIGITS
Convert numeric base-n value into a vector of digits. General utility function included here for completeness.

