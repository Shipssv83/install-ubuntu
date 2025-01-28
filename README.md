Hi, ![](https://user-images.githubusercontent.com/18350557/176309783-0785949b-9127-417c-8b55-ab5a4333674e.gif)my name is Serhii Shypylov
=========================================================================================================================================

-------------------------------

### Socials
<p align="left">
  <a href="https://t.me/oneitpro">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/telegram-app.png" alt="Telegram" width="30" height="30" />
  </a>
  <a href="https://www.linkedin.com/in/sergey-shipilov-7262a31b4/">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/linkedin.png" alt="LinkedIn" width="30" height="30" />
  </a>
  <a href="https://www.instagram.com/shipssvpl/">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/instagram-new.png" alt="Instagram" width="30" height="30" />
  </a>
  <a href="https://www.facebook.com/profile.php?id=100083345006373">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/facebook.png" alt="Facebook" width="30" height="30" />
  </a>
  <a href="https://discord.com/invite/6z5EyagDyW?ref=1it.pro">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/discord.png" alt="Discord" width="30" height="30" />
  </a>
  <a href="mailto:admin@1it.pro">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/new-post.png" alt="Mail" width="30" height="30" />
  </a>
  <a href="https://1it.pro/">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/domain.png" alt="Website" width="30" height="30" />
  </a>
</p>
---
# install-ubuntu

```
#!/bin/bash
echo "
 SSSSSSS  EEEEEEE  RRRRRR   HHH   HHH IIIIIIII IIIIIIII
 SSS      EEE      RRR  RR  HHH   HHH    III     III
 SSSSSS   EEEEE    RRRRRR   HHHHHHHHH    III     III
     SSS  EEE      RRR  RR  HHH   HHH    III     III
 SSSSSSS  EEEEEEE  RRR   RR HHH   HHH IIIIIIII IIIIIIII

 SSSSSSS  HHH   HHH YYY   YYY PPPPPP   YYY   YYY LLL      OOOOOOO  VVV     VVV
 SSS      HHH   HHH  YYY YYY  PPP  PP   YYY YYY  LLL      OOO OOO   VVV   VVV
 SSSSSS   HHHHHHHHH   YYYYY   PPPPPP     YYYYY   LLL      OOO OOO    VVV VVV
     SSS  HHH   HHH    YYY    PPP        YYY     LLL      OOO OOO     VVVV
 SSSSSSS  HHH   HHH    YYY    PPP        YYY     LLLLLLL  OOOOOOO      VV

      11   iii tttttttt      pppppp  rrrrrrr   ooooooo
      11         ttt         pp   pp rr   rr  oo     oo
      11   iii   ttt   ..... pppppp  rr  rrr  oo     oo
      11   iii   ttt         pp      rr   rr  oo     oo
      11   iii   ttt         pp      rr    rr  ooooooo
"
#!/bin/bash

# Функция для вывода сообщений с форматированием
fancy_echo() {
  local fmt="$1"; shift
  printf "\n$fmt\n" "$@"
}

# Запрос пароля администратора
sudo -v

# Обработка ошибок
trap 'ret=$?; test $ret -ne 0 && printf "failed\n\n" >&2; exit $ret' EXIT

set -e

# Настройка репозиториев
configure_repositories() {
  fancy_echo "Adding necessary repositories..."
  # Добавление репозитория AnyDesk
  echo "deb http://deb.anydesk.com/ all main" | sudo tee /etc/apt/sources.list.d/anydesk.list
  wget -qO - https://keys.anydesk.com/repos/DEB-GPG-KEY | sudo apt-key add -

  # Добавление репозитория Google Chrome
  echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" | sudo tee /etc/apt/sources.list.d/google-chrome.list
  wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo tee /etc/apt/trusted.gpg.d/google.gpg

  # Добавление Flathub в Flatpak
  if [ ! -f /var/lib/flatpak/repo/flathub ]; then
    flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
  fi
}

# Установка необходимых пакетов
install_packages() {
  fancy_echo "Installing necessary packages..."
  sudo apt-get update
  sudo apt-get -y install vim python3 python3-pip openssh-server ufw ansible \
    gzip p7zip-rar cabextract unace rar expect openjdk-8-jdk ecryptfs-utils \
    cryptsetup gimp google-chrome-stable flameshot net-tools \
    speedtest-cli gnome-tweaks pritunl-client-electron dconf-editor flatpak \
    ubuntu-restricted-extras nautilus-admin exe-thumbnailer
}

# Установка пакетов из Snap
install_snap_packages() {
  fancy_echo "Installing snap packages..."
  sudo snap install telegram-desktop eversticky standard-notes teams-for-linux \
    postman bitwarden
}

# Установка AnyDesk
install_anydesk() {
  fancy_echo "Installing AnyDesk..."
  sudo apt-get update
  sudo apt-get -y install anydesk
}

# Настройка конфигурации SSHD
configure_sshd() {
  fancy_echo "Configuring SSH daemon..."

  sudo sed -i 's/^#\?PermitEmptyPasswords.*/PermitEmptyPasswords no/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?PermitUserEnvironment.*/PermitUserEnvironment no/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?PasswordAuthentication .*/PasswordAuthentication no/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?UsePAM.*/UsePAM no/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?X11Forwarding.*/X11Forwarding no/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?ClientAliveInterval.*/ClientAliveInterval 300/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?ClientAliveCountMax.*/ClientAliveCountMax 0/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?LogLevel.*/LogLevel VERBOSE/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?MaxAuthTries.*/MaxAuthTries 4/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?IgnoreRhosts.*/IgnoreRhosts yes/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?Protocol.*/Protocol 2/' /etc/ssh/sshd_config
  sudo sed -i 's/^#\?Banner.*/Banner \/etc\/issue.net/' /etc/ssh/sshd_config
}

# Основная логика
configure_repositories
install_packages
install_snap_packages
install_anydesk
setup_ssh
configure_sshd

fancy_echo "Done."
```
