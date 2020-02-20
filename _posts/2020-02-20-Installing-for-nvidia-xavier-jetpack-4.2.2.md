
Created: 2020 Feb 20

# Pycharm

(link)[https://www.jetbrains.com/pycharm/download/#section=linux]

1. Download Community edition.
2. Open terminal
3. cd Downloads
4. tar -xzf pycharm-community-2018.1.4.tar.gz
5. cd pycharm-community-2018.1.4
6. cd bin
7. sh pycharm.sh

# Java jdk

  1. apt-cache search openjdk 
  2. sudo apt-get install openjdk-8-jdk 
  3. java -version 
  4. which javac 
  5. file /usr/bin/javac 
  6. file /etc/alternatives/javac 
  7. file /usr/lib/jvm/java-8-openjdk-arm64/bin/java
  8. sudo gedit ~/.bashrc
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-arm64
    export JRE_HOME=${JAVA_HOME}/jre
    export CLASSPATH=:${JAVA_HOME}/lib:${JRE_HOME}/lib
    export PATH=${JAVA_HOME}/bin:$PATH
  9. source ~/.bashrc

# Install setup tools

> For Python 2.x:
  sudo apt-get install python-setuptools
> For Python 3.x:
  sudo apt-get install python3-setuptools

# Install pip

> Python 2.7
  sudo apt-get install -y python-pip python-dev
> Python 3.5
  sudo apt-get install -y python3-pip python3-dev

# Install Scipy 

  pip3 install --upgrade setuptools
  sudo pip3 install -U setuptools
  sudo apt-get install libpcap-dev libpq-dev
  sudo pip3 install cython
  pip install scipy
  
> If it has any errors such as: AttributeError: module 'enum' has no attribute 'IntFlag. Make sure to uninstall enum 
  by:
  
  pip freeze | grep enum34
  pip uninstall -y enum34
  
  and then reinstall again Scipy.
