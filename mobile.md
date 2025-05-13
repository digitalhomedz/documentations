# Buil mobile Commands
## Build with expo servers:
pull from dev:
git checkout dev
git pull
eas build --platform android
wait for 20 minutes


## Build with digital home servers:
ssh-keygen -t ed25519 -f ~/.ssh/mobile_key -C "deploy@vps"

cat ~/.ssh/mobile_key.pub

put it in githb Deploy keys
nano ~/.ssh/config
```
# Second GitHub identity (alias)
Host mobile
  HostName github.com
  User git
  IdentityFile ~/.ssh/mobile_key
  IdentitiesOnly yes

Host front_customers
  HostName github.com
  User git
  IdentityFile ~/.ssh/front_customers
  IdentitiesOnly yes

Host back_customers
  HostName github.com
  User git
  IdentityFile ~/.ssh/back_customers
  IdentitiesOnly yes
```

git clone git@mobile:nailKhaled/DH-Mobile-App.git Mobile-App

cd Mobile-App

npm install expo@51

sudo apt install npm

sudo apt install openjdk-17-jdk unzip wget -y

mkdir -p $HOME/Android/Sdk

cd $HOME/Android/Sdk

wget https://dl.google.com/android/repository/commandlinetools-linux-10406996_latest.zip

unzip commandlinetools-linux-*.zip -d cmdline-tools

cd cmdline-tools

mv cmdline-tools latest

export ANDROID_HOME=$HOME/Android/Sdk

export PATH=$ANDROID_HOME/cmdline-tools/latest/bin:$PATH

export PATH=$ANDROID_HOME/platform-tools:$PATH

export PATH=$ANDROID_HOME/emulator:$PATH

source ~/.bashrc

sdkmanager --sdk_root=$ANDROID_HOME "platform-tools" "platforms;android-34" "build-tools;34.0.0" "emulator"

cd ~/Mobile-App

nano ~/.bashrc

  138  ls
