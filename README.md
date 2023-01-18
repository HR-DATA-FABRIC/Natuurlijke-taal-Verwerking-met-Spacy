<img align="right" width="300" height="300" src="https://avatars.githubusercontent.com/u/115706761?s=400&u=7c6cae892816e172b0b7eef99f2d32adb948c6ad&v=4">

# NLP-PRIMER-WORKSHOP
Natural Language Processing (NLP) --natuurlijke taal verwerking-- is een hybride AI-discipline, ontwikkeld vanuit de taalkunde en de informatica om menselijke taal begrijpelijk te maken voor machines.


********
## Context & Leeruitkomst
********


<div align="left">

|Leerdoel|
| --------- |
| 1. Coderen in Python met Anaconda + Jupyter notebooks |
| 2. ChatGPT als hulpmiddel om te lere coderen |
| 3. Tekstgegevens importeren en visualiseren | 
| 4. Tekstgegevens voorbewerken en opschonen |

</div> <br />

********
## STAP [1]: Coderen in Python met Anaconda + Jupyter notebooks
******** 

<br>

|Materialen|
| --------- |
| https://github.com/robvdw/Creating-AI-Data-Products-Using-Jupyter-Notebooks| 

<br>

********
## STAP [2]: ChatGPT als hulpmiddel om te leren coderen
******** 

<br>


|Materialen|
| --------- |
| https://github.com/robvdw/AIs-NEW-FRONTIER-Chat-GPT |

<br>

********
## STAP[3]: Tekstgegevens kunnen importeren en visualiseren
******** 

### Python code voor het inlezen van text data van .docx formaat documenten
 
Hier leer je hoe .docx en .pdf bestanden kunnen worden ingelezen in Python  <br> zodat we er vervolgens mee kunnen werken in SPacy.

We gaan hiervoor gebruik maken van de volgende libraries:

PyPDF2 (voor het inlezen van pdf bestanden)
docx (voor het inlezen van dox bestanden)
spacy (voor het verwerken van de ingelezen tekst)
Stap 1: Installeer de benodigde libraries
Voordat we aan de slag kunnen, moeten we eerst de benodigde libraries installeren. Dit kun je doen door de volgende commando's uit te voeren in je command prompt of terminal:

```python
pip install PyPDF2
pip install python-docx
pip install spacy

```
Stap 2: Importeer de libraries in je Python script
Nu we de libraries geïnstalleerd hebben, kunnen we ze importeren in ons Python script. Dit doen we door de volgende regels toe te voegen aan het begin van ons script:

```python
import PyPDF2
import docx
import spacy

```


Stap 3: Lees een pdf bestand in
Om een pdf bestand in te lezen gebruiken we de PyPDF2 library. <br> 
Hieronder staat een voorbeeld van hoe je dit kunt doen:

```python
# open het pdf bestand
with open('voorbeeld.pdf', 'rb') as file:
    # lees het bestand in met PyPDF2
    pdf = PyPDF2.PdfFileReader(file)
    # haal de tekst uit het bestand
    tekst = ""
    for i in range(0, pdf.getNumPages()):
        tekst += pdf.getPage(i).extractText()
    print(tekst)

```

Stap 4: Lees een dox bestand in
Om een dox bestand in te lezen gebruiken we de docx library. Hieronder staat een voorbeeld van hoe je dit kunt doen:

```python
# open het dox bestand
document = docx.Document('voorbeeld.docx')
# haal de tekst uit het bestand
tekst = ""
for para in document.paragraphs:
    tekst += para.text
print(tekst)
    
```

Stap 5: Verwerk de ingelezen tekst met SPacy
Nu we de tekst uit ons .docx of pdf bestand hebben gehaald, kunnen we deze verwerken met SpaCy. Hieronder staat een voorbeeld van hoe je dit kunt doen:

```python
# laden van de spacy NLP model
nlp = spacy.load("en_core_web_sm")

```

### Python code voor visualiseren van text dataFrames van .docx en/of .pdf formaat documenten
 
We hebben geleerd hoe we .docx en .pdf bestanden kunnen inlezen in Python, maar nu gaan we leren hoe we deze ingelezen tekst kunnen omzetten in dataframes met behulp van Numpy en Pandas.

We gaan hiervoor gebruik maken van de volgende libraries:

Numpy
Pandas
Stap 1: Installeer de benodigde libraries
Voordat we aan de slag kunnen, moeten we eerst de benodigde libraries installeren. Dit kun je doen door de volgende commando's uit te voeren in je command prompt of terminal:

```
pip install numpy
pip install pandas
```
Stap 2: Importeer de libraries in je Python script
Nu we de libraries geïnstalleerd hebben, kunnen we ze importeren in ons Python script. Dit doen we door de volgende regels toe te voegen aan het begin van ons script:

```python
import numpy as np
import pandas as pd

```

Stap 3: Creëer een dataframe van de ingelezen pdf bestanden
In deze stap gaan we de ingelezen tekst uit ons pdf bestand omzetten in een dataframe. Hieronder staat een voorbeeld van hoe je dit kunt doen:

```python
# open het pdf bestand
with open('voorbeeld.pdf', 'rb') as file:
    # lees het bestand in met PyPDF2
    pdf = PyPDF2.PdfFileReader(file)
    # haal de tekst uit het bestand
    tekst = ""
    for i in range(0, pdf.getNumPages()):
        tekst += pdf.getPage(i).extractText()
    # creëer een dataframe van de ingelezen tekst
    data = {'tekst': [tekst]}
    pdf_df = pd.DataFrame(data)
    print(pdf_df)
```
Stap 4: Creëer een dataframe van de ingelezen dox bestanden
In deze stap gaan we de ingelezen tekst uit ons dox bestand omzetten in een dataframe. Hieronder staat een voorbeeld van hoe je dit kunt doen:

```python
# open het dox bestand
document = docx.Document('voorbeeld.docx')
# haal de tekst uit het bestand
tekst = ""
for para in document.paragraphs:
    tekst += para.text
# creëer een dataframe van de ingelezen tekst
data = {'tekst': [tekst]}
dox_df = pd.DataFrame(data)
print(docx_df)
```

******
### STAP[4]: Named Entities Recognition (NER) leren opporen in vrije-tekst met SPacy
******** 

The code zoasl hieronder weergegeven kan worden ge

<br>
