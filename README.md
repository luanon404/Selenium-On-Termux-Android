Selenium-On-Termux-Android
--------------------------

- This tutorial provides instructions on how to install and use Selenium on Termux for Android.
- I used ChatGPT to correct grama, because my english is not good, but that is not problem, enjoy!

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

- Type `termux-setup-storage`.
- Reopen the Termux app.
- Type `yes | pkg update -y && yes | pkg upgrade -y`.
- Type `pip install selenium`.

Installation
------------

- Although it mentions Android in the tutorial, it actually guides you to use WebDriver for Windows. You can try using VNC Server, and you will see that it is working with Windows, not Android. (Wrong, this not true, i will edit when i have time)

  <details>
  <summary>Selenium.</summary>
    <ul>

    <li>
    <details>
    <summary>Selenium Non-Headless.</summary>

    - Type ```curl -sLf https://raw.githubusercontent.com/Yisus7u7/termux-desktop-xfce/main/boostrap.sh | bash```.
    - Start the VNC server by typing ```vncserver -listen tcp```.
    - Download VNC Viewer from CH Play and use ```localhost:1``` as the address.

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

    ### Chrome Headless
    ```
    from selenium import webdriver
    options = webdriver.ChromeOptions()
    options.add_argument("--headless=new")
    driver = webdriver.Chrome(options=options)
    driver.get("https://www.google.com")
    driver.save_screenshot("/sdcard/download/screenshot.png")
    driver.quit()
    ```

    ### Non-headless Chrome
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

    ### Firefox Headless
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
    </li>

    </ul>
  </details>

  <details>
  <summary>Selenium & Appium (Don't try, updating).</summary>

    - Special thanks to [@mauro199304](https://github.com/mauro199304), [@remo7777](https://github.com/remo7777/), [@lzhiyong](https://github.com/lzhiyong) for this tutorial.
    - Tested on Android 9. You can also use commands like `adb install app.apk` without errors.

      [Image](https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/07e21df5-a0fd-41cd-b84a-76b3c2d5433f)

      ### Important
       - For those using this to control Firefox, I don't know why Firefox doesn't have the context to switch. Therefore, this feature only works with Chrome for now.

      ### Requirements
       - PC/Laptop to activate adb ***(If you turn off or restart your device, you must do this again)***.

      ### Required Libraries
      ```
      yes | pkg install nodejs -y
      npm install -g appium
      pip install Appium-Python-Client
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
      - Go to Settings.
      - Find Developer Mode.
      - Enable Developer Mode.
      - Enable USB connect.
      - Connect your phone to PC/Laptop using a USB cable.
      - On PC/Laptop, open the shell with administrator privileges.
      - Type `Get-ExecutionPolicy`.
      - If it returns `Restricted`, then type `Set-ExecutionPolicy AllSigned` or `Set-ExecutionPolicy Bypass -Scope Process`.
      - Type `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))`.
      - After installing Choco, type `choco install adb`.
      - Open the command prompt, type `adb tcpip 5555`.
      - From now on, you can unplug the USB cable connecting to the PC/Laptop.
      - Open Termux, type `ifconfig`, and remember your device's IPv4 address.

        ![Image](https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/58b5f7db-7422-40b8-b984-7ea3be0a6eae)

      - Type `adb kill-server`.
      - Type `adb connect <device IPv4>`.
      - Type `adb devices`. If you see your device's IPv4, then run `adb kill-server` again.
      - Type `appium` to run the adb server.
      - Try this test Python script.

        ```
        Updating...
        ```

      <details>
      <summary>Error Handling Solution</summary>

      - Version not supported:
        - This means you are using an old version of Appium, which does not support the current version.
        - Solution:
          - Type `npm ls -g --depth=0`. If `appium` is in this list, then type `npm uninstall -g appium`.
          - Otherwise, type `npm ls --depth=0`. If `appium` is in this list, then type `npm uninstall appium`.
          - Install again globally with `npm install -g appium --chromedriver-version="xxx.xxx.xxx.xxx"`, where xxx is your version.
          ![version](https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/c7bde0a4-e25c-407a-b7f3-05553318f133)
          - Then run Appium with the command `appium --allow-insecure chromedriver_autodownload`.

      - Can't switch context:
        - This means you can't switch context at the moment. I have never used Appium before, so I don't know why.
        - Solution:
          - Updating...

      </details>

  </details>

References
----------

- [Termux Desktop Xfce](https://github.com/Yisus7u7/termux-desktop-xfce)
- [Termux Issues](https://github.com/termux/termux-packages/issues/2149)
