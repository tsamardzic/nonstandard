Tanja Samardžić,  Tutorial at the Mexican NLP Summer School, 2 June 2021

# Language (de)standardisation and NLP 

The term non-standard language covers all linguistic expressions not conforming to an official orthography and pronunciation. Such expressions include dialects (written and spoken), historical texts and social media posts. They require special processing techniques in order to deal with the fact that the same word can be written (or pronounced) very differently in the same text (or recording). This tutorial provides an introduction to the notion of language standard and an overview of the challenges that increasingly non-standard writing and speech pose to NLP. 

Learning objectives for you: 

- Big picture: know how to think about the problems
- Know where to look for solutions, data, code, new ideas, code  

<br>

---
### 1. What is standard language? 


<img src="figures/haugen.png" alt="conic" width="600"/>


Source: 

- Einar Haugen (1966), [Dialect, Language, Nation](https://anthrosource.onlinelibrary.wiley.com/share/VHDXIIS4K43WSXKETNBW?target=10.1525/aa.1966.68.4.02a00040), American Anthropologist. 


Popular misconceptions: 

- "Standard is cultivated by suppressing non standard"  <br>
WRONG! Humans are capable and should be encouraged to to master multiple varieties 


-  "Non-standard is dangerous" <br>
WRONG! The danger is only in the totalitarian mind  

<br>

But who determines what spelling is correct? This is a complicated matter that turns out to be political. While there is a need for fully unified spelling in some context, imposing the same spelling on all speakers    

<br>

---
### 2. Good and bad sides of language standardisation


<a href="https://youtu.be/fS4X1JfX6_Q"><img src="figures/oknotok-video.png" alt="oknotok" width="570"/></a>a>

Source: 

-  Gretchen McCulloch   [Resources](https://gretchenmcculloch.com/resources/)

<br>


<img src="figures/norm-procontra.png" alt="conic" width="400"/>

<br>

|         | Standard |  Non-standard |
|:--------|:----------|:---------------| 
| __Good__  | <ul> <li >Broader unity </li> <li>Clarity</li><li>Easy to process</li> </ul> | <ul><li>Expressiveness</li></li>  <li>Fun </li> <li>Local identity</li> </ul> |  
| __Bad__   |<ul> <li>Pressure on minorities</li> <li>Flatness</li> <li>Hard to maintain</li></ul>  | <ul> <li>Hard to process</li><li>Hard to process!!</li><li>Hard to process!!!</li></ul>| 

<br>

___

BREAK

--- 

<br>

### 3. Time, space, society


<img src="figures/conic.png" alt="conic" width="700"/>

Cones borrowed from an [Introduction to Conic Sections](https://www.ck12.org/section/introduction-to-conic-sections/)

<br> 

---

### 4. Non-standard language and NLP





<br> 

#### Spelling correction

> "The disruptive Bell Atlantic and Pacific Bell telephone network outages that occurred during the summer of 1991 were due in part to a __typographical error__ in a software patch."

Source: 
- Karen Kukich (1992), [Techniques for automatically correcting words in text
Share on](https://doi.org/10.1145/146370.146380)

This is an extreme case illustrating well the context where __correct spelling__ is extremely important. The first language processing algorithms started being developed at the point when language standardisation was at its peak (in those few languages that did go through the process of standardisation).  This is how the idea of single "correct" spelling became an inherent part of language technology far beyond programming. Until recently, "correct" spelling was necessary in order to use computers at all, to perform internet searches, for instance, or dictionary look-up. 

Traditional methods for spelling correction rely on large dictionaries. Ideally, such dictionaries would list all correct words in a language, and then we just need to have efficient algorithms to search these dictionaries. The problem with this approach is that it is not possible to list all correct words of a language since such a set would be __infinite__ even in a perfectly standardised language. Thinking that the set of words is finite is one of the biggest illusions about language. This quote by the famous lexicographer Patrick Hanks provides some ideas of why one can never make a complete list of all words:

> Should _strobilus_, _strobila_, _strobilation_ be entries [in a dictionary]?  [...]  Native-speaker dictionary users expect the inventory of words in a dictionary to be complete, and the lexicographer must find ways of satisfying that expectation, despite the fact that the goal is impossible: the lexicon of a living language is dynamic and the boundaries of its vocabulary are fuzzy, so that new words and expressions are being coined — invented or borrowed — all the time.

Source:

- Patrick Hanks (2010), [Compiling a Monolingual
Dictionary for Native Speakers](http://www.patrickhanks.com/uploads/5/1/4/9/5149363/compiling_a_monoligual_dictionary.pdf) 

Despite these limitations, the long tradition of spelling correction provides some useful help. A rather popular project that helped many people get their spelling right is:

- [GNU Aspell](http://aspell.net)

I myself use spelling correction a lot, including writing this tutorial. Strangely enough, I feel strongly bothered by spelling errors and try to avoid them by all means. As imperfect as it is, automatic correction still makes up for my lacking memory. How about you?

<br> 

#### Normalisation

Spelling correction can be seen as a specific case of a broader field of text __normalisation__. Even if there is no right spelling in some language (it has not undergone standardisation at all) and if we don't care whether something is written "correctly", we want to map all variants of a single word to a single meaning. 

Although we will find it quite impossible to explain why and how, we humans have no problems figuring out that `so` and `sooo` are slightly different variants of the same word while `so` and `soap` are entirely different words. Because we don't know how we do this, making computers figure this out for us is very difficult. It involves a lot of surprises and hidden problems that have been a long-lasting topic of research. This article contains a fairly complete list of literature on this problem:


##### Swiss German Example  


Here we focus on Swiss German WhatsApp data as a good example of why normalisation is needed even when there is no single correct writing. 


<img src="figures/weil.png" alt="wiel" width="600"/>


##### Overview of NLP approaches to normalisation



- Devopedia, [Text normalisation](https://devopedia.org/text-normalization) 
- Tim Baldwin 

My overview:


| General framework | General technology | How it works | Pros | Contras |
|:-----------|:-----------|:-----------|:-----------|:-----------|
|   |   |   |   |   | 
| Rule-based | Finite state transducers, e.g. [xfst](https://web.stanford.edu/~laurik/fsmbook/home.html), [hfst](http://hfst.github.io), [OpenFst](http://www.openfst.org/twiki/bin/view/FST/WebHome)  | You write a large set of rules using the exact formalism required by the software, the software reads your rules and applies them to transform any given input| No need for training data, your knowledge is enough| You quickly understand how little you know, rules get complicated with small coverage poor, needs to be manually updated |  
|   |   |   |   |   | 
|Statistical machine translation with IBM models (cSMT)| [Moses toolkit](http://www.statmt.org/moses/?n=Moses.Baseline)   |  Like machine translation, just that we "translate" characters instead of words | You can train a model on your laptop, works better for this task than for actual translation | You need training data e.g. our [Swiss German WhatsApp](https://drive.switch.ch/index.php/s/chlu1xuLzfQ0kBi)|
|   |   |   |   |   |
|Neural transducers with LSTMs | There are many, e.g. [Hard attention transducer](https://github.com/roeeaharoni/morphological-reinflection) by Aharoni , [Multilevel approach](https://github.com/tatyana-ruzsics/uzh-corpuslab-normalization) by Ruzsics, check the last section for more | Similar as with cSMT, but quickly gets too much for your laptop | More flexible than cSMT, more opportunities for improvements  | Needs more data and computation, hard to see big improvements |
|  |   |   |   |   |
|Neural translation with Transformers |  There are many, e.g. [ G2P toolkit]( https://github.com/cmusphinx/g2p-seq2seq)  | Similar as above, just that you need to mimic the grapheme representation on the target side  | Works considerably better  than other systems | Needs GPUs and generally more recent technology |


---

BREAK

---

<br>

### 5. Language standard in text generation


<br>

---
### 6. Relevant NLP workshops


- VarDial
- WNUT
- SIGMORPHON

---

Q&A, DISCUSSION

___