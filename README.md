# openGloss
A linked data standard for representing navigable language glosses.

## Quick Introduction
**Glossed reading** is the practice of reading text while looking up everything that is unfamiliar or needs refreshment during the reading process. For centuries, language learners have produced and shared "glossed texts" to accelerate the deep reading of difficult texts in unfamiliar languages. In this context, a "gloss" is the condensed, contextually attentuated report of all supplementary information necessary to understand a sentence of foreign-language text. In paper books, the gloss is often interlinear or on a facing page, and includes information such as the definition of words, their part of speech, etymologies, usage information, additional example sentences, and grammatical explanation.

openGloss provides a standard serialisation and graph representation of language glosses, so that a new generation of open software can be produced to serve the diverse needs of language students and textual scholars. Tools such as project perseus, fluentU, and other commercial and semi-open projects provide decent interfaces and infrastructure for supporting "glossed reading", but their software systems are monolithic and their data is not available in a form appropriate for quickly building new, custom interfaces.

## Introduction
When it comes to the literacy side of language acquisition, there comes a cusp in the learning curve, after learning grammar, verb tables, and common expressions, when the fastest way to make further progress is to read and watch and listen a great deal. Unfortunately, reading, watching, and listening will only expand vocabulary and deepend one's listening comprehension and sense of the language's rhythm if the input is comprehensible. In general, this is not the case, because real writing introduces words as necessary to express a thought, and not in the order in which the learner can infer their meaning from prior context. In practice, making text and audio and video comprehensible requires thousands of time-consuming, manual reference lookups which could (and SHALL!) be completed automatically by software. It is common for the uninitiated to assume this lookup cost isn't important, or too small to justify addressing, but let's look at an example.

