# multiple-PDF-download
PDF download project
%pip install selenium
%pip install webdriver-manager
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.by import By
import time
options = webdriver.ChromeOptions()

options.add_experimental_option('prefs',{
    'download.prompt_for_download': False,
    'plugins.always_open_pdf_externally': True
})

driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=options)
URL = "https://www.nmdpra.gov.ng/daily-truckout/"
driver.get(URL)
driver.implicitly_wait(3)

loadbutton = driver.find_element(By.XPATH, "//span[text()='Load More']")
for i in range(3):
    time.sleep(10)
    loadbutton.click()
    
buttons = driver.find_elements(By.CLASS_NAME, "elementor-button-text")
time.sleep(10)
for button in buttons:
    if button.text == 'Download PDF':
        button.click()
        time.sleep(0.2)
