### Java Installation Steps:
* Update the Package List
  ```
  sudo apt update
  ```
* Download Java 18 using `wget`
  ```
  wget https://download.oracle.com/java/18/archive/jdk-18.0.2.1_linux-x64_bin.deb
  ```
* Extract the Archive.
  ```
  tar xvf openjdk-18_linux-x64_bin.tar.gz
  ```
* Move to /opt Directory
  ```
  sudo mv jdk-18 /opt/
  ```
* Set Environment Variables - Java Home
  ```
  export JAVA_HOME=/opt/jdk-18
  ```
* Set Environment Variables - Java Path
  ```
  export PATH=$JAVA_HOME/bin:$PATH
  ```
* Add the Java Path Manually - Open `vim ~/.bashrc` and Add these lines 
  ```
  export JAVA_HOME=/opt/jdk-18
  export PATH=$JAVA_HOME/bin:$PATH
  ```
* Verify Installation
  ```
  echo $JAVA_HOME
  java -version
  ```
* Set Default Java Version (if needed) | Select Java 18 if multiple versions exist.
  ```
  sudo update-alternatives --config java
  ```
 



