# 分词

核心逻辑：将句子、段落、文章这种长文本，分解为以字词为单位的数据结构。

* 文本切分：分词是将连续的文本切分为独立的、有意义的词汇单元的过程。这些词汇单元可以是单词、词组或特定的符号，切分的目的是使文本更易于处理和解析。
* 语义理解的基础：分词是语义理解的基础步骤。计算机通过分词能够识别出文本中的基本语义单元，进而进行词性标注、句法分析、语义推理等更高级的处理。
* 数据结构化：分词将非结构化的文本数据转化为结构化的词汇序列，使得文本数据能够被计算机程序有效地处理和分析。
  
为什么要分词： 分词是将自然语言简化为数学问题，提供合适语义粒度的关键步骤。

问题转化：分词可以将非结构化的文本数据转化为结构化数据，这样复杂的自然语言处理就被转化为了更易于处理的数学问题。

合适的语义粒度：词是语言中表达完整含义的基本单位。 与字相比，词能够提供更丰富的语义信息。单个字往往无法独立表达完整的意义，而词则可以。同时，与句子相比，词的粒度更小，更易于处理和复用。

![alt text](<pic/截屏2025-05-12 19.33.34.png>)

* 分词方式：英文文本天然地通过空格分隔单词，为自动分词提供了便利。中文则缺乏明确的分隔符，分词需要依据语义和上下文进行，更加复杂且容易产生歧义。
* 词形变化：英文单词具有丰富的词形变化，如时态、语态、单复数等，需要进行词形还原（Lemmatization）和词干提取（Stemming）以统一处理。词性还原：does，done，doing，did 需要通过词性还原恢复成 do。词干提取：cities，children，teeth 这些词，需要转换为 city，child，tooth”这些基本形态。中文则不需要。
* 粒度问题：中文分词时需要考虑粒度大小，即词汇的划分粗细。不同粒度可能对应不同的语义，需要根据具体场景选择。英文中由于单词本身即为基础单位，不存在这一问题。

## prompt engineering


![alt text](<pic/截屏2025-05-12 20.07.05.png>)

![alt text](<pic/截屏2025-05-12 20.06.03.png>)

