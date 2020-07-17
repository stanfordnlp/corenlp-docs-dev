---
layout: default
title: Overview
keywords: CoreNLP, Java, NLP, Natural Language Processing
type: first_page
permalink: '/index.html'
nav_order: 1
homepage: true
---


<p align="center">
   <img src="assets/images/corenlp-title.png">
</p>

[<i class="fab fa-java"></i> Download CoreNLP 4.0.0](http://nlp.stanford.edu/software/stanford-corenlp-latest.zip){: .btn .fs-5 .mr-2 .mb-md-0 }
[<i class="fab fa-github"></i> CoreNLP on GitHub](https://github.com/stanfordnlp/CoreNLP){: .btn .fs-5 .mr-2 .mb-md-0 }

{: .no_toc }

## About

CoreNLP is your one stop shop for natural language processing in Java! CoreNLP enables users to derive linguistic annotations for text, including token
and sentence boundaries, parts of speech, named entities, numeric and time values, dependency and constituency parses, coreference, sentiment, 
quote attributions, and relations. CoreNLP currently supports 6 languages, including Arabic, Chinese, English, French, German, and Spanish.

### Pipeline

The centerpiece of CoreNLP is the pipeline. Pipelines take in raw text, run a series of NLP annotators on the text, and produce a final
set of annotations.

<p align="center">
   <img src="assets/images/pipeline.png">
</p>

### CoreDocument

Pipelines produce CoreDocuments, data objects that contain all of the annotation information, accessible with a simple API, and serializable
to a Google Protocol Buffer.

<p align="center">
  <img src="assets/images/text-to-annotation.png">
</p> 

## Quickstart

1. Download and unzip [CoreNLP 4.0.0](http://nlp.stanford.edu/software/stanford-corenlp-latest.zip)

1. Download model jars for the language you want to work on and move the jars to the distribution directory.

| Language | model jar | version |
| :------- | :-------- | | :----- |
| Arabic  | [download](http://nlp.stanford.edu/software/stanford-corenlp-4.0.0-models-arabic.jar) | 4.0.0 |
| Chinese | [download](http://nlp.stanford.edu/software/stanford-corenlp-4.0.0-models-chinese.jar) | 4.0.0 |
| English | [download](http://nlp.stanford.edu/software/stanford-corenlp-4.0.0-models-english.jar) | 4.0.0 |
| English (KBP) | [download](http://nlp.stanford.edu/software/stanford-corenlp-4.0.0-models-english-kbp.jar) | 4.0.0 |
| French | [download](http://nlp.stanford.edu/software/stanford-corenlp-4.0.0-models-french.jar) | 4.0.0 |
| German | [download](http://nlp.stanford.edu/software/stanford-corenlp-4.0.0-models-german.jar) | 4.0.0 |
| Spanish | [download](http://nlp.stanford.edu/software/stanford-corenlp-4.0.0-models-spanish.jar) | 4.0.0 |

```bash
mv /path/to/stanford-corenlp-4.0.0-models-french.jar /path/to/stanford-corenlp-4.0.0
```

1. Include the distribution directory in your CLASSPATH.

```bash
export CLASSPATH=$CLASSPATH:/path/to/stanford-corenlp-4.0.0/*:
```

1. You're ready to go! There are many ways to run a CoreNLP pipeline. For instance here's how to run a pipeline on a text file.

```bash
java -Xmx5g edu.stanford.nlp.pipeline.StanfordCoreNLP -file input.txt
```

