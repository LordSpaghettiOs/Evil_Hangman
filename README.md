# Evil Hangman
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Travis (.org)](https://travis-ci.org/caminek/Evil_Hangman.svg?branch=master)
![AppVeyor](https://ci.appveyor.com/api/projects/status/github/caminek/Evil_Hangman?branch=master&svg=true)

Tested on:
- Ubuntu 16.04 LTS (Xenial Xerus) with gcc 5.4.0 and cmake 3.12.4
- Ubuntu 18.04 LTS (Bionic Beaver) with gcc 7.4.0 and cmake 3.12.4
- Windows using MSYS2, gcc 9.1.0 (64-bit), gcc 5.3.0 (32-bit) and clang 9.0.0

Incompatible with:
- OS X

# About

### Reflection On The Assignment
Taken during the Summer Session, Computing II (Data Structures) proved to be one of the most challenging courses I would take.  The semester-long assignment would require us to implement most-everything we had learned in one way or another.  We had to create string and vector libraries, unit tests, self-learn AVL Trees (if we wanted the maximum points available), and implement everything using opaque objects.  Code was to be written on Linux using Vim.  Using GCC as the compiler, the Makefile had to include the complier option -Wall and memory leaks were to be checked using Valgrind.

This project earned "extra credit" as it solved a common problem found in other projects. The initial lag that would occur with the first guess, and to a lesser extent, the second guess entered was eliminated by swapping out the largest vector instead of deep copying it.

While this was intended to be a two-person project, I completed this project solo as we had an odd number of people in the class. It was during this time that I learned how to code while looking though my tears.

Of all the courses I have taken, this remains my favorite.  While very difficult, it was fair, and it pushed me like no other. I've wholeheartedly recommended this class to those who were looking for a challenge.

### Assignment
In case you aren't familiar with the game of Hangman, the rules are as follows:

> 1. One player chooses a secret word, then writes out a number of dashes equal to the word length.

> 2. The other player begins guessing letters. Whenever she guesses a letter contained in the hidden word, the first player reveals every instance of that letter in the word. Otherwise, the guess is wrong.

> 3. The game ends either when all the letters in the word have been revealed or when the guesser
	has run out of guesses.

Fundamental to the game is the fact the first player accurately represents the word she has chosen. That way, when the other players guess letters, she can reveal whether that letter is in the word. But what happens if the player doesn't do this? This gives the player who chooses the hidden word an enormous advantage. For example, suppose that you're the player trying to guess the word, and at some point you end up revealing letters until you arrive at this point with only one guess remaining:

>D O – B L E
	
There are only two words in the English language that match this pattern: “doable” and “double.” If the player who chose the hidden word is playing fairly, then you have a fifty-fifty chance of winning this game on your next guess if you guess 'A' or 'U' as the missing letter. However, if your opponent is cheating and hasn't actually committed to either word, then there is no possible way you can win this game on that first guess. No matter what letter you guess, your opponent can claim that she had picked the other word. That is, if you guess that the word is “doable,” she can pretend that she committed to “double” the whole time, and vice-versa.

### Prerequisites

1. A string-handling module. You have already completed your MyString module for this purpose.

2. A generic vector module. You have already completed this in class

3. An array of Vectors of MyStrings containing the entire dictionary read from the “dictionary.txt” file. The dictionary file contains an unabridged dictionary with over 120,000 words. The array of Vectors of MyStrings should hold 30 Vectors (to hold vectors of words of lengths 1 to 29), each of which holds MyString objects, which each hold a word.

4. An AssociativeArray module, as described during class, which allows using MyString data as the “key” or “index” to locate a particular Vector of Mystrings. The AssociativeArray must be based on (implemented using) the AVL Tree that you have written in class (or the easy way out described in lab). There will be no duplicate keys. When a new MyString data item is added to the AssociativeArray, a “key” value (also a MyString object) will be given. That “key” is located in the AVL tree (or added to the AVL tree), and the data MyString is added to the Vector associated with that “key”. Look-up by “key” yields

### Requirements

1. Prompt the user for a word length, re-prompting as necessary until she enters a number such that there's at least one word that's exactly that long. That is, if the user wants to play with words of length -42 or 137, since no English words are that long, you should reprompt her.

2. Prompt the user for a number of guesses, which must be an integer greater than zero. Don't worry about unusually large numbers of guesses – after all, having more than 26 guesses isclearly not going to help your opponent!

3. Prompt the user for whether she wants to have a running total of the number of words remaining in the word list. This completely ruins the illusion of a fair game that you'll be cultivating, but it's quite useful for testing (and grading!)

4. Play a game of Hangman using the Evil Hangman algorithm, as described below:

	 a. Select the Vector of all words in the English language whose length matches the input length.

	 b. Print out how many guesses the user has remaining, along with any letters the player has guessed and the current blanked-out version of the word. If the user chose earlier to see the number of words remaining, print that out too.

	 c. Prompt the user for a single letter guess, re-prompting until the user enters a letter that she hasn't guessed yet. Make sure that the input is exactly one character long and that it's a letter of the alphabet.

	 d. Partition the words in the dictionary into groups by word family. The word family is the “key” in the AssociativeArray, and the words (already contained in MyStrings from having been read into the Vector of Vectors of MyStrings initially), are added to the Vector in the AssociativeArray which is associated with the given “key” word family.

	 e. Find the most common “word family” in the remaining words, remove all words from the word list that aren't in that family, and report the position of the letters (if any) to the user. If the word family doesn't contain any copies of the letter, subtract a remaining guess from the user.

	 f. If the player has run out of guesses, pick a word from the word list and display it as the word that the computer initially “chose.”

	 g. If the player correctly guesses the word, congratulate her.

5. Ask if the user wants to play again and loop accordingly.

