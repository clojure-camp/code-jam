# Mastermind

You will start by implementing the game of Mastermind in the REPL, and then continue by building an interface for it, or work on AIs: one to play as the guesser, and one to play as a 'cheating' adversary.

Mastermind is a classic 2-player game of code-breaking. The 'code-maker' chooses a set of pegs of varying colors (the 'code'). The 'code-breaker' then takes turns guessing a code, getting feedback, and applying their logic skills to figure out the code.

## Set Up

(there's no repo for this one, start fresh!)

## Getting Started

- review the [rules of the game](https://en.wikipedia.org/wiki/Mastermind_(board_game))
- choose a representation for codes and feedback
- write the scoring function: guess + secret → exact/partial counts; test it
  - be extra careful about how you handle duplicaates (ex. secret RRGB, guess RGGG)
- devise functions to play a game via the REPL against a randomly chosen secret

## Extensions

Choose one or more of these, based on your interests:

- have the game playable via the terminal instead of the REPL
  - maybe port to babashka
  - or compile into an executable with graal, jank or jolt
- make peg count and color count parametrizeable
- make the scoring function swappable - allowing for [Bulls-and-Cows](https://en.wikipedia.org/wiki/Bulls_and_Cows) rules or Wordle rules
- *Property Testing* - Use [test.check](https://clojure.org/guides/test_check_beginner) to property test your scoring function.
- *AI Code-Breaker* - Write an algorithm to solve the game. Here are some ideas. [Wikipedia](https://en.wikipedia.org/wiki/Mastermind_(board_game)) lists a few different strategies.

  - Random - The number of solutions for a game with 4 holes and 6 colors is only 1296. You can enumerate all possible solutions, and each turn, pick one randomly (and decrease the list based on feedback).
  - Information Theory - Like Random, but, each turn it picks the guess with the highest Shannon entropy over the feedback partition.
  - Minimax - Compute the game decision tree, make the best minimax choice. Maybe save the tree to a file.
  - Constraint Solving - Use [core.logic](https://github.com/clojure/core.logic) to filter the solution space based on feedback received.
  - Genetic Algorithm - [Wikipedia](https://en.wikipedia.org/wiki/Mastermind_(board_game)#Genetic_algorithm) provides a sketch of an algorithm.
- *Evaluate Your Bots* - If you have multiple implementations of code-makers, evaluate them: simulate games, draw histograms of turns-to-win; compare strategies.
- *'Cheating' Code-Maker* - Instead of picking a random code to start, have the code-maker make up the feedback in an effort to keep the player guessing (but, always giving consistent feedback). This will also probably involve keeping track of all potential solutions that are valid. How many turns does your best Code-Breaker take to beat a random Code-Maker vs the Cheater?

## Super Stretch

Done everything else? Take this on:

- *Web App* - make a web app, playable by two players on separate devices
  - variant: server sets a random code, the players try to guess the fastest
  - variant: server uses the 'cheater' described above, and players try to guess the fastest
  - variant: players each set a code, then take turns making guesses - that reveal feedback on both their codes
