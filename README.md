# polish-wsd-datasets
Data and code for paper published at ICCS 2022: "A Unified Sense Inventory for 
Word Sense Disambiguation in Polish".

## Task
Word Sense Disambiguation (WSD) task is to assign the appropriate meaning to 
a word for its use in the text context. Thus, this is a standard classification 
problem is a standard classification task where multiple classes are available.

## Data description
The Polish WSD inventory is published in the CCL-XML format. Each text in corpus was split
into chunks containing sentences which are further divided into tokens (`<tok>`) -
a single word or its part. This process was done semi-automatically by our tagger tools.
The tokens underwent an automatic morpho-syntactic 
analysis, after which a selected subgroup of them was manually annotated for WSD.

The disambiguated tokens contain the synset id from Polish WordNet 4.2 (plWN4.2) in the 
prop attribute value. That value should be an integer or a string in case of lemmatization 
or annotation errors (`AUX`). We distinguish four main part of speech: __n__ - noun, __v__ - verb, 
__a__ - adjective and __r__ - adverb.
```
<prop key="sense:wsd_lemma_part-of-speech>plWN4.2_id</prop>
```

Additional property present in data is key `mwe_base`. It is used to assign whole
multi-word expression (MWE) base lemma to its main token (more info about MWE - section below).

An example of a file in corpora:
```xml

<chunkList>
    <chunk id="ch1">
        <sentence id="sent1">
            <tok>
                <orth>Co</orth>
                <lex disamb="1">
                    <base>CO</base>
                    <ctag>subst:sg:nom:n</ctag>
                </lex>
                <lex disamb="1">
                    <base>co</base>
                    <ctag>subst:sg:nom:n</ctag>
                </lex>
                <ann chan="mwe">0</ann>
            </tok>
            <tok>
                <orth>się</orth>
                <lex disamb="1">
                    <base>się</base>
                    <ctag>qub</ctag>
                </lex>
                <ann chan="mwe">1</ann>
            </tok>
            <tok>
                <orth>dzieje</orth>
                <lex disamb="1">
                    <base>dziać</base>
                    <ctag>fin:sg:ter:imperf</ctag>
                </lex>
                <ann chan="mwe">1</ann>
                <prop key="mwe_base">dziać się</prop>
                <prop key="sense:wsd_dziać_się_v">7078144</prop>
            </tok>
            <ns/>
            <tok>
                <orth>?</orth>
                <lex disamb="1">
                    <base>?</base>
                    <ctag>interp</ctag>
                </lex>
                <ann chan="mwe">0</ann>
            </tok>
        </sentence>
        <sentence id="sent2">
            <tok>
                <orth>Pożar</orth>
                <lex disamb="1">
                    <base>pożar</base>
                    <ctag>subst:sg:nom:m3</ctag>
                </lex>
                <prop key="sense:wsd_pożar_n">2119</prop>
            </tok>
            <ns/>
            <tok>
                <orth>?</orth>
                <lex disamb="1">
                    <base>?</base>
                    <ctag>interp</ctag>
                </lex>
            </tok>
        </sentence>
        ...
    </chunk>
</chunkList>
```

### Multi-word expression (MWE)

In the WSD, we often find multi-word expressions that should be treated as a __single sense__, 
e.g. _czerwona kartka_). The development of WSD data built on the basis of plWordNet (_Słowosieć_) 
also includes MWE expressions - mainly of fixed type.
Fixed type means that tokens forming a single MWE occur one after another. 
An exception to this rule are verbs that are joined with token `się`. 


## Corpora

### Składnica
Manually annotated corpus (1 364 files).

### KPWr - N


### KPWr - 100
Manually annotated part of full KPWr corpus (98 files). 

### SPEC
Manually annotated corpus of Sherlock Holmes stories (31 files).

### GLEX
Glosses definitions and usage examples from plWordNet 4.2.

### EmoGLEX

### WikiGLEX
Manually annotated subcorpus of GLOSSEX (1 635 files). Extracted from wordnet examples usage and 
definitions. 


## License
The available code is distributed under the terms of the MIT license. 
All corpora are licensed under CC-BY-SA-4.0.
