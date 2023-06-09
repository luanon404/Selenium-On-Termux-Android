Selenium-On-Termux-Android
--------------------------

- This tutorial provides instructions on how to install and use Selenium on Termux for Android.
- I used ChatGPT to correct grama, because my english is not good, but that is not problem, enjoy!

Dont like english?
------------------

[![vietnamese](https://img.shields.io/badge/lang-vietnamese-red.svg)](https://github.com/luanon404/Selenium-On-Termux-Android/blob/main/README.vi.md)

Download
--------

- Termux -> [F-Droid](https://f-droid.org/packages/com.termux/).

Step
-----

- Choose the installation option you prefer.

  <details>
  <summary>Uninstall the current Termux and download/install the latest version.</summary>

  - Uninstall the current Termux app.
  - Install the new Termux app downloaded from F-Droid.
  - Open the Termux app.

  </details>

  <details>
  <summary>Keep my current Termux version and follow your instructions for installation.</summary>

  - Open the Termux app.

  </details>

- Run `termux-setup-storage`.
- Reopen the Termux app.
- Run `yes | pkg update -y && yes | pkg upgrade -y`.
- Run `pip install selenium`.

Installation
------------

- There are many types of selenium, the choice depends on your specific needs or requirements.

  <details>
  <summary>Using Selenium with a Headless Desktop WebDriver.</summary>

    - **Advantages:** `Instead of complex installations, just use the 'pkg' command`.
    - **Disadvantages:** `This does not have a GUI or 'graphical user interface'`.

    <ul>

    <li>
    <details>
    <summary>Chrome</summary>

    ### Required Libraries
    ```
    yes | pkg install x11-repo -y
    yes | pkg install tur-repo -y
    yes | pkg install chromium -y
    ```

    ### Example Chrome Headless
    ```
    from selenium import webdriver
    options = webdriver.ChromeOptions()
    options.add_argument("--no-sandbox")
    options.add_argument("--disable-dev-shm-usage")
    options.add_argument("--headless=new")
    driver = webdriver.Chrome(options=options)
    driver.get("https://www.google.com")
    driver.save_screenshot("/sdcard/download/screenshot.png")
    driver.quit()
    ```

    </details>
    </li>

    <li>
    <details>
    <summary>Firefox</summary>

    ### Required Libraries
    ```
    yes | pkg install x11-repo -y
    yes | pkg install firefox -y
    yes | pkg install geckodriver -y
    ```

    ### Example Firefox Headless
    ```
    from selenium import webdriver
    options = webdriver.FirefoxOptions()
    options.add_argument("--headless")
    driver = webdriver.Firefox(options=options)
    driver.get("https://www.google.com")
    driver.save_screenshot("/sdcard/download/screenshot.png")
    driver.quit()
    ```

    </details>
    </li>

    </ul>
  </details>

  <details>
  <summary>Using Selenium with a Non-Headless Desktop WebDriver.</summary>

    - **Advantages:** `Why 'Desktop'? Just try it, you will know why, this install only need to download a few additional things, it's not difficult at all`.
    - **Disadvantages:** `However, this still doesn't reach my goal. If you need to use Selenium to control Chrome or Firefox (Android), please follow the instructions below`.

      https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/4e5ed0bf-c1d8-4357-b034-9d0842f303b4

    <ul>

    <li>
    <details>
    <summary>Install VNC Server.</summary>

    - Run `curl -sLf https://raw.githubusercontent.com/Yisus7u7/termux-desktop-xfce/main/boostrap.sh | bash`.
    - At the end of installation, you will receive notice to input password, remember this password if you want login VNC Viewer from CH Play.
    - Start the VNC server by typing `vncserver -listen tcp`, for first time you will see it show something like `New 'localhost:1 ()' desktop is localhost:1`, then `localhost:1` is your display ip address.
    - You can download VNC Viewer from CH Play to view your webdriver, just use `localhost:1` as the ip address.

    </details>
    </li>

    <li>
    <details>
    <summary>Chrome</summary>

    ### Required Libraries
    ```
    yes | pkg install x11-repo -y
    yes | pkg install tur-repo -y
    yes | pkg install chromium -y
    ```

    ### Example Non-headless Chrome
    ```
    from selenium import webdriver
    options = webdriver.ChromeOptions()
    options.add_argument("--no-sandbox")
    options.add_argument("--disable-dev-shm-usage")
    options.add_argument("--display=:1") # localhost:1 -> display ID = 1
    driver = webdriver.Chrome(options=options)
    driver.get("https://www.google.com")
    driver.save_screenshot("/sdcard/download/screenshot.png")
    driver.quit()
    ```

    </details>
    </li>

    <li>
    <details>
    <summary>Firefox</summary>

    ### Required Libraries
    ```
    yes | pkg install x11-repo -y
    yes | pkg install firefox -y
    yes | pkg install geckodriver -y
    ```

    ### Example Non-headless Firefox
    ```
    from selenium import webdriver
    options = webdriver.FirefoxOptions()
    options.add_argument("--display=:1") # localhost:1 -> display ID = 1
    driver = webdriver.Firefox(options=options)
    driver.get("https://www.google.com")
    driver.save_screenshot("/sdcard/download/screenshot.png")
    driver.quit()
    ```

    </details>
    </li>

    </ul>
  </details>

  <details>
  <summary>Using Selenium with a Non-Headless Android WebDriver (adb required).</summary>

    https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/d4d3fd6d-f790-438d-8e66-28ca6e37c8a3

    ### Required Libraries
    ```
    yes | pkg install wget -y
    cd $HOME
    wget https://github.com/Lzhiyong/termux-ndk/releases/download/android-sdk/android-sdk-aarch64.zip
    unzip android-sdk-aarch64.zip -d android-sdk
    rm -r android-sdk-aarch64.zip
    echo "export ANDROID_HOME=$HOME/android-sdk" >> $HOME/.bashrc
    echo "export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools" >> $HOME/.bashrc
    ```

    - After that, close Termux and open it again ***(Make sure you killed all sessions)***.

    ### Step
    <details>
    <summary>First (very important), you need to enable adb server, there is 3 ways to do that.</summary>
    <ul>

    <li>
    <details>
    <summary>I have a rooted device.</summary>

    - Then this will be easy, run this command, you **dont** need PC/Laptop to enable adb server.

      ```
      su -c stop adbd && su -c start adbd
      su -c setprop service.adb.tcp.port 5555
      ```

    </details>
    </li>

    <li>
    <details>
    <summary>I have an Android phone running Android 11 and above.</summary>

    - From android 11 you **dont** need PC/Laptop to enable adb server on android. Watch this [video](https://youtu.be/NDAiJQxM7Fw) for how to enable adb server on android 11 and above. After install just scroll down, continue step.

    </details>
    </li>

    <li>
    <details>
    <summary>I have PC/Laptop</summary>

    - Go to your phone Settings.
    - Find Developer Mode.
    - Enable Developer Mode.
    - Follow me this step.

      ![settings_1](https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/27552cb2-560e-4e85-82c9-c494b05a71e3)

      ![settings_2](https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/ae1e36b4-dcf4-4e9f-920a-1c3781b089af)

    - If your device doesn't match or is not similar to my phone, then try [this solution](https://stackoverflow.com/questions/52079343/how-can-i-use-adb-to-grant-permission-without-root).
    - Connect your phone to PC/Laptop using a USB cable.
    - On PC/Laptop, open the shell with administrator privileges.
    - Next, you need to install Choco (This is a very easy way to install adb).
    - Run `Get-ExecutionPolicy`.
    - If it returns `Restricted`, then run `Set-ExecutionPolicy AllSigned` or `Set-ExecutionPolicy Bypass -Scope Process`.
    - Run `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))`.
    - After installing Choco, run `choco install adb`.
    - Open the command prompt on PC/Laptop, run `adb devices`.
    - Then continue run `adb tcpip 5555`.
    - \** And run this (I don't know if it's very important or not, but my Oppo phone needs this to run successfully) to allow termux write secure settings `adb shell pm grant com.termux android.permission.WRITE_SECURE_SETTINGS`.
    - From now on, you can unplug the USB cable connecting to the PC/Laptop.

    </details>
    </li>

    </ul>
    </details>

    - \--------------------------------------------------
    - Make sure you have enabled the adb server.
    - Open Termux.
    - Run `adb kill-server`.
    - Then run `adb devices`.
    - Make sure you only see `emulator-5554` in the list, with the attached `device`.

    ### Important
    - ***If you turn off or restart your device, you must enable adb server again***.
    - If you close termux app and open again, you need to active adb server by run `adb devices`.

    ### Chromium
    - [Download link](https://github.com/macchrome/droidchrome/tags) (current selenium only support chromium <= 110).
    - Or use this [link](https://github.com/macchrome/droidchrome/releases/download/v110.5481.153-M110.0.5481.153-r1191-Ungoogled-And64/arm64_ChromePublic_HEVC-110.0.5481.153.apk) for fast download.

      ```
      import os
      os.system("adb devices")
      from selenium import webdriver
      options = webdriver.ChromeOptions()
      options.add_argument("--no-sandbox")
      options.add_argument("--disable-dev-shm-usage")
      options.add_experimental_option("androidPackage", "org.chromium.chrome.stable")
      driver = webdriver.Chrome(options=options)
      driver.get("https://www.google.com")
      print("Page title:", driver.title)
      driver.quit()
      ```

  <details>
  <summary>Error Handling Solution.</summary>

  - **Missing java library:**
    - This indicates that you need to install Java.
    - Step
      ```
      cd $HOME
      wget https://github.com/lzhiyong/termux-ndk/releases/download/openjdk/openjdk-11.0.12-aarch64.zip
      unzip openjdk-11.0.12-aarch64.zip -d openjdk-11.0.12
      rm -r openjdk-11.0.12-aarch64.zip
      echo "export PATH=$PATH:$HOME/openjdk-11.0.12/bin" >> $HOME/.bashrc
      echo "export JAVA_HOME=$HOME/openjdk-11.0.12" >> $HOME/.bashrc
      ```

</details>

References
----------

- Special thanks to [@mauro199304](https://github.com/mauro199304), [@remo7777](https://github.com/remo7777/), [@lzhiyong](https://github.com/lzhiyong) for this tutorial.
- [Termux Desktop Xfce](https://github.com/Yisus7u7/termux-desktop-xfce)
- [Termux Issues](https://github.com/termux/termux-packages/issues/2149)
