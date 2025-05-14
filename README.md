# Hangman-Game

##  🕹️ Description : 

A simple terminal based hangman game in Python . Created using AI tools called Warp . It is a terminal based coding ai tool. Try to guess the word letter by letter before the stickman is hanged .

## 🎮 Gameplay

- Guess letters in a secret word
- Limited number of incorrect guesses allowed
- ASCII art of the Hangman updates with each wrong guess


## 📸 Preview

       ------
       |    |
       O    |
      /|\\  |
      / \\  |
            |
    ---------
    
    Word: _ _ _ _ _
    
    Attempts left: 1
    
    Guessed letters: A, E, R, T, M
## 🧑‍💻 Code
```
import random
import os

# List of words for the game
words = [
    'python', 'hangman', 'computer', 'programming', 'keyboard', 
    'developer', 'algorithm', 'variable', 'function', 'string',
    'integer', 'boolean', 'dictionary', 'array', 'loop'
]

# ASCII art for hangman states
hangman_states = [
    '''
       -----
       |   |
           |
           |
           |
           |
    -------
    ''',
    '''
       -----
       |   |
       O   |
           |
           |
           |
    -------
    ''',
    '''
       -----
       |   |
       O   |
       |   |
           |
           |
    -------
    ''',
    '''
       -----
       |   |
       O   |
      /|   |
           |
           |
    -------
    ''',
    '''
       -----
       |   |
       O   |
      /|\\  |
           |
           |
    -------
    ''',
    '''
       -----
       |   |
       O   |
      /|\\  |
      /    |
           |
    -------
    ''',
    '''
       -----
       |   |
       O   |
      /|\\  |
      / \\  |
           |
    -------
    '''
]

def clear_screen():
    """Clear the terminal screen."""
    os.system('cls' if os.name == 'nt' else 'clear')

def select_random_word():
    """Select a random word from the word list."""
    return random.choice(words).upper()

def display_game_state(word, guessed_letters, attempts):
    """Display the current state of the game."""
    clear_screen()
    
    # Display hangman
    print(hangman_states[attempts])
    
    # Display the word with underscores for unguessed letters
    word_display = ''
    for letter in word:
        if letter in guessed_letters:
            word_display += letter + ' '
        else:
            word_display += '_ '
    
    print(f"Word: {word_display}")
    print(f"Attempts left: {6 - attempts}")
    
    # Display guessed letters
    print(f"Guessed letters: {', '.join(sorted(guessed_letters))}")

def is_word_guessed(word, guessed_letters):
    """Check if all letters in the word have been guessed."""
    for letter in word:
        if letter not in guessed_letters:
            return False
    return True

def play_hangman():
    """Main game function."""
    print("Welcome to Hangman!")
    
    word_to_guess = select_random_word()
    guessed_letters = set()
    attempts = 0
    
    while attempts < 6:
        display_game_state(word_to_guess, guessed_letters, attempts)
        
        # Get user input
        guess = input("Guess a letter: ").upper()
        
        # Validate input
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single letter.")
            input("Press Enter to continue...")
            continue
        
        # Check if letter was already guessed
        if guess in guessed_letters:
            print(f"You already guessed '{guess}'. Try again.")
            input("Press Enter to continue...")
            continue
        
        # Add the guessed letter to the set
        guessed_letters.add(guess)
        
        # Check if the guessed letter is in the word
        if guess not in word_to_guess:
            attempts += 1
            print(f"'{guess}' is not in the word.")
            input("Press Enter to continue...")
        
        # Check if the player has won
        if is_word_guessed(word_to_guess, guessed_letters):
            display_game_state(word_to_guess, guessed_letters, attempts)
            print(f"Congratulations! You guessed the word: {word_to_guess}")
            break
    
    # If the player has used all attempts
    if attempts >= 6:
        display_game_state(word_to_guess, guessed_letters, attempts)
        print(f"Game Over! The word was: {word_to_guess}")

# Start the game if the script is run directly
if __name__ == "__main__":
    while True:
        play_hangman()
        play_again = input("Do you want to play again? (y/n): ").lower()
        if play_again != 'y':
            break
    
    print("Thanks for playing Hangman!")


```
## Screenshots

![image](https://github.com/user-attachments/assets/5d29109d-5484-429c-8d6f-8e121709719e)


