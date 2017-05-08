# crawler
#on bottom left of the page there different companies that provide health plans and plans are on respective tables on pages ,pls store the data 
import urllib2
from bs4 import BeautifulSoup
import re
import requests

html_doc = urllib2.urlopen('https://www.policybazaar.com/health-insurance/health-insurance-india/')
soup = BeautifulSoup(html_doc,'lxml')
url_list=[]
titles=[]
for link in soup.find_all('a',{'class':'blueClr'}):
        url_list.append((link.get('href')))
        titles.append(link.string)

tables=[]
keys=[]
e=[[]]*22
d=[[]]
i=0
while i<len(e):
        for item in range(len(url_list[5:])):
            r=requests.get(url_list[5:][item])
            data=r.text
            soup = BeautifulSoup(data,'lxml')
            tables=soup.find('table')
    #e=[{}]
    #d=d*len(tables)
            for table in tables:
                    for tab in table:
        #e[table]={}
                        tab1=tab.find_all('tr')[0]
                        tab2=tab.find_all('tr')[1:]
                        col1=tab1.find_all('td')
        for j in range(len(col1)):
                e[i][col1[j].get_text()]=[]
        i+=1
                
                
