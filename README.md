# Games
Files containing Python 3.0 codes that play different games with user.

Hello, and welcome to my Python 3.0 gamepack! This file contains several
classic games I have written myself to build upon and display my Python 
coding skills. Each ".py" file also features a corresponding text file
to view if you do not have Python 3.0 to run the script. The three text
files "babyanimals.txt","states.txt", and "countries.txt" are used by
the Hangman game to draw words from. It is important that these files
are not renamed so the script can find them, and also that they are in
the same folder as the Hangman script. If you'd like to add on words,
simply append them to one of the three text files. Below I have also
included descriptions of the games and a short explanation as to how the
game scripts function. Enjoy!


HANGMAN:
Choose a category and difficulty, and the game will select a secret word
for you to guess the letters of. Be careful though, if you guess a
letter that is not in the word, you get a strike and a part of the
picture is added. Get too many wrong, and the picture will complete and
you lose. If you guess correctly and complete the word, you win!

HOW IT WORKS:
Each image of the Hangman game is contained as eight lines of ASCII 
characters within a unique function found of the beginning of the script.
Each image is then placed sequentially within a list to be called upon
as the game progresses. I placed the images in a list so I can later call
upon them by incrementing the index of this new list because it is
 easier than calling each individual function and there is no reason to 
regress the image. The next block of code imports the lists of words in
external text files. An empty list is instantiated and the script appends
each word in the text file to this list to draw from when it word is chosen.
The three lists are: "states_pool","baby_animals_pool", and "countries_pool".
The next block of code asks for the user to choose a category. It very
simply checks for a match to what the user entered and recognizes a few
variations the user might enter when choosing, such as "states" vs.
"us states". If the user's entry is not recognized, the script will ask
the user again until they enter something it knows. When the player makes
a choice, the script sets that choice equal to a variable called "playlist"
to indicate which list of words will be used for the game. After this,
the game shuffles the chosen list randomly and chooses a word based on
its index, also at random. Some non-essential code pauses the script
and talks to the user to make it seems more playful and then asks the user
to select a difficulty. The diffuclty selection processes works the same
way as the category selection process. This script also contains a hidden
difficulty. The next block generates blank spots for each letter 
of the word. If the script detects a space, it adds a space instead of a
blank spot. The next block of code plays the actual game with the user.
First, a string of all english letters is created. This is so the game 
can run the player's guessed letter against it for a match and keep
track of which letters the user has already tried. If it finds a match,
the letter is replaced in the pool with a space and the game then checks
where, if anywhere, the letter appears in the secret word. The game also
verifies that the entry is a letter, and has a length < 2 (meaning the
user entered exactly 1 letter). If these conditions fail, the user will
be asked to enter a letter until the entry is valid. I also chose to
not have it remove a point if the user guesses a letter twice, but
instead remind them that they have already tried it. After the script
verifies a new single letter was entered, it uses a "for" loop to
look for it in the "game_word". If it finds a match, then it replaces
the corresponding space by its index. If it is wrong, then it subracts
a point from "plyr_lives" and increments the image by one. Next in the
script is a small block of code to handle what happens if a player
already guessed a letter. If you recall, the game checks the player's
guess against a string containing all 26 english letters. It does this
by using a "for" loop, and will stop as soon as it finds a match. The
value of "i" will be whatever the loop ends on. If the loop passes the
letter "z" then it means the player already guessed the letter and it
has been removed from the string. The final value of the alphabet string
is the number 0, which is impossible for the player to guess. If the script
detects that i = 0, then it does not break the loop, and asks the player
to enter another letter. It also does not remove the number unlike other
channels. The next block of code simply verifies if the game is over by
checking the "plyr_lives" variable. And the last block of code offers
to restart the game if the player would wish. The entirety of the code
is within a "while True" loop that only exits when the player selects "no"
at the end of the game.


BLACKJACK:
This card game requires skill as much as it requires luck. Play against
the computer to reach 21 with your cards. Number cards are worth face
value, face cards are 10, and Aces are worth 11 or 1 (the game will
change its value in your favor). The dealer gives you two cards, and
draws two for themself; one card face-up for you to see, the other face
down. you then have the choice to "hit" (draw one more card), or "stay"
(finish drawing cards). The goal is to get as close to 21 without going
over. If you land on 21, you have blackjack and you win. If you go over,
you bust, and lose. Lastly, if you tie with the dealer it is a "push."
When you finish drawing, the dealer reveals their other card and will
continue to draw as long as their hand is 16 or under.

HOW IT WORKS:
This script starts off by establishing two functions that will be
frequently called upon throughout the rest of the script. The first
function seen is "check_score". This function takes in a list (a 
player's hand) and assigns values to the face cards and ace. It then
checks if the hand has gone over 21 and if so, will attempt to change
exactly one ace from 11 to 1 (which actually subtracts 10 from the score).
The script flips a switch so this change will only happen once, even
if the hand has multiple Aces. The second function "draw_card" will add
a card to the hand when called upon. The function takes in the hand,
pops a card from the stack of playing cards, and appends it to the list
(player hand). This function is usually followed by the "check_score"
function to ensure a card is not drawn when it is not possible. The next
block of code creates the deck of cards. It begins by taking a range of
numbers from 1 to 10, and combines it with the letter cards. It then
multiplies the deck four times, and then uses the "random.shuffle"
command to randomize the cards. An empty list is created to hold the
dealer's cards and the draw function is called twice. One card is
revealed to the player, and then the dealer's score is checked.
The next block of code does the same thing for the player. The next
block of code asks the player to hit or stay. The loop will allow the
user draw cards as long as their score is below 21, and is given
instructions to terminate the loop if the player's score is over, or
if they enter "stay." Like all my loops that ask for player entry,
the question is kept inside a "while True" loop until a very
specific input is detected. If the player does bust, the rest of
the code is skipped and the player is asked if they would like to
restart. If they do not bust, then the next block determines if the
dealer needs to draw. The code is the same as when the player is
taking their turn. The only difference is that a card is
automatically drawn as long as the dealer's score is under 16. If
neither the player nor the dealer have busted, then the next block
of code evaluates the winner. Lastly, the player is asked to play
again. If they choose yes, the entire code is whithin a "while True"
loop and it resets. Otherwise, the loop exits and the code ends.

