# stanza

## 1.安装

pip install stanza

## 2.下载语言包

进入Python环境

`import stanza`

`stanza.download('en')`#对应英语包

`stanza.download('zh-hans')`#对应中文包

`nlp = stanza.Pipeline('en')#set up a default neural pipeline in English`

`doc = nlp("Hello world")`

`doc.sentences[0].print_dependencies()`

