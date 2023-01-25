<img align="right" width="300" height="300" src="https://avatars.githubusercontent.com/u/115706761?s=400&u=7c6cae892816e172b0b7eef99f2d32adb948c6ad&v=4">

# NLP-PRIMER-WORKSHOP
Natural Language Processing (NLP) --natuurlijke taal verwerking-- is een hybride AI-discipline, ontwikkeld vanuit de taalkunde en de informatica om menselijke taal begrijpelijk te maken voor machines.


********
## Context & Leeruitkomst
********



<div align="left">

|LEERDOEL|
| --------- |
| 1. [Coderen in Python met Anaconda + Jupyter notebooks](#l1) |
| 2. [ChatGPT als hulpmiddel om te leren coderen](#l2) |
| 3. [Tekstgegevens importeren en visualiseren](#l3)  | 
| 4. [Tekstgegevens voorbewerken en opschonen](#l4)  |
| 5. [Tekstgegevens analyseren en interpreteren](#l5)  |
| 6. [Aanpassen van vrije-tekst](#l6)   |

Na afloop van deze workshop ben je instaat om 
* met behulp van Python en Jupyter notebooks, tekstgegevens te importeren, te visualiseren en te voorbewerken. <br>
*  om met behulp van NLP technieken, tekstgegevens te analyseren en te interpreteren. <br>

De python-broncode voor deze workshop is te vinden in de [Notebooks folder van deze repository](https://github.com/robvdw/NLP-PRIMER-WORKSHOP/blob/main/Notebooks/Docx-NER-pandas-V07.ipynb)


</div> <br />

********
# l1
## LEERDOEL [1]: Coderen in Python met Anaconda + Jupyter notebooks
******** 

<br>

|Materialen|
| --------- |
| https://github.com/robvdw/Creating-AI-Data-Products-Using-Jupyter-Notebooks| 

<br>

********
# l2
## LEERDOEL [2]: ChatGPT als hulpmiddel om te leren coderen
******** 

<br>


|Materialen|
| --------- |
| https://github.com/robvdw/AIs-NEW-FRONTIER-Chat-GPT |

<br>

********
# l3
## LEERDOEL [3]: Tekstgegevens kunnen importeren en visualiseren
******** 

### Python code voor het inlezen van text data van .docx formaat documenten
 
Hier leer je hoe .docx en .pdf bestanden kunnen worden ingelezen in Python  <br> zodat we er vervolgens mee kunnen werken in SpaCy.

We gaan hiervoor gebruik maken van de volgende libraries:

os (voor het inlezen van bestanden uit de lokale omgeving)
spacypdfreader (voor het inlezen van pdf bestanden)
docx (voor het inlezen van dox bestanden)
spacy (voor het verwerken van de ingelezen tekst)


### Stap 3.1

Installeer de benodigde libraries
Voordat we aan de slag kunnen, moeten we eerst de benodigde libraries installeren. Dit kun je doen door de volgende commando's uit te voeren in je command prompt of terminal:

```python
# IF NO MODULE named spacypdfreader | python-docx | spacy
# install the following libraries by uncommenting the following lines

#!pip install spacypdfreader
#!pip install python-docx
#!pip install spacy

```

Op de SpaCy website kun je meer informatie vinden over de verschillende SpaCy libraries en hoe je deze kunt gebruiken en installeren: https://spacy.io/usage


![Instal-SpaCy](https://user-images.githubusercontent.com/684692/214674372-9b36237e-2a54-44d4-8c78-f3aeae91bcbc.jpg)


```python
pip install -U pip setuptools wheel
pip install -U spacy
python -m spacy download nl_core_news_sm
python -m spacy download en_core_web_sm

```


Met de os library kunnen we *"operating system"*  [OS] "command line" instructies's uitvoeren in Python. 
Het is dan mogelijk om de huidige directory instellen naar de map waar de data bestanden zich bevinden. 
Dit doen we door de volgende regels toe te voegen aan het begin het script:

```python
# code needed to set current directory to path with data files
# XXXXXXXXXX = path to data files
import os
currentdir = os.getcwd() + r'/XXXXXXXXXX'
flist = pd.DataFrame()

# create dataframe with list of .xxx files that are in the data map
# for example .docx | .pdf |  .html | .csv
file_type='.pdf' #   select desired file type

# Create dataframe with list of .docx files in de data map
for r, d, f in os.walk(currentdir):
    for idx, file in enumerate(f):
        if file_type in file:
            #print(os.path.join( ' ', file))
            temp = df([file], index = [idx+1])
            flist = pd.concat([flist, temp])   
            
#  Create column with label "filename"    
#  Column contains list of filenames of type as specified in file_type
filenameslist = flist.rename(columns={0: 'filename'})

# Display current directory
# Notice that dataframes are displayed in a for humans nice readable format
display(currentdir)

# DISPLAY content of the current directory + path + filenames  in Table format
# ROWS index represent the number of files available in the current directory
display(filenameslist)
```

### Stap 3.2

Importeer de libraries in je Python script
Nu we de libraries geïnstalleerd hebben, kunnen we ze importeren in ons Python script. Dit doen we door de volgende regels toe te voegen aan het begin van ons script:

```python
# importeer de benodigde libraries
import os
import docx
import spacy
from spacypdfreader import pdf_reader
```

### Stap 3.3
Lees een pdf bestand in
Om een pdf bestand in te lezen gebruiken we de PyPDF2 library. <br> 
De volgende regels code laten zien hoe je een pdf bestand inleest en vervolgens de inhoud van de eerste pagina weergeeft:

```python
## SELECT FILENAME + path
currentdir = os.getcwd()
datadir = r'/DATA/'

## NUMBER selects index of filename in the list 
number = 2-1  # 2 - 1 = 2rd file in the list
docsel  = currentdir + datadir + filenameslist.filename.iloc[number]
display(docsel)


# laden van de spacy NLP model
nlp = spacy.load('nl_core_news_sm')

# open het pdf bestand
data = pdf_reader(docsel, nlp)

# Toon alle text van pagina selp van de PFD file.
selp = 4; # select page number
display(doc._.page(selp))         # 'able to display the destination page'

```

### Stap 3.4

Lees een .docx bestand in
Om een .docx bestand in te lezen gebruiken we de docx library. <br>

```python
# open het dox bestand
document = docx.Document('voorbeeld.docx')
# haal de tekst uit het bestand
tekst = ""
for para in document.paragraphs:
    tekst += para.text
print(tekst)
    
```

### Stap 3.5

Verwerk de ingelezen tekst met SpaCy.
Nu we de tekst uit ons .docx of pdf bestand hebben gehaald, kunnen we deze verwerken met SpaCy. 
Hieronder staat voorbeeld code van hoe je dit kunt doen.



```python
# laden van de spacy NLP model
nlp = spacy.load("en_core_web_sm")

```

### Stap 3.6

Python code voor visualiseren van text dataFrames van .docx en/of .pdf formaat documenten
 
We hebben geleerd hoe we .docx en .pdf bestanden kunnen inlezen in Python, maar nu gaan we leren hoe we deze ingelezen tekst kunnen omzetten in dataframes met behulp van Numpy en Pandas.

We gaan hiervoor gebruik maken van de volgende libraries:

Numpy
Pandas
Stap 1: Installeer de benodigde libraries
Voordat we aan de slag kunnen, moeten we eerst de benodigde libraries installeren. Dit kun je doen door de volgende commando's uit te voeren in je command prompt of terminal:

```
!pip install numpy
!pip install pandas
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
# laden van de spacy NLP model
nlp = spacy.load('nl_core_news_sm')

# open het pdf bestand
data = pdf_reader(voorbeeld.pdf, nlp)

pdf_df = pd.DataFrame(data)
print(pdf_df)

```

### Stap 3.7

Creëer een dataframe van de ingelezen .docx bestanden
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
docx_df = pd.DataFrame(data)
print(docx_df)
```

********
# l4
### LEERDOEL [4]: Tekstgegevens voorbewerken en opschonen met SpaCy
******** 

In de vorige les hebben we geleerd hoe we ingelezen .docx en .pdf bestanden kunnen omzetten in dataframes met behulp van Numpy en Pandas. 

Nu leren we hoe deze dataframes kunnen voorbereiden voor het benutten van een natuurlijke taal verwerking functie: Named Entity Recognition (NER). Met aLs doel om vrije-tekst documenten te kunnen anonimiseren.

We gaan hiervoor gebruik maken van het  Nederlandse taal corpus zoals beschikbaar via SpaCy.
Via de volgende link kun je meer informatie vinden over de verschillende SpaCy libraries en hoe je deze kunt gebruiken en installeren: https://spacy.io/usage




### Stap 4.1

Downloaden van het Nederlandse NLP model
Voordat je het model kunt gebruiken, moet je het eerst downloaden. Dit kun je doen door de volgende commando uit te voeren in je command prompt of terminal:

```
python -m spacy download nl_core_news_sm
```
<br> 

### Stap 4.2

Laden van het Nederlandse NLP model
Nadat het model is gedownload, kun je het laden in je Python script door de volgende regel toe te voegen:

```python
# importeren van SpaCy NLP library
import spacy
# laden van de spacy NLP model
nlp = spacy.load("nl_core_news_sm")
```
Met deze stappen heb je het Nederlandse NLP model geladen in spacy en kun je deze gebruiken om Nederlandse tekst te verwerken en analyseren.

<br> 

### Stap 4.3

Voorbereiden van de dataframe voor NER
In deze stap gaan we de dataframe voorbereiden voor NER. <br> 
Hieronder staat een voorbeeld van hoe je dit kunt doen met de ingelezen pdf dataframe:


```python
# verwerk de ingelezen tekst met spacy
pdf_doc = nlp(pdf_df.tekst[0])

# maak een lijst van entiteiten
entiteiten = []
for ent in pdf_doc.ents:
    entiteiten.append((ent.text, ent.label_))

# maak een nieuwe kolom in de pdf dataframe voor de entiteiten
pdf_df["entiteiten"] = entiteiten
print(pdf_df)
```
Herhaal deze stap ook met de ingelezen docx dataframe.
<br>

### Stap 4.4

Analyseren van de entiteiten
Nu we de entiteiten hebben toegevoegd aan onze dataframes, kunnen we deze analyseren. 
<br> Hieronder staat een voorbeeld van hoe je dit kunt doen met de pdf dataframe:

<br>



```python
# aantal entiteiten per type
entiteiten_per_type = pdf_df.entiteiten.apply(pd.Series).stack().value_counts()
print(entiteiten_per_type)
``` 
### Stap4.5 

Voor het opschonen van de vrije-tekst nodig om NER te kunnen detecteren is de volgende code nodig.

Belangrijk is om nu te begrijpen wat de tokenisatie is en wat de verschillende tags betekenen.

* Welke tags zijn er en wat betekenen ze? 
* Waar in de code vindt tokenisatie plaats? 
* Aan welke variabele wordt de tokenisatie toegekend?



```python
## DOWNLOAD + INSTALL DUTCH language CORPUS (if not installed already)
## https://spacy.io/models/nl
#!python -m spacy download nl_core_news_md
#!python -m spacy download nl_core_news_sm
#!python -m spacy download nl_core_news_lg

import os
import docx
import spacy
from spacy import displacy
import numpy as np
import pandas as pd
from pandas import DataFrame as df

currentdir = os.getcwd() + r'/RAW_DATA/NON'
flist = pd.DataFrame()

# create dataframe with list of .docx files in de data map
for r, d, f in os.walk(currentdir):
    for idx, file in enumerate(f):
        if ".docx" in file:
            #print(os.path.join( ' ', file))
            temp = df([file], index = [idx+1])
            flist = pd.concat([flist, temp])   
            
#  Create column label "filename"      
filenameslist = flist.rename(columns={0: 'filename'})

# DISPLAY content of currentdir + filenames  .docx list   
# ROWS index the number of files available
display(currentdir)
display(filenameslist)

## SELECT FILENAME + path
currentdir = os.getcwd()
datadir = r'/RAW_DATA/NON/'

## NUMBER selects index of filename in the list 
number = 5
docsel  = currentdir + datadir + filenameslist.filename.iloc[number]

#  DISPLAY selected filename
display(docsel)


## READ .docx file
doc = docx.Document(docsel)
data = ""
fullText = []

for para in doc.paragraphs:
    fullText.append(para.text)
    data = '\n'.join(fullText)
    
import spacy
from spacy import displacy

spacy.prefer_gpu()
nlp = spacy.load("nl_core_news_lg")
doc = nlp(data) 

## DISPLAY XXXXXXXXX results
## In jupyter Notebooks Use .render (NIET .serve)
displacy.render(doc, style="ent")

for token in doc:
    print(token.text, token.pos_, token.dep_)

    for token in doc:
    print(token.text, token.lemma_, token.pos_, token.tag_, token.dep_,
            token.shape_, token.is_alpha, token.is_stop)

tokens = [(token.text, token.lemma_, token.pos_, token.tag_, token.dep_,token.shape_, token.is_alpha, token.is_stop) for token in doc]
df = pd.DataFrame(tokens, columns=['text','lemma', 'PoS', 'tag', 'dependency', 'shape', 'alpha', 'stop woord'])
pd.set_option("display.max_rows", None, "display.max_columns", None) # show all rows
df
```


********
# l5
### LEERDOEL [5]: Uitvoeren van NER op opgeschoonde vrije-tekst met SpaCy
******** 

Op basis van de resultaten van de vorige stap, kunnen we nu de NER uitvoeren op de opgeschoonde vrije-tekst.

* Kun je de onderstaande code begrijpen? 
* Bedenk dat we Pandas gebruiken om de data te analyseren en te visualiseren.
* Vervolgens wordt SpaCy gebruikt om de NER uit te voeren.

```python
#SEARCH for  Named Entity Studentnummer in text column of dataframe df
sel = (df.text == 'Studentnummer')
nums = np.array( list(np.where(sel)[0]) )
display( nums[0]                 )
display( df[sel]                 )
display( df.iloc [nums[0]+3, 0]  )  

# NER
for entity in doc.ents:
    print(entity.text + ' - ' + entity.label_ + ' - ' + str(spacy.explain(entity.label_)))


 entities = [(e.label_,e.text) for e in doc.ents]
df = pd.DataFrame(entities, columns=['Entity','Identified'])

pd.set_option("display.max_rows", None, "display.max_columns", None)
display(df)

# Selecteer op de gewenste NER

sel = (df.Entity == 'PERSON')
df[sel] 

sel = (df.Entity == 'CARDINAL')
df[sel] 
```



********
#### Stap[6]: Aanpassen van bestaande vrije-tekst voor je eigen doeleinden

De onderstaande code maakt het mogelijk om op basis van Spacy-Based NER analyse vrije-tekst te anonimiseren. <br>

We gebruiken hiervoor de volgende packages die nodig zijn om .docx bestanden te kunnen lezen en te schrijven; 
zonder dat het format en/of Layout van de .docx file wordt aangetast. <br>

```python
!pip install -U -q --verbose python-docx
!pip install -U -q --verbose python-docx-replace
!pip install -U -q --verbose docxedit
```

We importeren eersts de packages die we nodig hebben om de .docx file te kunnen lezen en te schrijven. <br>

```python
import docx
import os
from docx import Document
#from python_docx_replace import docx_replace
#from python_docx_replace import docx_remove_table
import docxedit

# get your document using python-docx
doc = Document('replaced.docx')
```

We gebruiken de volgende code ode vrije-tekst op specifieke plaatsen aan te passen. <br>

```python
# Replace all instances of 'yyyyyy'' in the document by 'xxxxxx'
docxedit.replace_string(doc, old_string='Judith Adriaanse', new_string='XXXXXX XXXXXXX')
```

Vervolgens slaan we het aangepaste .docx  bestand op onder een  herkenbare naam. <br>

```python
# save the ALTERED document
doc.save("replacedx.docx")
```
Door de code van leerdoel 6 te combineren met de code van leerdoel 5, kunnen we de NER uitvoeren op de opgeschoonde vrije-tekst. <br>


Hoe zou deze code er uit kunnen zien?





