---
layout: page
title: Tokenization
keywords: tokenize, TokenizerAnnotator, tokenization
permalink: '/tokenize.html'
nav_order: 4
parent: Pipeline
---

## Description

Tokenization is the process of turning text into tokens. For instance the sentence `Marie was born in Paris.` would be tokenized as the list `"Marie", "was", "born", "in", "Paris", "."`.
CoreNLP splits texts into tokens with an elaborate collection of rules.

| Name | Annotator class name | Requirement | Generated Annotation | Description |
| --- | --- | --- | --- | --- |
| tokenize | TokenizerAnnotator | - | TokensAnnotation (list of tokens), and CharacterOffsetBeginAnnotation, CharacterOffsetEndAnnotation, TextAnnotation (for each token) | Tokenizes text |

## Options

| Option name | Type | Default | Description |
| --- | --- | --- | --- |
| tokenize.language | Enum { English, French, German, Spanish, Unspecified, Whitespace } | Unspecified | Use the appropriate tokenizer for the given language. If the tokenizer is Unspecified, it defaults to using the English PTBTokenizer. |
| tokenize.class | class name | null | If non-null, use this class as the `Tokenizer`. In general, you can now more easily do this by specifying a language to the TokenizerAnnotator. |
| tokenize.whitespace | boolean | false | If set to true, separates words only when whitespace is encountered. |
| tokenize.keepeol | boolean | false | If true, end-of-line tokens are kept and used as sentence boundaries with the WhitespaceTokenizer. |
| tokenize.options | String | null | Accepts the options of `PTBTokenizer` for example, things like "americanize=false" or "strictTreebank3=true,untokenizable=allKeep". See [the PTBTokenizer documentation](http://nlp.stanford.edu/software/tokenizer.html#Options). |
| tokenize.verbose | boolean | false | Make the TokenizerAnnotator verbose - that is, it prints out all tokenizations it performs. |

The `tokenize.options` option accepts a wide variety of settings for the `PTBTokenizer`.

| Option name | Description |
| --- | --- |
| invertible | Store enough information about the original form of the token and the whitespace around it that a list of tokens can be faithfully converted back to the original String. Valid only if the LexedTokenFactory is an instance of CoreLabelTokenFactory. The keys used are: TextAnnotation for the tokenized form, OriginalTextAnnotation for the original string, BeforeAnnotation and AfterAnnotation for the whitespace before and after a token, and perhaps BeginPositionAnnotation and EndPositionAnnotation to record token begin/after end character offsets, if they were specified to be recorded in TokenFactory construction. (Like the String class, begin and end are done so end - begin gives the token length.) |
| tokenizeNLs | Whether end-of-lines should become tokens (or just be treated as part of whitespace). |

## Tokenizing From The Command Line

This will command will take in the text of the file `input.txt` and produce a human readable output of the tokens.

```bash
java -Xmx5g edu.stanford.nlp.pipeline.StanfordCoreNLP -annotators tokenize -file input.txt
```

Other output formats include `conllu`, `conll`, `json`, and `serialized`.

## Tokenizing From Java

```java
package edu.stanford.nlp.examples;

import edu.stanford.nlp.ling.*;
import edu.stanford.nlp.pipeline.*;

import java.util.*;

public class PipelineExample {

  public static String text = "Marie was born in Paris.";

  public static void main(String[] args) {
    // set up pipeline properties
    Properties props = new Properties();
    // set the list of annotators to run
    props.setProperty("annotators", "tokenize");
    // build pipeline
    StanfordCoreNLP pipeline = new StanfordCoreNLP(props);
    // create a document object
    CoreDocument document = pipeline.processToCoreDocument(text);
    // display tokens
    for (CoreLabel tok : document.tokens()) {
      System.out.println(String.format("%s\t%d\t%d", tok.word(), tok.beginPosition(), tok.endPosition()));
    }
  }
}
```

This demo code will produce the tokens and the character offsets of the text.

```
Marie	0	5
was	6	9
born	10	14
in	15	17
Paris	18	23
.	23	24
```
