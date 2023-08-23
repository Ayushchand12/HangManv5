# PlasticHangMan
import random

def draw_hangman(attempts):
    hangman_graphics = [
        """
          _______
         |       |
         |
         |
         |
         |
        _|_
        """,
        """
          _______
         |       |
         |       O
         |
         |
         |
        _|_
        """,
        """
          _______
         |       |
         |       O
         |       |
         |
         |
        _|_
        """,
        """
          _______
         |       |
         |       O
         |      /|
         |
         |
        _|_
        """,
        """
          _______
         |       |
         |       O
         |      /|\\
         |
         |
        _|_
        """,
        """
          _______
         |       |
         |       O
         |      /|\\
         |      /
         |
        _|_
        """,
        """
          _______
         |       |
         |       O
         |      /|\\
         |      / \\
         |
        _|_
        """
    ]
    if attempts < len(hangman_graphics):
        print(hangman_graphics[attempts])
    else:
        print(hangman_graphics[-1])

def hangman_game():
    words_list = [
        ["plastic", "pollution", "ocean", "marine", "environment", "waste"],
        ["turtle", "bottle", "fish", "trash", "seabird", "bag"],
        ["recycle", "cleanup", "microplastics", "coral", "straw", "wave"],
        ["conservation", "biodegradable", "ecosystem", "jellyfish", "net", "current"]
    ]

    total_rounds = len(words_list)
    current_round = 1
    total_score = 0

    print("Welcome to the Plastic Pollution Hangman Game!")
    print("You will play a total of", total_rounds, "rounds.")
    
    while current_round <= total_rounds:
        print("\nRound", current_round, "- Guess the word related to plastic pollution in the oceans.")
        word_to_guess = random.choice(words_list[current_round - 1])
        guessed_letters = []
        attempts_left = 8
        correct_guesses = 0

        while attempts_left > 0 and correct_guesses < len(word_to_guess):
            print("\nWord:", end=" ")
            for letter in word_to_guess:
                if letter in guessed_letters:
                    print(letter, end=" ")
                else:
                    print("_", end=" ")

            guess = input("\nGuess a letter: ").lower()

            if guess in guessed_letters:
                print("You've already guessed that letter.")
                continue

            guessed_letters.append(guess)

            if guess in word_to_guess:
                correct_guesses += word_to_guess.count(guess)
            else:
                attempts_left -= 1
                draw_hangman(8 - attempts_left)

            print("Attempts left:", attempts_left)

        if correct_guesses == len(word_to_guess):
            print("\nCongratulations! You've uncovered the word:", word_to_guess)
            score = correct_guesses * attempts_left
            total_score += score
            print("Your score for this round:", score)
        else:
            print("\nGame over! The word was:", word_to_guess)
            draw_hangman(7)
            score = 0
            print("Your score for this round:", score)

        current_round += 1

        if current_round <= total_rounds:
            play_next_round = input("Do you want to play the next round? (yes/no): ").lower()
            if play_next_round != "yes":
                break

    print("\nThank you for playing! Your total score:", total_score)

hangman_game()
