# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").

The hints were indeed backwards. For example, entering 25 when the true number was 75 showed "Go LOWER!", and entering 79 showed "Go HIGHER!". The messages should be swapped with each other. The New Game button doesn't work after completing the game. I expect it to clear the history, reset my attempts, and generate a new number to guess, but instead, it does the exact same thing as the Submit Guess. Finally, the Hard difficulty has range 1 to 50, which is smaller than Normal with 1 to 100. I expect Hard to have a bigger range.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

I used Claude Code directly in my terminal. An example of a correct suggestion is fixing the score function so that both the "Too High" and "Too Low" errors deducted the same 5 points instead of erroneously rewarding in one of the cases. I verifed the result quickly since I alredy knew what I would've changed myself, and surely enough, the AI landed on that exact result. One misleading suggestion was adding `st.rerun()` in the `if submit` block. While it fixed thei issue of the attempts and history lagging behind submits by one, it also created another issue, in which the hints would always be disabled until the end of the game. Even though I wasn't able to verify the change and predict this bug before accepting Claude's solution, I caught the bug during test, made follow-up prompts, and had it fixed. 

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I decided that a bug was fixed mainly from observation. I noticed that when I entered a guess higher than the secret, I got the hint "TOO HIGH," and vice versa for a lower guess. I three tests, one checking equality and inequality between the secret and guess. It solidified my personal observations, confirming that my code was robust and free of errors regarding this one functionality. The AI helped fix the tests by ensuring that the tuples got unpacked before checking "Too High", "Too Low", or "Win". More importantly, when I got import errors due to the test file being unable to find the `logic_utils.py` file outside of the `test` folder, Claude added a an empty `conftest.py` at the root to signal to find the required module.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

The secret did not keep changing in the original app. Luckily it was using session state already to ensure it doesn't change across reruns. Session state is a way of persisting data across rerurns, which are basically rerenders of a Streamlit app. Again, the secret number was already stable, but if it weren't, I would've added it to the session state so that it wouldn't change across reruns in the same game. 

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

I would like to reuse my strategy of hunting down bugs from the user's eyes. As a developer sometimes we get lost in the code and forget that encountering bugs from the user's perspective is equally important to diagnosing subtle issues. Next time when I use AI, I would make sure to select the bits I want it to look at and give specific prompts to target the issue without making unnecessary edits that may ripple into other bugs. This project helped me feel more comfortable with AI generated code because despite media stories, it helped me see that code generation in the software industry is often done in a strategic way with only a few slip-ups. This project helped me hone in on the prompting essentials and necessity for verification when working with generative AI.