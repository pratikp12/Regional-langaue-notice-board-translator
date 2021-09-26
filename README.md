# Regional-langaue-notice-board-translator
# idea
For a new-comer to the city, Pune and Puneite may appear to be arrogant, rude and not-so-friendly. However, after you spend a considerable time in the historic city that you realize the true character of a Punekar, the Pune citizen.

Pati is a term which is used in Marathi for signboards or billboards.

Patya is the plural of Pati.

The Patyas in Pune were once omnipresent wherever one chose to venture in-restaurants, shops, libraries, gardens and old ancestral homes of Punekars, known as 'Wadas'. They reduced in number over a period of time.

No matter however curt or nasty, there is no denying their precision and directness. For, Punekars don't believe in sugar-coating words. They call a spade a spade.

These Patya have become famous thanks to social media so much so that there's an entire site dedicated to it.

I found these pretty savage!

<img src='https://static.abplive.com/wp-content/uploads/sites/4/2018/06/24204056/puneri-pati-11.jpeg'>
Someone who eat paan while sitting here will get slap 

People come to pune from different regions.
Sign boards written in reginal langauge is not understood by some new comers.

# Python libraries implemented
1. easyocr
Ready-to-use OCR with 80+ supported languages and all popular writing scripts including Latin, Chinese, Arabic, Devanagari, Cyrillic and etc.

## Installation

Install using `pip` for stable release,

``` bash
pip install easyocr
```

For latest development release,

``` bash
pip install git+git://github.com/jaidedai/easyocr.git
```

Note 1: for Windows, please install torch and torchvision first by following the official instruction here https://pytorch.org. On pytorch website, be sure to select the right CUDA version you have. If you intend to run on CPU mode only, select CUDA = None.

