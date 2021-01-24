# ChineseScraper
This scipt scrapes the frequency list at http://www.zein.se/patrick/3000char.html to create a set of textfiles contaning the 3000 most frequent Chinese characters.
These texfiles are formatted in way so that they can be easily imported into Anki.


## nouyang

- scrape files
- use to add example words to https://ankiweb.net/shared/info/39888802
- make chinese only cards:


import regex
#result = regex.sub(ur'[^\p{Latin}]', u'', text)
with open('0-500.txt') as f:
    for i in range(20):
        text = f.readline()
        #lines = f.readlines
        #print(lines[:5])
        print(text)
        text = text[1:] #remove first character (which is the hanzi)
        text = text.split('{')[0]
        #string.punctuation
        r = regex.sub(r'[.]{3,}', u'…', text)
        r = r.replace('<BR>', ';')
        r = regex.sub(r'[\p{Latin}]', u'', r)
        r = re.sub(r"[^\w^;^…^!]+",'', r) # replace not-word charatesr with empty string
        r = re.sub(r"[^\w^…]{2,}",'; ', r) # replace not-word charatesr with empty string
        r = re.sub(r"[0-9]+",'', r) # replace numbers
        r = re.sub(r"^[^\w]+",'', r) # replace beginning not word chars
        r = r.strip()
        r = regex.sub(r'[;]$', u'', r) #add space between words
        #r = regex.sub(r'[;]', u'; ', r)


        #s = re.sub(r'[^\w\s]','',s)
        print(r)
        print('\n---\n')

def get_words(hanzi, line):
    line = line[1:] #remove first character (which is the hanzi)
    line = line.split('{')[0] # remove "{compare to " information
    r = regex.sub(r'[.]{3,}', u'…', line) # replace ellipsis so not removed later
    r = r.replace('<BR>', ';')
    r = regex.sub(r'[\p{Latin}]', u'', r)
    r = re.sub(r"[^\w^;^…^!]+",'', r) # replace not-word charatesr with empty string
    r = re.sub(r"[^\w^…]{2,}",', ', r) # replace not-word charatesr with empty string
    r = re.sub(r"[0-9]+",'', r) # replace numbers
    r = re.sub(r"^[^\w]+",'', r) # replace beginning not word chars 
    r = r.replace(';;', ';') 
    r = r.replace(';', '; ') # add space between words
    r = r.strip()
    r = regex.sub(r'[;,]$', u'', r) # remove comma or semicolon at end
    return r


mydict = {}
with open('0-500.txt') as f:
    lines = f.readlines()
    for line in lines:
        hanzi, full_defn = line.split(':')
        words = get_words(line)
        mydict[hanzi] = full_defn, words
        
pd.DataFrame.from_dict(mydict, orient='index', columns=['zein.se definition', 'words'])
