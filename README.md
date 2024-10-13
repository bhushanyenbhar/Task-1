import random

def choose_word():
    words = ["python", "hangman", "programming", "development", "challenge"]
    return random.choice(words)

def display_word(word, guessed_letters):
    return " ".join(letter if letter in guessed_letters else "_" for letter in word)

def hangman():
    word = choose_word()
    guessed_letters = set()
    incorrect_guesses = 0
    max_incorrect_guesses = 6

    print("Welcome to Hangman!")
    
    while incorrect_guesses < max_incorrect_guesses:
        print("\nCurrent word: ", display_word(word, guessed_letters))
        print(f"Incorrect guesses left: {max_incorrect_guesses - incorrect_guesses}")
        
        guess = input("Guess a letter: ").lower()

        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single letter.")
            continue

        if guess in guessed_letters:
            print("You've already guessed that letter. Try again.")
            continue

        guessed_letters.add(guess)

        if guess not in word:
            incorrect_guesses += 1
            print(f"Wrong guess! The letter '{guess}' is not in the word.")
        else:
            print(f"Good guess! The letter '{guess}' is in the word.")

        if all(letter in guessed_letters for letter in word):
            print(f"\nCongratulations! You've guessed the word: {word}")
            break
    else:
        print(f"\nSorry, you've run out of guesses. The word was: {word}")

if __name__ == "__main__":
    hangman()
