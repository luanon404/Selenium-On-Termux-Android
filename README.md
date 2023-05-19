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
- Type ```yes | pkg update -y && yes | pkg upgrade -y```.
- Type ```pip install selenium```.

Install
-------

##### Install this if you want to use Non-headless mode ***(For Chrome, Firefox only, with appnium, you dont need install this)***.
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

<details>
<summary>Appnium</summary>

- Big thanks to [@mauro199304](https://github.com/mauro199304), [@remo7777](https://github.com/remo7777/), [@lzhiyong](https://github.com/lzhiyong) for this tutorial.
- Tested on Android 9, you can also use command like ```adb install app.apk``` without error.

https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/07e21df5-a0fd-41cd-b84a-76b3c2d5433f

#### Requirement
- PC/Laptop to active adb (only first time).

#### Requirement Library
```
yes | pkg install nodejs -y
npm install -g appium
pip install Appium-Python-Client
yes | pkg install wget -y
cd $HOME
wget https://github.com/Lzhiyong/termux-ndk/releases/download/android-sdk/android-sdk-aarch64.zip
unzip android-sdk-aarch64.zip -d android-sdk
rm -r android-sdk-aarch64.zip
echo "export ANDROID_HOME=/data/data/com.termux/files/home/android-sdk" >> ~/.bashrc
echo "export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools" >> ~/.bashrc
```

- After that, close termux and open again.

#### Step
- Enable Developer Mode.
- Enable USB connect.
- Connect your phone to PC/Laptop using usb plug.
- On PC/Laptop, open shell with administrator.
- Type ```Get-ExecutionPolicy```.
- If it returns ```Restricted```, then type ```Set-ExecutionPolicy AllSigned``` or ```Set-ExecutionPolicy Bypass -Scope Process```.
- Type ```Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))```.
- After install choco, type ```choco install adb```.
- Open cmd, type ```adb tcpip 5555```
- From now, you can unplug usb connect to PC/Laptop
- Open termux, type ```ifconfig```, save your device ip.

![ifconfig](https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/58b5f7db-7422-40b8-b984-7ea3be0a6eae)

- Type ```adb kill-server```
- Type ```adb connect <device ip>```.
- Type ```appium``` for run adb server.
- Try this test python script.

```

```

</details>

Reference
---------

- [Termux Desktop Xfce](https://github.com/Yisus7u7/termux-desktop-xfce)
- [Termux Issues](https://github.com/termux/termux-packages/issues/2149)
