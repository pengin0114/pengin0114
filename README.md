
from selenium import webdriver
from selenium.webdriver.common.by import By
from time import sleep


driver=webdriver.Firefox()


url = 'https://scraping-for-beginner.herokuapp.com/login_page'

driver.get(url)

elem_username =driver.find_element(By.ID,"username")
elem_username.send_keys('imanishi')
elem_password =driver.find_element(By.ID,"password")
elem_password.send_keys('kohei')
sleep(3)
elem_login_btn=driver.find_element(By.ID,'login-btn')
elem_login_btn.click()


elems_th=driver.find_elements(By.TAG_NAME,'th')

keys=[]
for elem_th in elems_th:
    key=elem_th.text
    keys.append(key)



elems_td=driver.find_elements(By.TAG_NAME,'td')

values=[]
for elem_td in elems_td:
    value=elem_td.text
    values.append(value)


import pandas as pd

df=pd.DataFrame()

df['項目']=keys
df['値']=values

df.to_csv('講師情報.csv',index=False)
