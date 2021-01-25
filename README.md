# ChineseScraper
This scipt scrapes the frequency list at http://www.zein.se/patrick/3000char.html to create a set of textfiles contaning the 3000 most frequent Chinese characters.
These texfiles are formatted in way so that they can be easily imported into Anki.


## nouyang

- scrape files
- use to add example words to https://ankiweb.net/shared/info/39888802
- make chinese only cards:

## quickstart

Run 
```
python scraper.py
for file in *.txt; do (cat "${file}"; echo) >> concatenated.txt; done
```
This leaves some empty lines between concat'd files, if desired use following to
delete empty lines:
````
vi: g/^$/d 
```

Open the jupyter notebook, run to turn the output from the zein.se website (concatenated.txt) into a dataframe. 

We get our 2nd dataframe from ankiweb, where the description links to a
spreadsheet, I included as 'AnkiwebMostCommon3000.csv'. The same python notebook
reads this into a dataframe.

Both dataframes are concatenated by the Hanzi character. This new dataframe is
saved to `ankiweb+zein_merged.csv`.  I open this is google sheets or libreoffice
and convert to format as indicated by Ankiweb Addon Excel Import (see `SpreadsheetURL.txt` for link to this google sheet).
 I save this final formmated version as `Formatted for Import.xsls`. Then open
 Anki -> Import -> and it should detect fields correctly. For me I selected
 "update notes" by accident and it actually did the merge step for me... I did
 create fields beforehand as appropriate. Finally I styled my cards. 

 Makre sue to check 'Allow HTML in fields!'

ALSO - When importing - make sure to have correct deck open. Or else Anki will
not auto-detect the matching fields.

Anyway - there are some pecularities - maybe best to just download from versionn
I uploaded to ankiweb.: https://ankiweb.net/shared/info/595636619

I have included some screenshots in the Screenshots folder in case of use -
including of the styling I used, what it looks like to study on Android, etc.

