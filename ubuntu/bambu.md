sudo apt update
sudo apt install flatpak

sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

flatpak install flathub com.bambulab.BambuStudio

flatpak run com.bambulab.BambuStudio