# Selenium-On-Termux-Android
Tutorial about how to install and use selenium on termux android.

Download
--------

Termux: [F-droid](https://f-droid.org/repo/com.termux_118.apk)

Step
-----

- Uninstall current termux app.
- Install new termux app downloaded from F-droid.
- Open termux app.
- Type ```termux-setup-storage```.
- Reopen termux app.
- Type ```yes | apt update -y && yes | apt upgrade -y```.

#### Requirement Library
```
yes | pkg install x11-repo -y
yes | pkg install tur-repo -y
yes | apt install xorg-server-xvfb -y
```

#### Chromium
```
yes | pkg install chromium -y
```

#### Firefox
```
yes | pkg install firefox -y
yes | apt install geckodriver -y
```

How to use
---------

- Type ```pip install pyvirtualdisplay```.
- Type ```pip install selenium```.

### Chromium headless
```
from selenium import webdriver
options = webdriver.ChromeOptions()
options.add_argument("--headless=new")
driver = webdriver.Chrome(options=options)
driver.get("https://www.google.com")
driver.save_screenshot("/sdcard/download/screenshot.png")
driver.quit()
```

### Non-headless Chromium
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

### Firefox headless
```
from selenium import webdriver
options = webdriver.FirefoxOptions()
options.add_argument("--headless")
driver = webdriver.Firefox(options=options)
driver.get("https://www.google.com")
driver.save_screenshot("/sdcard/download/screenshot.png")
driver.quit()
```

### Non-headless Firefox
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

[Termux Issues](https://github.com/termux/termux-packages/issues/2149)
