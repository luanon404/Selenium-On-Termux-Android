# Selenium-On-Termux-Android
Tutorial about how to install and use selenium on termux android.

Download
------

Termux: [F-droid](https://f-droid.org/repo/com.termux_118.apk)

Step
-----

#### Step 1
Uninstall current termux app.

#### Step 2
Install new termux app downloaded from F-droid.

#### Step 3
Open termux app.

#### Step 4
Type ```termux-setup-storage```.

#### Step 5
Reopen termux app.

#### Step 6
Type ```yes | apt update -y && yes | apt upgrade -y```.

#### Step 7
Type

##### Chromium
```
yes | pkg install tur-repo -y
yes | pkg update -y
yes | pkg install chromium -y
```

##### Firefox
```
yes | pkg install x11-repo -y
yes | pkg update -y
yes | pkg install firefox -y
yes | apt install geckodriver -y
```

#### Step 8
Type ```pip install pyvirtualdisplay```.

#### Step 9
Type ```pip install selenium```.

### Chromium headless ###
```
from selenium import webdriver
options = webdriver.ChromeOptions()
options.add_argument("--headless=new")
driver = webdriver.Chrome(options=options)
driver.get("https://www.google.com")
driver.save_screenshot("/sdcard/download/screenshot.png")
driver.quit()
```

### Non-headless Chromium ###
```
from selenium import webdriver
from pyvirtualdisplay import Display
display = Display(visible=0, size=(1920, 1080))
display.start()
options = webdriver.ChromeOptions()
options.add_argument("--no-sandbox")
options.add_argument("--disable-dev-shm-usage")
driver = webdriver.Chrome(options=options)
driver.get("https://www.google.com")
driver.save_screenshot("/sdcard/download/screenshot.png")
driver.quit()
display.stop()
```

### Firefox headless ###
```
from selenium import webdriver
options = webdriver.FirefoxOptions()
options.add_argument("--headless")
driver = webdriver.Firefox(options=options)
driver.get("https://www.google.com")
driver.save_screenshot("/sdcard/download/screenshot.png")
driver.quit()
```

### Non-headless Firefox ###
```
from selenium import webdriver
from pyvirtualdisplay import Display
display = Display(visible=0, size=(1920, 1080))
display.start()
options = webdriver.FirefoxOptions()
options.add_argument("--no-sandbox")
options.add_argument("--disable-dev-shm-usage")
driver = webdriver.Firefox(options=options)
driver.get("https://www.google.com")
driver.save_screenshot("/sdcard/download/screenshot.png")
driver.quit()
display.stop()
```

Reference
---------

[Termux issues](https://github.com/termux/termux-packages/issues/2149)
