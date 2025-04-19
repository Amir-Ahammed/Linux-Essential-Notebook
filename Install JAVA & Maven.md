### Java Installation Steps:
* Update the Package List
  ```
  sudo apt update
  ```
* Download Java 18 using `wget`
  ```
  wget https://download.oracle.com/java/18/latest/jdk-18_linux-x64_bin.deb -O jdk-18.deb
  ```
* Install Java 18 | The second command ensures dependencies are installed correctly.
  ```
  sudo dpkg -i jdk-18.deb
  sudo apt install -f
  ```
* Verify Installation | Confirms Java 18 is installed.
  ```
  java -version
  ```
* Set Default Java Version (if needed) | Select Java 18 if multiple versions exist.
  ```
  sudo update-alternatives --config java
  ```
 



