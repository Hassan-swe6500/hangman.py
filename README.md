# hangman.py
guess the laters and complete the words


import random

# 5 predefined words (list)
words = ["python", "program", "keyboard", "computer", "internet"]

# Random word choose karo
secret_word = random.choice(words)

guessed_letters = []      # ab tak guess kiye hue letters
incorrect_guesses = 0     # galat guesses ki ginti
max_incorrect = 6         # sirf 6 galat guesses allowed

print("=== Welcome to Hangman! ===")
print("I am thinking of a word with", len(secret_word), "letters.")

while incorrect_guesses < max_incorrect:
    # Word display: guess kiye hue letters dikhao, baqi ke liye _
    display = ""
    for letter in secret_word:
        if letter in guessed_letters:
            display += letter + " "
        else:
            display += "_ "

    print("\nWord:", display)
    print("Incorrect guesses left:", max_incorrect - incorrect_guesses)
    if len(guessed_letters) == 0:
        print("Guessed letters: None")
    else:
        print("Guessed letters:", ", ".join(guessed_letters))

    # Win check: agar koi underscore nahi bacha
    if "_" not in display:
        print("\nCongratulations! You won! The word was '" + secret_word + "'.")
        break

    guess = input("Guess a letter: ").lower()

    # Input validation
    if len(guess) != 1 or not guess.isalpha():
        print("Please enter a single letter (a-z).")
    elif guess in guessed_letters:
        print("You already guessed '" + guess + "'. Try another letter.")
    else:
        guessed_letters.append(guess)
        if guess in secret_word:
            print("Good job! '" + guess + "' is in the word.")
        else:
            print("Oops! '" + guess + "' is not in the word.")
            incorrect_guesses += 1
else:
    # Ye tab chalta hai jab loop bina break ke khatam ho (guesses khatam)
    print("\nGame Over! You ran out of guesses. The word was '" + secret_word + "'.")
