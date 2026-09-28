# Clojure Warrior

Your task is to write a bot to fight through a dungeon (a Clojure remake of RubyWarrior). Each turn your function will receive what the warrior perceives and must return an action: walk, attack, rest (and others). Early levels can be solved with a simple `cond`, but that won't be enough to reach the top. The real game is managing your code complexity as the rules pile up.

## Set Up

- `git clone https://github.com/clojure-camp/clojure-warrior-ui.git`
- `npm install`
- `npm start`
- open https://localhost:8080
- open in your editor of choice and connect the REPL (shadow-cljs, `:app` build)
- edit `src/warrior/bot.cljs` to have it hot-reload

See the [README](https://github.com/clojure-camp/clojure-warrior-ui) if you run into issues.

If all else fails, you can [use the web version](https://warrior.clojure.camp/).


## First Steps

- investigate [what the different functions do](https://github.com/clojure-camp/clojure-warrior-ui#the-board)
- start by writing the simplest code that beats a level
- refactor as needed
- get to the top!


## Extensions

Choose one or more of these, based on your interests:

- *Go for Perfect* - Your performance on each level is graded. Try to get each level to 'S' tier.

- *Try a Completely Different Approach* - You've made it to the top, but can you do it again, in a completely different way? Here are some ideas:

    - *One Big Cond* - it's simple, and gets the job done. But how easy is it to understand and modify?
    - *Sense, then decide* - Compute a set of situations that describes the current state, for example `#{:low-health, :taking-damage, :near-captive}`, then define and use a data-structure mapping a set-of-situations to an action.
    - *State Machine* - Give your bot explicit modes: `:explore`, `:fight`, `:retreat`, etc. Store the mode in an atom. Each mode would then have its own small decision function and a rule for when to change modes.
    - *Hand-Rolled Neural Net* - Decide on some input features (ex. `taking-damage?`, `low-health?`) and for each action compute a score as a dot product of weights and features. Hand tune the weights.

  When you've done it again, take an opportunity to reflect on the pros-and-cons of each approach. Which is a better fit for Clojure? Which was easier to iterate on?

## Super Stretch

Done everything else? Take this on:

- *Train a Neural Net* - Start with 0-layer net of random weights (as described above). Come up with a fitness function. Wire it up with [the underlying bot library](https://github.com/clojure-camp/clojure-warrior). Perturb the weights and keep them if they result in better fitness. Run the optimization for a few thousand cycles.


