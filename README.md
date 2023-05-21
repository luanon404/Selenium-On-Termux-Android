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

- There are many types of selenium, the choice depends on your specific needs or requirements.

  <details>
  <summary>Using Selenium with a Headless WebDriver.</summary>

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

    <ul>

    <li>
    <details>
    <summary>Install VNC Server.</summary>

    - Type `curl -sLf https://raw.githubusercontent.com/Yisus7u7/termux-desktop-xfce/main/boostrap.sh | bash`.
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
  <summary>Using Selenium with a Headless Android WebDriver.</summary>

  - Special thanks to [@mauro199304](https://github.com/mauro199304), [@remo7777](https://github.com/remo7777/), [@lzhiyong](https://github.com/lzhiyong) for this tutorial.
  - Tested on Android 9. You can also use commands like `adb install app.apk` without errors.
  - Some devices like OPPO (my current phone) may not be able to use this method due to insufficient permissions for adb (must root). In such cases, please choose either option 1 or 2 instead.

    [Image](https://github.com/luanon404/Selenium-On-Termux-Android/assets/71830807/07e21df5-a0fd-41cd-b84a-76b3c2d5433f)

    ### Requirements
    - PC/Laptop to activate adb ***(If you turn off or restart your device, you must do this again)***.

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
    - Open the command prompt, type `adb devices`.
    - \** Just run this to allow termux write secure setting `adb shell pm grant com.termux android.permission.WRITE_SECURE_SETTINGS`.
    - From now on, you can unplug the USB cable connecting to the PC/Laptop.
    - Type `adb devices`. If you see something like IPv4, then type `adb kill-server`.
    - Make sure you only see `emulator-5554` from list.
    - Try running this test Python script (Chrome). For Firefox, it seems that you need to download the driver from [this link](https://github.com/mozilla/geckodriver/releases/tag/v0.33.0). I'm not sure about the installation process, but I will update you later.

      ```
      from selenium import webdriver
      chrome_options = webdriver.ChromeOptions()
      chrome_options.add_experimental_option("androidPackage", "com.android.chrome")
      driver = webdriver.Chrome(options=chrome_options)
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

    - **ADB clearing user data is forbidden:**
      - This indicates that you need to root device.
      - Step
        ```
        There are many tutorial about root, but I don't recommend doing that, use option 1 or 2 instead.
        ```

  </details>

References
----------

- [Termux Desktop Xfce](https://github.com/Yisus7u7/termux-desktop-xfce)
- [Termux Issues](https://github.com/termux/termux-packages/issues/2149)
