
# IBM Watson Natural Language Understanding API

This is the code for NLP lab Assignment 3 where the task is to classify a particular news article into categories. It then creates folders for each category and saves the news article in the particular folder.





## Requirements

Make sure you have installed the ibm_watson library. You can do this by runnning the following code:

```
!pip install ibm_watson

```

Enable the IBM Watson Natural Language Understanding API from:   
https://www.ibm.com/in-en/cloud/watson-natural-language-understanding 




## Changes in the code


 ```
import json
from ibm_watson import NaturalLanguageUnderstandingV1
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator
from ibm_watson.natural_language_understanding_v1 import Features, CategoriesOptions

authenticator = IAMAuthenticator('{YOUR_API_KEY}')
natural_language_understanding = NaturalLanguageUnderstandingV1(
    version='2021-08-01',
    authenticator=authenticator
)

natural_language_understanding.set_service_url('{Service_URL}')

response = natural_language_understanding.analyze(
    url='{NEWS_ARTICLE_LINK',
    features=Features(categories=CategoriesOptions(limit=3))).get_result()

print(json.dumps(response, indent=2))
```

Replace:   
__'{YOUR_API_KEY}'__ with the API Key from the instance on IBM Watson  
__'{Service_URL}'__ with the instance URL from IBM Watson  
__'{NEWS_ARTICLE_LINK}'__ with the news article link of your choice  



## Categorizing
Running the following code will give you the categories which the news article falls under.  

``` 
import os
import glob
lab = response['categories']
cat = []
for num in range(len(lab)):
  lbls = lab[num]
  lst = lbls['label'].split('/')
  lst.pop(0)
  for x in lst:
    cat.append(x)


cat = set(cat)
cat
```


## Saving the article in a folder

The code creates a new folder of a category if it doesn't exist and adds the article link every category it is a part of.  

``` 
for x in cat:
    if not os.path.exists("{custom_path" + x):
      print("true")
      os.makedirs("custom_folder_path" + x)

    dir = os.path.dirname("custom_folder_path" + x)
    z = dir + "/" + x + "/"
    fle = len(glob.glob(z + '.*/.txt'))

    link = z + "news" + str(fle + 1) + ".txt"
    f = open(link, 'w+')
    f.write(response['retrieved_url'])
    f.close()
 ```   

 Replace:  
__'{custom_path}'__ with the directory path  
__'{custom_folder_path}'__ with the folder path in the directory  
The glob functions will go through all text files that are present in our custom folder