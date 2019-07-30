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
### Reading Project Gutenberg Texts in their Original Language
### Custom Children's Books on Mobile Devices

## Major Patterns
### Word Gloss
### Phrase Gloss
### Word Report
### Etymology
### Word pronunciation
### Sentence Pronunciation
### Part of Speech Gloss
### Grammatical Supplement
### Navigation Structure