Take the following lines of text from the first chapter of "El Principito" (the Spanish translation of Antoine de St. Exupery's "Le Petit Prince"):

>Cuando yo tenía seis años vi en un libro sobre la selva virgen que se titulaba "Historias vividas",
una magnífica lámina. Representaba una serpiente boa que se tragaba a una fiera.

As a reader of spanish as a foreign language, I might know most of these words, but if I don't remember whether _tenía_ is preterite or imperfect, I will have to invoke another resource, such as a verb conjugation website or paper grammar book, to then review the inflections of _tener_. This will have an overhead cost of breaking the reader's attention and consuming 10-40 seconds of time (at the _very least_). If the reader must do this several times per paragraph of text, they will make very little progress deepening their language knowledge, and instead spend roughly half of their precious study time shuffling paper, clicking badly-designed interface elements, and waiting for webpages to load. The non-context-specific nature of legacy reference materials introduces a high risk of distraction from the primary task (especially the web browser).

A suite of custom-designed tools for glossed reading would solve this problem, but it is currently very difficult to build such tools because of a lack of quality data and standards for representing navigable glosses. Without a community project and standards to support it, dictionaries, frequency-lists, and supplementary resources cannot interoperate, and work is duplicated unnecessarily. All the necessary data for such a suite of tools exists, spread across wikipedia, wiktionary, forvo, wordreference, spanishDict, Linguee, and countless academic websites, but without a way to represent the relationship of canonical reference material to the exact context of reading means that tools to create glossed texts must always be written from the ground-up, and must be slow due to network calls. Otherwise, they may exist in a legal gray area because of unclear license agreements with major reference systems.  

This atrocious lack of open data for language learners and students of history and literature is unacceptable, and a first step toward rectifying the situation is providing a set of patterns for representing such data where it is most useful: the seam between a reference pool and a number of custom interfaces. 

## Use Cases
### Studying Subtitles in VLC
It should be possible to supplement subtitles with glosses, and navigate them with a plugin. This should be a community effort, but it is currently not possible to build such a thing in an acceptable manner because of a the lack of a shared representation scheme for these glosses. The video usecase requires fundamentally different software from reading a text, but the underlying data that must be traversed by the viewer's attention is the same. FluentU provides a commercial example of such software for video, but it is not possible for a community or individual to use the software to study content of their own choosing. 
### Reading Project Gutenberg Texts in their Original Language
Project Gutenberg provides an inexhaustible library of the highest quality written works in many languages, for free. But integrating materials such as wordreference, forvo, and example sentence archives is fraught with copyright problems and, again, would be difficult to achieve in a community because of a lack of standards for representing the relationship between reference materials 
### Custom Children's Books on Mobile Devices
Lighter-weight software for more casual use could easily be created over the same datasets
## Technical Details
### Serialisation
OpenGloss graphs are distributed as JSON-LD serialisations with the `type` `gloss`. If they are accessed on a static file system, they are saved with the file extension `.ogloss`. OpenGloss graphs are serialised as an adjacency list, and graphs are recontructed as necessary by the consuming software. 
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
Occasionally, it is necessary to provide a wider view of an aspect of a passage encompassing multiple disparate phrases, such as the use of a subjective inflection based on a previous clause, or of instances of shaded bracketing negation ("ne... pas, ne... point, ne... jamais) in French. As another example, at times an entire paragraph will be in the future tense for a specific reason. These "points of interest" should be available in a layer of information parallel to the other, more granular gloss patterns.
### Points of Cultural Interest
Occasionally, words, idioms, or syntactical conventions such as poetic forms or songs require more protracted information. This can simply be a paragraph or links to other resources (video, etc.). 
### Navigational Structure
All particles of the gloss must be connected to one another in a navigational structure so that there is always a "next", "previous", "deeper", "shallower", "pivot", and "branch" operation such as could be traversed eyes-free (with no visible interface elements such as buttons, links, or sliders, whatsoever) with a game controller or other eyes-free hardware device. A mouse must be completely unnecessary to navigate the content. Thus, the gloss must include this connective information in a graph or multiply-linked list. This aspect will be expanded upon elsewhere. 

## Other Criteria
### Data is Present Without Network Calls
Computers have very large storage devices, and we should be using them. Just as it is unacceptable to listen to music over a bad network connection, it is unacceptable to wait for multiple network requests when in the flow of reading. A study session is finite, and unfolds in a predictable sequence, so the user should _never_ wait for _a single_ network call during their session. Text is extremely efficiently stored in a computer, and _all_ data required during a study session should be _immediately_ displayed when requested, to avoid violating the user's precious flow of attention.
### Graph Segmentation
It must be possible to recycle and include segments of the graph of glosses in other glosses. This requires nearly all node types to be computationally dereferenceable.
### Open to Addition
It must be possible to add to glosses without the author's permission. Thus, additional layers must address nodes of an existing gloss and be able to be fused with it at runtime for a seamless experience.
## Technical Implementation
### Representation of Whole Texts
A "glossed text" begins with a `text`. A bounded segment of a text for which the user may want a gloss will be called a `focus`. To support the broadest range of possible glosses, any kind of text must be tokenisable. However, the most established way to tokenise texts is using the TEI "standard". Ideally, in TEI, any bounded text segment (whether it be a "word", multiple words comprising a "phrase", or even single syllables or single characters, can be wrapped in xml tags and given an `id`. This id is the anchor of the entire system, and a deep problem with the web in general, which accounts for it being entirely unannotatable, is the lack of ability for users to address arbitrarily granular segments of documents in a standard way. This being the case, for the sake of open glosses, a `text` is a stored file of any description with a given absolute hash. The absolute hash ensures that a tokenisation scheme can reliably address pieces of the text using character offsets.  
For example, there are millions of books on Internet Archive and Project Gutenberg that require glosses, and none of them are available in TEI format with all the necessary tokens already identified. And even if they were available in this format, users would need the ability to augment these at will in their own contexts of use. If, for example, I wish to tokenise _Nieblas_ by Unamuno into a set of `foci` to gloss, Project Gutenberg has a plain text version and an HTML version. I can gloss either of these as long as I know it is stable. Therefore, whatever encoding is used for a text, a community can use this standard to collaboratively gloss it. In this way, the frozen version of the text serves as a kind of coordinate system whose character offsets provide the addressing axis.
### The Gloss Container
The `gloss-container` wraps all the aspects of the gloss together as a single object. This is the dereferenceable, static serialisation of the gloss for an entire text. It looks like the following:
``` javascript
{
  id: "238293jf928fj93jf029fj209fj",
  text_id: "8923h4cf92jr392mx934m489rm284tuxm90",
  type: "gloss_container",
  foci: [
    { 
      //... See below.
    },
    {
      //...
    },
    { 
      //...
    },
    {
      //...
    },  
    //...
  ],
  glosses: [
    {
      //... See below.
    },
    {
      //...
    },
    //...
  ],
  focus_tree: [
    //... more on this below.
  ]
}
```
Note that there are no URLs. IDs are the hashes of the content. This ensures that glosses may be shared on permanent web systems such as IPFS and DAT.

Yes, this does mean that there could be a long-form article's worth of text for more than every word in the original text. This is natural, desireable, and feasible because computers have lots of memory and should use it.
### Attentive Tokenisation (`foci`)
The user's attention must fixate on several kinds of text phenomena that need be glossed. For the purposes of language learning glosses, the two main categories of `focus` are `expression`s, and `scaffold`s.
#### Expression
An `Expression` is a contiguous set of characters with no spaces that stands on its own as a semantic unit. An `expression` `focus` appears in the `foci` array and looks like this:
``` javascript
//...
foci: [
  {
    id: "ansd9f8s9d8fj0sdjf0asdjf0sajd0fj9asdf09asjdf",
    type: "focus",
    focus_type: "expression"
    chars: "perrito",
    target_interval: [341, 348]
  }
]
//...
```
#### Scaffold
An `Scaffold` is any non-contiguous set of expressions that together comprise a semantic or functional unit. A scaffold's `focus` appears in the `foci` array and looks like this:
``` javascript
//...
foci: [
  //...,
  {
    id: "ansd9f8s9d8fj0sdjf0asdjf0sajd0fj9asdf09asjdf",
    type: "focus",
    focus_type: "scaffold"
    target_foci: ["hnqw9c84fnw9874ynq87hg9", "jnfc948nt9qn4g8424cq4"]
  },
  //...
]
//...
```
### Glosses
The `glosses` array of the `gloss_container` lists the `glosses` that target various `foci` in the text. `gloss`es are complex, and come is several flavours depending on the type of the `focus` they gloss. We will first cover a fairly full example, and then consider smaller details and variations.
``` javascript
//...
glosses: [
  //...,
  {
    id: "ansd9f8s9d8fj0sdjf0asdjf0sajd0fj9asdf09asjdf",
    type: "gloss",
    target_foci: ["hnqw9c84fnw9874ynq87hg9", "jnfc948nt9qn4g8424cq4"]
  },
  //...
]
//...
```
#### Level 1
A level 1, single-word or single-expression gloss 
## The Focus Tree
The focus tree construct defines the _navigable structure_ of the text. That is, **there will always be a well-defined "next", "previous", "up", "down", "in", and "out" operation**. There can also be branches and cross-linkages in the tree, which could more properly be called (and will be represented as) a graph. We call it a tree because the final feeling of using the graph should be that of navigating a tree, digressions from which should be experienced by the user as incidental, contained, well-defined, and avoidable.
