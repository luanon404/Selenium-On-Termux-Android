# Selenium-On-Termux-Android
Tutorial about how to install and use selenium on termux android.

Appnium
-------

- Big thanks to [@mauro199304](https://github.com/mauro199304) for this tutorial.

https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/07e21df5-a0fd-41cd-b84a-76b3c2d5433f

#### Requirement Library
- PC/Laptop to active adb (only first time).
- Enjoy!

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
- Type ```yes | pkg update -y && yes | pkg upgrade -y```.
- Type ```pip install selenium```.

Install
-------

##### Install this if you want to use Non-headless mode
- Type ```curl -sLf https://raw.githubusercontent.com/Yisus7u7/termux-desktop-xfce/main/boostrap.sh | bash```.
- Start vnc server ```vncserver -listen tcp```.
- Download VNC Viewer from CH Play, use ```localhost:1``` as address.

<details>
<summary>Chromium</summary>
  
#### Requirement Library
```
yes | pkg install x11-repo -y
yes | pkg install tur-repo -y
yes | pkg install chromium -y
```

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
options = webdriver.ChromeOptions()
options.add_argument("--display=:1")
driver = webdriver.Chrome(options=options)
driver.get("https://www.google.com")
driver.save_screenshot("/sdcard/download/screenshot.png")
driver.quit()
```

</details>

<details>
<summary>Firefox</summary>

#### Requirement Library
```
yes | pkg install x11-repo -y
yes | pkg install firefox -y
yes | pkg install geckodriver -y
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
options = webdriver.FirefoxOptions()
options.add_argument("--display=:1")
driver = webdriver.Firefox(options=options)
driver.get("https://www.google.com")
driver.save_screenshot("/sdcard/download/screenshot.png")
driver.quit()
```

</details>

Reference
---------

- [Termux Desktop Xfce](https://github.com/Yisus7u7/termux-desktop-xfce)
- [Termux Issues](https://github.com/termux/termux-packages/issues/2149)
