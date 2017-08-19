# Learning English and French Grammar with a Recurrent Neural Network

[The python notebook with full source code is on Github](https://github.com/wenqinYe/language_analysis/blob/master/lstm.ipynb)

### Introduction

Language is complicated because different languages have different grammar rules. Forgetting old rules and learning new rules is a challenge new language learners must overcome.

For example, in French the verb comes before the pronoun instead of after like in English. As a result a new French learner will wrongly translate a sentence like “he **asks him** a question” to “il **pose lui** une question” — with verb before the pronoun — when the correct translation is “il **lui pose** une question”.

If a computer is able to model differences between two languages, like French and English, it is then possible to predict mistakes that a second language learner will make. Then further work can be done to make a correction based on the knowledge gained from the research.

The main idea behind this work is to use a recurrent neural network:

- To learn a vector representation of the grammar of two languages
- Use the vector space to find the differences between two languages, namely English and French.

### The Process

The general process is to tag sentences, represent the tags with embeddings and then train the embeddings on a task with a recurrent neural network.

In the preprocessing step a text corpus is split into sentences. The words in each sentence are tagged with a part of speech. Parts of speech are the basic units of grammar making them a natural choice for understanding language.

![img](https://cdn-images-1.medium.com/max/800/1*zQ2jaPwa5uW5jAq8_OPKSw.png)

A sentence converted into POS tags

Each part of speech is represented by a five dimensional vector. A sentence is then represented by a series of these part of speech vectors.

![img](https://cdn-images-1.medium.com/max/800/1*-PZ5B21GLDe5LvLTN-qCCg.png)

The 15 parts of speech tags represented by 15 vectors that are each 5 dimensional

Each sentence’s part of speech vectors are fed into a recurrent neural network sequentially. The objective of the model is to reconstruct the input sequence. This training forces the recurrent neural network to learn the sequential structure of the sentence.

![img](https://cdn-images-1.medium.com/max/800/1*RjOWxb43XhLpnDT0wYEDGw.png)

A sequence to sequence model

The cool part is, even though the part of speech vectors are initially random, during training the optimizer updates them just as it does with the weights. With a proper training task the vector space will reflect the relationships between the part of speech tags. Since grammar consists of a series of relationships between parts of speech, it follows that the vector space will reflect the grammar of the language. By comparing the vector spaces of two languages after training, it is possible to uncover grammatical differences.

#### Analysis

After training the model we visualize the vector spaces using t-SNE.

![img](https://cdn-images-1.medium.com/max/800/1*SfjP56b7Y4Bo6WhEkahMGA.png)

![img](https://cdn-images-1.medium.com/max/800/1*xaErUej9MER9OZcafwMo5A.png)

From a first glance we notice that the vector from VERB → NOUN is the same (after normalizing the distance) in both English and French. This is expected because adverbs in French and English work the same with a few exceptions.

To quantify this idea compute the part of speech discrepancies between English and French and list the top 10:

![img](https://cdn-images-1.medium.com/max/800/1*xkUAy-laOlIH3L5GRFtgkw.png)

As expected the pair (PRON, VERB) pair has the second largest difference. This makes sense because the pronoun-verb order is inverted in French.

Interestingly determiners (DET) appear in half of the top ten differences between English and French. This suggests that the way determiners like “a”, “an”, “his”, “her”, “their” are used in English differ in French in subtle ways. Speaking from first hand experience learning French I can confirm that knowing how to use determiners is hard because they do not agree with English usage.

### Conclusion

My research has only focused on English and French but the ideas here could easily be extended any language pair.

Future improvements to this research include using a more expansive dataset than just two books, and adjusting the vector size and cell sizes of the model to see if it produces different results.

In addition I am not an expert at French and English grammar. Someone who has experience analyzing grammar could interpret the results much better than I can.

But overall, it has been demonstrated that a neural network combined with a vector space is a promising approach to linguistic modelling. The neural network was able to effectively hit on major discrepancies as well as find more subtle ones. In fact, what makes deep learning so great is that it uncovers hidden structure that is hard for humans to articulate and therefore represents a promising direction for future research.

[The python notebook with full source code is on Github](https://github.com/wenqinYe/language_analysis/blob/master/lstm.ipynb)

Thanks for reading, if you liked this give it a clap!