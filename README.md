# web-crawler
#爬國稅局發票中獎資料
#發票週期

#

import requests
from bs4 import BeautifulSoup
import numpy as np
year_date = str(input("請輸入查詢年和奇數月:"))
if len(year_date)<=5:
   
    url = 'https://www.etax.nat.gov.tw/etw-main/ETW183W2_' + year_date
    headers = {'useragent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64} AppleWebKit/537.36(KHTML, likeGecko) Chrome/65.0.3342.181 Safari/537.36'}  #授權
    resp = requests.get(url, headers = headers)
    resp.encoding = 'utf-8'
    html_doc = resp.text
    soup = BeautifulSoup(html_doc, "lxml")   #解析器'lxml' //html.parser
    num_tags = soup.find_all("td")  #搜td的屬性
    p_tags = num_tags[5].find_all('div',class_="col-12 mb-3") #在td 和共通col-12 mb-3
    print('發票週期', year_date)
    print('特別獎:', num_tags[1].text.lstrip())
    print('特獎:', num_tags[3].text.lstrip())
    print('頭獎:', p_tags[0].text,p_tags[1].text.lstrip(), p_tags[2].text.lstrip())

    A = p_tags[0].text
    B = p_tags[1].text
    C = p_tags[2].text
    a = A.lstrip()
    b = B.lstrip()
    c = C.lstrip()
    print('增開六獎:',a[5:8])
    print('增開六獎:',b[5:8])
    print('增開六獎:',c[5:8])
