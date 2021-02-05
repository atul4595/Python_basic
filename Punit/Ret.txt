def replace_p(b):
    list12 = ["\n", "/", "-"]
    #     print(list12)
    for re in list12:
        #         print(re)
        b = b.replace(re, " ")
    #         print(b)
    b = b.replace(" ", "")
    return b


from bs4 import BeautifulSoup
# requests module is easy to operate some people use urllib but I prefer this one because it is easy to use.
import requests
import lxml
import re

list1 = []
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.149 Safari/537.36'}
url = 'https://www.amazon.in/s?k=watches&ref=nb_sb_noss_2'
response = requests.get(url, headers=headers)
# print(response)
# The retrieved answer can be viewed by running:
# print(response.text)
soup = BeautifulSoup(response.content, features="lxml")
with open("output.txt", "w", encoding='utf-8') as file:
    file.write(str(soup))
for i in soup.find_all("a", {"class": "a-link-normal a-text-normal"}):
    url2 = ""
    response2 = ""
    soup1 = ""
    Title = ""
    a = ""
    file1 = ""
    filename = ""
    url2 = "https://www.amazon.in" + str(i.get('href'))
    response2 = requests.get(url2, headers=headers)
    #     print(response2)
    soup1 = BeautifulSoup(response2.content, features="lxml")
    print(soup1.title)
    if soup1.find(id="productTitle") is None:
        continue
    Title = soup1.find(id="productTitle")
    print(Title)
    filename = re.sub('[^A-Za-z0-9]+', '', str(Title))
    with open(str(filename) + ".html", "w", encoding='utf-8') as file1:
        file1.write(str(soup1))

# i=soup.find_all("a", {"class": "a-link-normal a-text-normal"})[0]
# url2="https://www.amazon.in"+str(i.get('href'))
# response2 = requests.get(url2, headers=headers)
# # print(response2)
# soup1 = BeautifulSoup(response2.content, features="lxml")
# with open("output1.txt", "w",encoding='utf-8') as file1:
#     file1.write(str(soup1))
# print(soup1)
# print(type(soup1))
# b=str(soup1)
# print(type(b))
# # print(b)
# with open('atul1.txt','a') as data:
#     data.write(b)
# print(soup.find_all("h2")[14].find_all('a')[0])
# for i in soup.find_all("h2", {"class": "top-cat"}):
#     a=i.find_all('a')[0]
#     print(a.get('href'))