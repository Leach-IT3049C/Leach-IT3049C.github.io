---
layout: default
title: 6. Hangman
parent: Assignments and Labs
published: true
nav_order: 6
---
# 4. Hangman
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Lab Goals
1. Build a web-based game (Hangman) that utilizes a variety of concepts and technologies.
2. Demonstrate ability to make network HTTP Requests using Fetch API.
3. Demonstrate ability to create graphics using Canvas.
4. Demonstrate ability to create forms to and handleing user input.
5. Demonstrate understanding of event-oriented programming.


## Instructions
For this assignment you will be building Hangman. Your goal is to build this game using HTML, CSS, JavaScript, and the concepts/techniques covered to-date to build the game completely. 

### Game process
The process of the game should be:
1. Allow the user to specify the difficulty:
    1. `easy` - for words of length 3-5
    2. `medium` - for words of length 6-9
    3. `hard` - for worfs of length 10-15
2. On difficulty selection, we'll make a HTTP Request to [https://hangman-micro-service-bpblrjerwh.now.sh/](https://hangman-micro-service-bpblrjerwh.now.sh/) to get a word for the game.
    1. You'll need to specifify the difficulty in the querystring of your url.
        * [https://hangman-micro-service-bpblrjerwh.now.sh/?difficulty=easy](https://hangman-micro-service-bpblrjerwh.now.sh/?difficulty=easy)
        * [https://hangman-micro-service-bpblrjerwh.now.sh/?difficulty=medium](https://hangman-micro-service-bpblrjerwh.now.sh/?difficulty=medium)
        * [https://hangman-micro-service-bpblrjerwh.now.sh/?difficulty=hard](https://hangman-micro-service-bpblrjerwh.now.sh/?difficulty=hard)
    2. **Hint**: Don’t hardcode all three URLs. Instead, use string templating to populate the querystring.
    3. It may take a few seconds to load initially.
3. Show the word's length as underscores in place of letters which have not yet been guessed.
    * for the word `BOOK` where the Letters `O`, and `K` have been guessed, this would look like `_ O O K `
4. Show a display/paragraph/span containing previously guessed letters to the user
    * `Previously Guessed: C, E, N, L`
5. Show a display/Canvas drawing of the “Hangman”
    a. use canvas API for the hangman drawing
6. Allow user to input a letter to guess. with the following form validations.
    * Alert the user if they enter a letter they have already guessed
    * Alert the user if the provided input wasn't a letter
    * Alert the user if they hit the submit without providing any input (length == 0)
    * Alert the user if they provided more than one character.
5. If the guessed letter is correct, show it in the proper place for the word display (the underscored placeholder)
    a. check if the word has completely been guessed and announce winner if so.
6. If the guessed letter is incorrect, draw the next body part on the hangman (whatever orderand number of lines/body parts you wish)
    a. check if all the body parts have been drawn to announce the game as lost.
7. When the game is over, alert the user if they won or lost and give an option to reset the game
8. For **1 Extra Credit point**, use tha animate.css library to animate the Hangman Title.

### Starter Files
```
.
├── resources
│   ├── css
│   │   └── styles.css                <== Your additional styles
│   ├── js
│   │   ├── Hangman.js                <== Hangman Game Logic
│   │   └── index.js                  <== DOM Manipulation and Event Listeners
│   └── vendor                        <== External Libraries, such as Bootstrap and jQuery
│       ├── bootstrap.min.css
│       ├── bootstrap.min.js
│       ├── fontawesome.min.css
│       ├── jquery-3.5.1.slim.min.js
│       └── popper.min.js
├── index.html                        <== The index.html - Built for you.
└── README.md                         <== Don't Forget the self-reflection evaluation
```

## Tips and Notes
* Remember to review the comments made for you on the code.
* Remember to utilize Git properly and to make frequent commits with meaningful commit messages.
* Remeber to fill out the self-evaluation on the README file.

## Grading
1. The application runs with no errors.
2. The user is presented with 3 difficulties to select from.
3. The application can send HTTP requests passing a difficulty level in the query string and able to parse the response.
4. The application obscures the word with underscores of same length as the original word.
5. The application alerts the user if an already guessed letter was guessed again.
6. The applicatoin draws the hangman (stick man) on wrong guesses.