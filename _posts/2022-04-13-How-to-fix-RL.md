---
layout: post
title: How to fix reinforcement learning
subtitle: ""
comments: true
cover-img: /assets/img/007/007-3.jpg
thumbnail-img: ""
# share-img: /assets/img/007/007-3.jpg
---

# How to fix reinforcement learning

Author:[Andrey Kurenkov](https://thegradient.pub/author/andrey/)  

This piece is the second in a two-part series, starting with Reinforcement learning’s foundational flaw.



## Why have we not moved beyond pure RL?

You might be thinking something like this:

```
We cannot just move beyond pure RL to emulate human learning — pure RL is rigorously formulated, and our algorithms for training AI agents are proven based on that formulation. Though it might be nice to have a formulation that aligns more closely with how people learn instead of learning-from-scratch, we just don't have one.
```

It’s true that algorithms that incorporate prior knowledge or instructions are by definition more complex than the pure RL ones that have been rigorously formulated over decades. But that last bit is *not* true --- we do in fact have a formulation for learning-not-from-scratch which aligns more closely with how people learn.    
Let’s start by more explicitly describing how human learning is different from pure RL. When starting to learn a new skill, we basically do one of two things: guess at what the instructions might be (recall our prior experience with board games), or read some instructions (check the board game's rules). We generally know the goal and broad approach for a particular skill from the get-go, and we never reverse-engineer these things from a low-level reward signal.  
![](https://www.filepicker.io/api/file/PeqgA7XkSzO0xEOUwc7l?policy=eyJoYW5kbGUiOiJQZXFnQTdYa1N6TzB4RU9Vd2M3bCIsImV4cGlyeSI6MTY0OTg1ODU0NywiY2FsbCI6WyJyZWFkIl19&signature=3993331e07e3f151f527e705da6bf5854d2ace2d674946e997e6ee7f382906d2)

#### Leveraging prior experience and instruction

The ideas of leveraging prior experience and getting instructions have very direct analogues in AI research:  

* **Meta-learning** tackles the problem of **learning how to learn**: making RL agents pick up new skills faster having already learned similar skills. And **learning how to learn**, as we'll see, is just what we need to move beyond pure RL and leverage prior experience.

* **Transfer learning,** roughly speaking, corresponds to 'transferring' skills attained in one problem to another potentially different problem. Here’s Demis Hassabis, CEO of DeepMind, talking about the importance of transfer learning:

  ```
  "I think transfer learning is the key to general intelligence. And I think the key to doing transfer learning will be the acquisition of conceptual knowledge that is abstracted away from perceptual details of where you learned it from." - Demis Hassabis @demishassabis pic.twitter.com/oDQjvx4TLa
  ```

> ![]([https://www.filepicker.io/api/file/9aJiI2KMS2q7PbVKfXmr?policy=eyJoYW5kbGUiOiI5YUppSTJLTVMycTdQYlZLZlhtciIsImV4cGlyeSI6MTY0OTg1ODg3OSwiY2FsbCI6WyJyZWFkIl19&signature=6acac16e9449a921519bface67540120b7e9080f5d85165b31b9589bfa3fbc9c #pic_center)



<img src="../assets/img/:Users:langzi:Documents:GitHub:AnonymousDestroyer.github.io:assets:img:yujin_blog:Screen Shot 2022-04-09 at 5.30.48 AM.png" alt="Screen Shot 2022-04-09 at 5.30.48 AM" style="zoom:50%;" />

```
And I think that [Transfer Learning] is the key to actually general intelligence, and that's the thing we as humans do amazingly well. For example, I played so many board games now, if someone were to teach me a new board game I would not be coming to that fresh anymore, straight away I could apply all these different heuristics that I learned from all these other games to this new one even if I've never seen this one before, and currently machines cannot do that... so I think that's actually one of the big challenges to be tackled towards general AI.
```

* **Zero-shot learning** is similar. It also aims to learn new skills fast, but takes it further by not leveraging **any** attempts at the new skill; the learning agent just receives 'instructions' for the new task, and is supposed to be able to perform well without any experience of the new task.
* **One-shot** and **few-shot** learning are also active areas of research. These fields differ from zero-shot learning in that they use demonstrations of the skill to be learned, or just a few iterations of experience, rather than indirect 'instructions' that do not involve the skill actually being executed.
* **Life Long Learning** and **Self Supervised Learning** are yet more examples of learning, in roughly defined as long-term continuous learning without human guidance.

## Conlusion

# Conclusion

The classic formulation of RL has a fundamental flaw that may limit it from solving any truly complex problems: its implied assumptions of starting from scratch and its heavy dependence on a low-level reward signal or provided environment model. As shown by the many papers cited here, going beyond starting from scratch does not necessitate hand-coded heuristics or rigid rules. Meta-RL methods empower AI agents to learn better through high-level instructions, accumulated experience, examples of what it should learn to do, learning a model of the world, intrinsic motivation, and more.  
Let's end on an optimistic note: the time is ripe for the AI community to embrace work such as the above, and **move beyond pure RL** with more **human-inspired** learning approaches. Based on the **board-game allegory** alone, it seems reasonable to claim that AI techniques must move towards this and away from pure RL in the long term. Work on pure RL should not immediately stop, but it should be seen as useful *insofar as it is complementary to non-pure RL methods* and as long as we remain cognizant of its *inherent limitations*. If nothing else, methods based on meta-learning, zero/few-shot learning, transfer learning, and hybrids of all of these should become the default rather than the exception. And as a researcher about to embark on my PhD, I for one am willing to bet my most precious resource — my time — on it.



Reference form

https://thegradient.pub/how-to-fix-rl/

