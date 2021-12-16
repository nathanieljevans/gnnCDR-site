
# List of random syntax examples 


## Downloading Data

`download_abcd_batch.sh` - Script to call NDA downloader <br>
`download.py` - NDA downloader (Fair Lab) <br>

<br>

.|File | Path | Func
-:|----------|-----|---------------------------
./|`download_abcd_batch.sh` | docs | Script to call NDA downloader
../../|`download.py` | docs | NDA data downloader
<img width=1/>|<img width=23/> | <img width=100/>|<img width=60/>

Name                               | Required | Details
---------------------------------- | -------- | -------
[Python Markdown][python-markdown] | Yes      | Python Markdown must be installed as it is the Markdown parser that is being used.
[Pygments (optional)][pygments]    | No       | If Pygments Syntax highlighting is desired, Pygments must be installed.  This can be omitted, and code blocks will be formatted for use with JavaScript code highlighters.

### Autoembed table from csv

??? note "Dynamically embedding a table from a .csv"
    === "Adding a new table"
        This is syntax to ad a new table
    === "Syntax"
        ``` 
        {{ read_csv('docs/tables/test_table.csv') }}
        ``` 
    === "output"
        {{ read_csv('docs/tables/test_table.csv') }}

```
### Add entire script

--8<--
"file1.ext"

"file2.ext"
--8<--
```


### Code snippets 

- add line numer and highlight lines 2 and 
```language linenums="1" hl_lines="2 3"```

??? bug  
	```pycon3 linenums="1" hl_lines="2 3"
	>>> import markdown
	>>> text = "A link https://google.com"
	>>> html = markdown.markdown(text, extensions=['pymdownx.magiclink'])
	```

??? note

    === "Output"
        Task List

        - [X] item 1
            * [X] item A
            * [ ] item B
                more text
                + [x] item a
                + [ ] item b
                + [x] item c
            * [X] item C
        - [ ] item 2
        - [ ] item 3


    === "Markdown"
        ```
        Task List

        - [X] item 1
            * [X] item A
            * [ ] item B
                more text
                + [x] item a
                + [ ] item b
                + [x] item c
            * [X] item C
        - [ ] item 2
        - [ ] item 3
        ```


!!! note
    test test for note

!!! todo
    test test for note

!!! tldr
    test test for note

!!! important
    test test for note

!!! done
    test test for note

!!! faq
    test test for note

!!! attention
    test test for note

!!! error
    test test for note

!!! bug
    test test for note

!!! quote
    test test for note




!!! reminder

    I still need to download the data   

???+ failure

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

??? example "Inline Highlighted Code Example"

    === "Output"
        Here is some code: `#!py3 import pymdownx; pymdownx.__version__`

        The mock shebang will be treated like text here: ` #!js var test = 0; `.

    === "Markdown"
        ```
        Here is some code: `#!py3 import pymdownx; pymdownx.__version__`.

        The mock shebang will be treated like text here: ` #!js var test = 0; `.
        ```


The mock shebang will be treated like text here: ` #!js var test = 0; `.

```bash
srun $PYTHON_ENV download.py \
	-i $manifest \
    	-o $outdir \
	-s $sublist \
    	-l $logfiles \
	-d $subset 
    	-p 6
```

```python

import pandas as pd
import numpy as np

def test_func(var1, var2):
    return x

```
### Clinical Data
 
`data_subsets.txt` - List of derivatives <br>
`subject_list.txt` - List of subjects <br> 
