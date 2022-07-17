#!/bin/python

import requests
from bs4 import BeautifulSoup as bs

social_req = requests.get("https://www.sas.ulisboa.pt/unidade-alimentar-tecnico-alameda", timeout=0.5)
content = social_req.text
soup = bs(content, features="lxml")

weekday = 2
for day in soup.findAll('div', attrs={"class":"menus"}):
    date = day.find("small", attrs={"class":"text-muted"}).get_text()
    print(str(weekday) + "ª - " + date)
    m = day.findAll("p", attrs={"class":"nome_prato"})

    if len(m) == 0:
        print("Nenhuma ementa disponível\n")
        weekday += 1
        continue

    print("Sopa: {}".format(m[0].get_text()))
    print("Prato: {}".format(m[1].get_text()))

    meals = [x.get_text() for x in day.findAll("h3")]
    if "Jantar" in meals:
        if len(m) == 4:
                print("Vegetariano: {}".format(m[2].get_text()))
        elif len(m) == 5:
                print("Prato: {}".format(m[2].get_text()))
                print("Vegetariano: {}".format(m[3].get_text()))

    else:
        if len(m) == 3:
                print("Vegetariano: {}".format(m[2].get_text()))
        elif len(m) == 4:
                print("Prato: {}".format(m[2].get_text()))
                print("Vegetariano: {}".format(m[3].get_text()))

    weekday += 1
    print()