Note 2: We also provide Dockerfile [here](https://github.com/JaidedAI/EasyOCR/blob/master/Dockerfile).

## Usage

``` python
import easyocr
reader = easyocr.Reader(['ch_sim','en']) # need to run only once to load model into memory
result = reader.readtext('chinese.jpg')
```

Output will be in list format, each item represents bounding box, text and confident level, respectively.

``` bash
[([[189, 75], [469, 75], [469, 165], [189, 165]], '愚园路', 0.3754989504814148),
 ([[86, 80], [134, 80], [134, 128], [86, 128]], '西', 0.40452659130096436),
 ([[517, 81], [565, 81], [565, 123], [517, 123]], '东', 0.9989598989486694),
 ([[78, 126], [136, 126], [136, 156], [78, 156]], '315', 0.8125889301300049),
 ([[514, 126], [574, 126], [574, 156], [514, 156]], '309', 0.4971577227115631),
 ([[226, 170], [414, 170], [414, 220], [226, 220]], 'Yuyuan Rd.', 0.8261902332305908),
 ([[79, 173], [125, 173], [125, 213], [79, 213]], 'W', 0.9848111271858215),
 ([[529, 173], [569, 173], [569, 213], [529, 213]], 'E', 0.8405593633651733)]
```
Note 1: `['ch_sim','en']` is the list of languages you want to read. You can pass
several languages at once but not all languages can be used together.
English is compatible with every languages. Languages that share common characters are usually compatible with each other.

Note 2: Instead of filepath `chinese.jpg`, you can also pass OpenCV image object (numpy array) or image file as bytes. URL to raw image is also acceptable.

Note 3: The line `reader = easyocr.Reader(['ch_sim','en'])` is for loading model into memory. It takes some time but it need to be run only once.

You can also set `detail` = 0 for simpler output.

``` python
reader.readtext('chinese.jpg', detail = 0)
```
Result:
``` bash
['愚园路', '西', '东', '315', '309', 'Yuyuan Rd.', 'W', 'E']
```

Model weight for chosen language will be automatically downloaded or you can
download it manually from the [model hub](https://www.jaided.ai/easyocr/modelhub) and put it in '~/.EasyOCR/model' folder

In case you do not have GPU or your GPU has low memory, you can run it in CPU mode by adding gpu = False

``` python
reader = easyocr.Reader(['ch_sim','en'], gpu = False)
```

For more information, read [tutorial](https://www.jaided.ai/easyocr/tutorial) and [API Documentation](https://www.jaided.ai/easyocr/documentation).


2. googletrans

Googletrans is a **free** and **unlimited** python library that
implemented Google Translate API. This uses the `Google Translate Ajax
API <https://translate.google.com>`__ to make calls to such methods as
detect and translate.

Compatible with Python 3.6+.

For details refer to the `API
Documentation <https://py-googletrans.readthedocs.io/en/latest>`__.

Features
--------

-  Fast and reliable - it uses the same servers that
   translate.google.com uses
-  Auto language detection
-  Bulk translations
-  Customizable service URL
-  HTTP/2 support

TODO
~~~~

more features are coming soon.

-  Proxy support
-  Internal session management (for better bulk translations)

HTTP/2 support
~~~~~~~~~~~~~~

This library uses httpx for HTTP requests so HTTP/2 is supported by default.

You can check if http2 is enabled and working by the `._response.http_version` of `Translated` or `Detected` object:

.. code:: python

   >>> translator.translate('테스트')._response.http_version
   # 'HTTP/2'


How does this library work
~~~~~~~~~~~~~~~~~~~~~~~~~~

You may wonder why this library works properly, whereas other
approaches such like goslate won't work since Google has updated its
translation service recently with a ticket mechanism to prevent a lot of
crawler programs.

I eventually figure out a way to generate a ticket by reverse
engineering on the `obfuscated and minified code used by Google to
generate such
token <https://translate.google.com/translate/releases/twsfe_w_20170306_RC00/r/js/desktop_module_main.js>`__,
and implemented on the top of Python. However, this could be blocked at
any time.

--------------

Installation
------------

To install, either use things like pip with the package "googletrans"
or download the package and put the "googletrans" directory into your
python path.

.. code:: bash

    $ pip install googletrans

Basic Usage
-----------

If source language is not given, google translate attempts to detect the
source language.

.. code:: python

    >>> from googletrans import Translator
    >>> translator = Translator()
    >>> translator.translate('안녕하세요.')
    # <Translated src=ko dest=en text=Good evening. pronunciation=Good evening.>
    >>> translator.translate('안녕하세요.', dest='ja')
    # <Translated src=ko dest=ja text=こんにちは。 pronunciation=Kon'nichiwa.>
    >>> translator.translate('veritas lux mea', src='la')
    # <Translated src=la dest=en text=The truth is my light pronunciation=The truth is my light>

Customize service URL
~~~~~~~~~~~~~~~~~~~~~

You can use another google translate domain for translation. If multiple
URLs are provided, it then randomly chooses a domain.

.. code:: python

    >>> from googletrans import Translator
    >>> translator = Translator(service_urls=[
          'translate.google.com',
          'translate.google.co.kr',
        ])

Advanced Usage (Bulk)
~~~~~~~~~~~~~~~~~~~~~

Array can be used to translate a batch of strings in a single method
call and a single HTTP session. The exact same method shown above works
for arrays as well.

.. code:: python

    >>> translations = translator.translate(['The quick brown fox', 'jumps over', 'the lazy dog'], dest='ko')
    >>> for translation in translations:
    ...    print(translation.origin, ' -> ', translation.text)
    # The quick brown fox  ->  빠른 갈색 여우
    # jumps over  ->  이상 점프
    # the lazy dog  ->  게으른 개

Language detection
~~~~~~~~~~~~~~~~~~

The detect method, as its name implies, identifies the language used in
a given sentence.

.. code:: python

    >>> from googletrans import Translator
    >>> translator = Translator()
    >>> translator.detect('이 문장은 한글로 쓰여졌습니다.')
    # <Detected lang=ko confidence=0.27041003>
    >>> translator.detect('この文章は日本語で書かれました。')
    # <Detected lang=ja confidence=0.64889508>
    >>> translator.detect('This sentence is written in English.')
    # <Detected lang=en confidence=0.22348526>
    >>> translator.detect('Tiu frazo estas skribita en Esperanto.')
    # <Detected lang=eo confidence=0.10538048>

GoogleTrans as a command line application
-----------------------------------------

.. code:: bash

    $ translate -h
    usage: translate [-h] [-d DEST] [-s SRC] [-c] text

    Python Google Translator as a command-line tool

    positional arguments:
      text                  The text you want to translate.

    optional arguments:
      -h, --help            show this help message and exit
      -d DEST, --dest DEST  The destination language you want to translate.
                            (Default: en)
      -s SRC, --src SRC     The source language you want to translate. (Default:
                            auto)
      -c, --detect

    $ translate "veritas lux mea" -s la -d en
    [veritas] veritas lux mea
        ->
    [en] The truth is my light
    [pron.] The truth is my light

    $ translate -c "안녕하세요."
    [ko, 1] 안녕하세요.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Implementation
    
<img src='https://live.staticflickr.com/8014/7568844308_962bd7370c_b.jpg -O /content/image3.jpg'></img>
```
rcParams['figure.figsize'] = 8, 16
reader = easyocr.Reader(['en','mr'])
file_name = "image3.jpg"
Image(file_name)
output = reader.readtext(file_name)
output
```

# Output
<pre>
[([[103, 88], [934, 88], [934, 175], [103, 175]], 
  'संबंधित सुजाण मित्रांसाटी विशेष सुचना', 
  0.5621431326373985),
 ([[249, 183], [859, 183], [859, 276], [249, 276]],
  'व्यवसायाची जागा आहे',
  0.6583658488009128),
 ([[187, 299], [847, 299], [847, 387], [187, 387]],
  'गप्पांसाठीचा अड्डा नाही',
  0.4396086459051765),
 ([[164, 408], [872, 408], [872, 465], [164, 465]],
  'स्टाफ इथे कामासाठी येतो, गप्पा मारण्यासाठी नाही',
  0.581407630456156),
 ([[117, 547], [917, 547], [917, 608], [117, 608]],
  'विचार करा तुमच्या नोकरीच्या ठिकाणी तुमचा बॉस अश्या',
  0.5607424213297094),
 ([[335, 601], [693, 601], [693, 663], [335, 663]],
  'गोष्टी खपवुन घेईल का?',
  0.9502857982612544),
 ([[678, 674], [842, 674], [842, 706], [678, 706]],
  '14/7/2012',
  0.7698384196079756),
 ([[870, 673], [966, 673], [966, 705], [870, 705]],
  '२२ :०8',
  0.549316698444405)]
  </pre>
  Translation of **Marathi Text**
  ```
  from googletrans import Translator

translator = Translator()
result = translator.translate(text, src='mr', dest='en')

print(result.src)
print(result.dest)
print(result.text)
```

OUTPUT <br>
mr <br>
en <br>
Special Suggestions for Relevant Sujan Friends There is a place for business No chat room Staff come here for work, not to chat Think your boss will tolerate such things in your work place?
