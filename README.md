# CM6206-Catalina
CM6206 Driver for MacOS Catalina 10.15

Thanks to: https://www.dr-lex.be/software/cm6206.html

## Compile 
* Open xcode Project and click play button 
* Click show finder for product and get your **cm6206int** file  

## Installation 

If you have Catalina get a tool that can unlock I use [Hackintool](https://github.com/headkaze/Hackintool). 

Click to unlock

![Imgur](https://i.imgur.com/2whO5kc.png)

Input your account password

![Imgur](https://i.imgur.com/zus6Pvr.png)

Run 

0. copy cm6206init file into the git. Then, cd into the location of downloaded package
  
1. ``sudo mkdir /Library/Application\ Support/CM6206``

2. ``sudo ./fixperm.sh``

3. ``sudo cp cm6206init /Library/Application\ Support/CM6206``

4. ``sudo cp Installer/be.dr-lex.cm6206init.plist /Library/LaunchDaemons``

5. Restart 
