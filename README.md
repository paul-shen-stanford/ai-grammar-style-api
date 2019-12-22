# ai-grammar-style-api
Free multilingual AI style enhancement and grammar correction REST API. English, French, Spanish, Arabic, Japanese, Chinese. Based on deep NLP language models. See BERT, attention transformer neural networks... 

Uses AI to improve the entire text instead of relying on pre-coded grammar rules. This is much more flexible, subtle and scalable than traditional grammar checkers. However, result may contain deviations from original meaning. This will continually be improved with more training. Use at your own risk. 

This API is currently free and in beta testing. Please be courteous and don't flood it with requests. We're happy to set up a production grade server at an affordable rate.

This API is a spinoff from our main project. We're developing a writing tool combining "Grammarly-like" features with other writing aids. Not just in English but in all the major languages. If you'd like to get involved as an investor or engineer, let us know!

Paul Shen
Contact pxshen@alumni.stanford.edu

##Output
```
{'corrections': [{'end': 18,
                  'new': 'My name is Peter. ',
                  'old': 'myy nam is peter. ',
                  'start': 0},
                 {'end': 23, 'new': "I'm not", 'old': 'im no', 'start': 18},
                 {'end': 54,
                  'new': 'spelling in English. ',
                  'old': 'speelling in english. ',
                  'start': 32},
                 {'end': 66,
                  'new': 'I will',
                  'old': "i'm going to",
                  'start': 54},
                 {'end': 102,
                  'new': 'I think that writing requires a',
                  'old': 'i think writing required a',
                  'start': 76},
                 {'end': 133,
                  'new': 'I guess what I say',
                  'old': 'guess i say what',
                  'start': 117}],
 'input': "myy nam is peter. im no good at speelling in english. i'm going to "
          'say that i think writing required a lot of skill. guess i say what',
 'output': "My name is Peter. I'm not good at spelling in English. I will say "
           'that I think that writing requires a lot of skill. I guess what I '
           'say',
 'status': 'success'}
{'corrections': [{'end': 26,
                  'new': 'No puedo hablar Inglés',
                  'old': 'me no puede hablas inglais',
                  'start': 0}],
 'input': 'me no puede hablas inglais',
 'output': 'No puedo hablar Inglés',
 'status': 'success'}
{'corrections': [{'end': 24,
                  'new': 'Je ne aime pas étudier les mathématiques',
                  'old': 'je aimes pas etude maths',
                  'start': 0}],
 'input': 'je aimes pas etude maths',
 'output': 'Je ne aime pas étudier les mathématiques',
 'status': 'success'}
{'corrections': [{'end': 19,
                  'new': 'أنا لا من أي وقت مضى',
                  'old': 'لا أَفْعَلُهُ قَطُّ',
                  'start': 0}],
 'input': 'لا أَفْعَلُهُ قَطُّ',
 'output': 'أنا لا من أي وقت مضى',
 'status': 'success'}
{'corrections': [{'end': 7, 'new': '我是外国人。', 'old': '我是国外人民。', 'start': 0},
                 {'end': 15, 'new': '嗯，我说中国话。', 'old': '我的说中文是好。', 'start': 7}],
 'input': '我是国外人民。我的说中文是好。',
 'output': '我是外国人。嗯，我说中国话。',
 'status': 'success'}
{'corrections': [{'end': 6, 'new': '私は寿司式ダイスキー', 'old': '私すし食大好', 'start': 0}],
 'input': '私すし食大好',
Traceback (most recent call last):
 'output': '私は寿司式ダイスキー',
  File "C:/Users/Paul/Desktop/gpt2server/writely/test.py", line 60, in <module>
 'status': 'success'}
 ```
 
##Test code
```python
import pprint

import requests

s = requests.Session()


def print(x):
    pprint.pprint(x)


def correct(text, lang='en'):
    url = 'https://us-central1-project-318531836785902414.cloudfunctions.net/writing'
    payload = {
        'method': 'correct',
        'text': text,
        'lang': lang,
    }
    r = s.post(url, json=payload).json()
    return r


test_inputs = {

    'en': [
        "myy nam is peter. im no good at speelling in english. i'm going to say that i think writing required a lot of skill. guess i say what"],
    'es': ['me no puede hablas inglais'],
    'fr': ['je aimes pas etude maths'],
    'ar': ['لا أَفْعَلُهُ قَطُّ'],
    'zh': ['我是国外人民。我的说中文是好。'],
    'ja': ['私すし食大好'],

}
for lang in test_inputs:
    for input in test_inputs[lang]:
        r = correct(input, lang)
        print(r)
```
