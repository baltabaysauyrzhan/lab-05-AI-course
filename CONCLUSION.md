# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

The layer that changed results the most was layer 1. Before layer 1, my bare agent got 16 correct, 6 wrong, and 4 no answer. After layer 1, it became 18 correct, 6 wrong, and 4 no answer. It changed what the agent can do because when the tool gave an error like bad region name, layer 1 sent this error back to the model, so the model could fix its mistake and try again. Layer 2 did not change numbers at all (it stayed 18 correct), and layer 3 only changed some wrong answers to no answer because of grounding, but layer 1 actually helped to fix things and get more correct answers.

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

One question that the full harness still gets wrong is q08. When I look at its trace, the model tried to find the lowest monthly wage, but it picked a wrong region from the list because it got confused by the sorting order of the tool output. To fix this, I would add a small check to the harness to verify if the model's chosen region actually matches the extreme value in the tool data. The cost of this would be extra model calls, more tokens, and it could take more time to run every step.

## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

For monthly ranking, I would ship the fixed workflow. From Part 1, the workflow was much faster and cheaper. It used only 3,852 tokens and 15 model calls, while the bare agent used 19,835 tokens and 26 model calls, and the workflow had better accuracy on fixed questions (13/15). However, I would choose the agent if the monthly task changes its structure and becomes an open question where we don't know the parameters in advance.

---

I wrote this file myself, without any AI tool.
