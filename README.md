# Web-Scrapping
#My goal is to scrap the results table in this website and store it in a csv for easier manipulation using Python:http://www.hubertiming.com/results/2018Resolution
from urllib.request import urlopen #Use urllib.request module to open URLs.
from bs4 import BeautifulSoup #The Beautiful Soup package is used to extract data from html files
html=urlopen("https://www.hubertiming.com/results/2018Resolution")
bsobj=BeautifulSoup(html,"lxml") ##There are two things to note 1) we are converting the html data to a beautiful soup object.2) lxml is a very useful XML/HTML processing library.
print(bsobj)
table_rows=bsobj.findAll('tr') #to retrieve the table rows
print(table_rows)
for row in table_rows: #we need is all table rows in a list so that we can convert the list into data frame
    each_row=row.findAll('td')
    print(each_row)
lists_of_all_rows=[]  #We are doing two things here. 1) removing html tags using BeautifulSoup and extracting only text 2) Creating an empty list and appending each row of text to the empty list.
for row in table_rows:
    each_row=row.findAll('td')
    str_row=str(each_row)
    row_text=BeautifulSoup(str_row,"lxml").get_text()
    lists_of_all_rows.append(row_text)
print(lists_of_all_rows)  
import pandas as pd #The next step is to convert the list into a data frame and get the view of the rows using Pandas
import numpy as np
data=pd.DataFrame(lists_of_all_rows[5:])
print(data)
data.to_csv(r'Untitled Folder\Web Scrapping.csv', encoding='utf-8', index=False)
