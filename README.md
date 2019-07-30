# openGloss
A linked data standard for representing navigable language glosses.

## Quick Introduction
**Glossed reading** is the practice of reading text while looking up everything that is unfamiliar or needs refreshment during the reading process. For centuries, language learners have produced and shared "glossed texts" to accelerate the deep reading of difficult texts in unfamiliar languages. In this context, a "gloss" is the condensed, contextually attentuated report of all supplemntary information necessary to understand a sentence of foreign-language text. In paper books, the gloss is often interlinear or on a facing page, and includes information such as the definition of words, their part of speech, etymologies, usage information, additional example sentences, and grammatical explanation.

openGloss provides a standard serialisation and graph representation of language glosses, so that a new generation of open software can be produced to serve the diverse needs of language students and textual scholars. Tools such as project perseus, fluentU, and other commercial and semi-open projects provide decent interfaces and infrastructure for supporting "glossed reading", but their software systems are monolithic and their data is not available in a form appropriate for quickly building new, custom interfaces.

## Introduction
There comes a cusp in the language learning curve, after learning grammar, verb tables, and common expressions, when the fastest way to make further progress is to read and watch and listen a great deal. Unfortunately, reading, watching, and listening will only expand vocabulary and deepend one's listening comprehension and sense of the language's rhythm if the input is comprehensible. Making text and audio and video comprehensible requires thousands of time-consuming, manual reference lookups which would be completed automatically by software.

For example, take the following lines of text from the first chapter of "El Principito" (the Spanish translation of Antoine de St. Exupery's "Le Petit Prince"):

>Cuando yo tenía seis años vi en un libro sobre la selva virgen que se titulaba "Historias vividas",
una magnífica lámina. Representaba una serpiente boa que se tragaba a una fiera.

As a reader of spanish as a foreign language, I might know most of these words, but if I don't remember whether _tenía_ is preterite or imperfect, I will have to invoke another resource, such as a verb conjugation website or paper book, to then review the inflections of _tener_. This will have an overhead cost of breaking the reader's attention and consuming 10-40 seconds of time. If the reader must do this several times per paragraph of text, they will make very little progress depening their language knowledge, and instead spend roughly half of their precious study time shuffling paper, clicking badly-designed interface elements, and waiting for webpages to load. The non-context-specific nature of legacy reference materials introduces a high risk of distraction from the primary task.

A suite of custom-designed tools for glossed reading would solve this problem, but it is currently very difficult to build such tools because of a lack of quality data and standards for representing navigable glosses. Without a community project and standards to support it, dictionaries, frequency-lists, and supplementary resources cannot interoperate, and work is duplicated unnecessarily. All the necessary data for such a suite of tools exists, spread across wikipedia, wiktionary, forvo, wordreference, spanishDict, Linguee, and countless academic websites, but without a way to represent the relationship of canonical reference material to the exact context of reading means that tools to create glossed texts must always be written from the ground-up, and must be slow due to network calls. Otherwise, they may exist in a legal gray area because of unclear license agreements with major reference systems.  

This atrocious lack of open data for language scholars is unacceptable, and a first step toward rectifying the situation is providing a set of patterns for representing such data where it is most useful: the seam between a reference pool and a number of custom interfaces. 

## Use Cases
### Studying Subtitles in VLC
It should be possible to supplement subtitles with glosses, and navigate them with a plugin. This should be a community effort, but it is currently not possible to build such a thing in an acceptable manner because of a the lack of a shared representation scheme for these glosses. The video usecase requires fundamentally different software from reading a text, but the underlying data that must be traversed by the viewer's attention is the same. FluentU provides a commercial example of such software for video, but it is not possible for a community or individual to use the software to study content of their own choosing. 
### Reading Project Gutenberg Texts in their Original Language
Project Gutenberg provides an inexhaustible library of the highest quality written works in many languages, for free. But integrating materials such as wordreference, forvo, and example sentence archives is fraught with copyright problems and, again, would be difficult to achieve in a community because of a lack of standards for representing the relationship between reference materials 
### Custom Children's Books on Mobile Devices
Lighter-weight software for more casual use could easily be created over the same datasets

## Major Patterns
### Word Gloss
A format for reporting on the meaning of a single word, in-context. This is most similar to a typical dictionary entry, but should include a description of how this word is used in the context in which its gloss is invoked.
### Word Report
Supplement and deeper level of word gloss. Would give the word's etymology, synonyms, other appearances in this text and similar texts, usage information, link to or include a part of speech gloss, and give grammatical supplementation _in situ_.
### Phrase Gloss
Similar to a word gloss, but covers a set phrase that may include multiple words. Useful for idioms or grammatically ambiguous but frequently used collections of words.
### Etymology
Etymology should include an account of the word's origins and changing usages over time. Google's etymology tree is not acceptable or useful in almost any context. Etymonline is a better prototype for an etymology format. Examples of usage over time could also be included using project gutenberg and internet archive texts. 
### Word pronunciation
Forvo.com has the data, but it is not easy to link to it in a "pull-based" paradigm due to licensing. FluentU provides an excellent interface for reviewing pronunciations in-context, but their data and software are monolithically fused, unlicensable, and commercially blocked.
### Sentence Pronunciation
Pronunciation of entire sentences can be provided by a community if the data standards existed. It is also possible to extract them from sources such as librivox, but the quality is low and standards would be needed to describe this relationship.
### Part of Speech Gloss
The expert-verified part of speech of every word should be given, with an explanation of how its part of speech can be inferred from its morphology and context. Any necessary grammatical supplment, such as a verb conjugation table, should be given for additional reference.
### Grammatical Supplement
Tables and transformation rules for verbs, inflection tables for nouns, and explanations for how these tables apply in the exact context in which they are invoked should be provided.
### Points of Grammatical Interest
Occasionally, it is necessary to provide a wider view of an aspect of a passage encompassing multiple disparate phrases, such as the use of a subjective inflection based on a previous clause, or of instances of shaded bracketing negation in French. These "points of interest" should be available in a layer of information parallel to the other, more granular gloss patterns.
### Points of Cultural Interest
Occasionally, words, idioms, or syntactical conventions such as poetic forms or songs require more protracted information. This can simply be a paragraph or links to other resources (video, etc.). 
### Navigation Structure
All particles of the gloss must be connected to one another in a navigational structure so that there is always a "next", "previous", "deeper", "shallower", "pivot", and "branch" operation such as could be traversed eyes-free (with no visible interface elements such as buttons, links, or sliders, whatsoever) with a game controller or other eyes-free hardware device. A mouse must be completely unnecessary to navigate the content. Thus, the gloss must include this connective information in a graph or multiply-linked list. This aspect will be expanded upon elsewhere. 
