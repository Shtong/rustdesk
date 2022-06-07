<p align="center">
  <img src="logo-header.svg" alt="RustDesk - Votre bureau à distance"><br>
  <a href="#serveurs-publics-gratuits">Serveurs</a> •
  <a href="#étapes-générales-pour-la-compilation">Compilation</a> •
  <a href="#comment-compiler-avec-docker">Docker</a> •
  <a href="#structure-de-fichiers">Structure</a> •
  <a href="#captures">Captures d'écran</a><br>
  [<a href="README-CS.md">česky</a>] | [<a href="README-ZH.md">中文</a>] | [<a href="README-ES.md">Español</a>] | [<a href="README-FA.md">فارسی</a>] | [<a href="README-FR.md">Français</a>] | [<a href="README-DE.md">Deutsch</a>] | [<a href="README-PL.md">Polski</a>] | [<a href="README-ID.md">Indonesian</a>] | [<a href="README-FI.md">Suomi</a>] | [<a href="README-ML.md">മലയാളം</a>] | [<a href="README-JP.md">日本語</a>] | [<a href="README-NL.md">Nederlands</a>] | [<a href="README-IT.md">Italiano</a>] | [<a href="README-RU.md">Русский</a>] | [<a href="README-PTBR.md">Português (Brasil)</a>] | [<a href="README-EO.md">Esperanto</a>] | [<a href="README-KR.md">한국어</a>]<br>
  <b>Nous avons besoin de votre aide pour traduire ce README, <a href="https://github.com/rustdesk/rustdesk/tree/master/src/lang">RustDesk UI</a> et <a href="https://github.com/rustdesk/doc.rustdesk.com">la documentation</a> en Français.</b>
</p>

Rejoignez la discussion : [Discord](https://discord.gg/nDceKgxnkV) | [Twitter](https://twitter.com/rustdesk) | [Reddit](https://www.reddit.com/r/rustdesk)


[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/I2I04VU09)

Encore un logiciel de bureau à distance, écrit en Rust. Prêt à fonctionner, sans configuration requise. Vous gardez le contrôle complet de vos données, sans avoir à vous soucier de sécurité. Vous pouvez utiliser nos serveurs de contact/relais, [installer votre serveur personnel](https://rustdesk.com/server), ou [écrire votre propre serveur](https://github.com/rustdesk/rustdesk-server-demo).

![image](https://user-images.githubusercontent.com/71636191/171661982-430285f0-2e12-4b1d-9957-4a58e375304d.png)

## Restez au courant

<p align="center"><img src="https://github.com/AppFlowy-IO/appflowy/blob/main/doc/imgs/howtostar.gif" alt="AppFlowy Github" width="1000px" /></p>

RustDesk accepte toutes les contributions. Consultez [`CONTRIBUTING.md`](CONTRIBUTING.md) pour savoir comment participer.

[**Comment fonctionne RustDesk ?**](https://github.com/rustdesk/rustdesk/wiki/How-does-RustDesk-work%3F)

[**TÉLÉCHARGEMENTS BINAIRES**](https://github.com/rustdesk/rustdesk/releases)

## Serveurs publics gratuits

Les serveurs listés ci-dessous peuvent être utilisés gratuitement. Cette liste peut varier dans le temps. Si vous n'êtes pas situés près d'un d'eux, la connetion pourrait être plus lente.
| Emplacement | Fournisseur | Caractéristiques |
| --------- | ------------- | ------------------ |
| Séoul | AWS lightsail | 1 VCPU / 0.5GB RAM |
| Singapour | Vultr | 1 VCPU / 1GB RAM |
| Dallas | Vultr | 1 VCPU / 1GB RAM | |

## Dépendances

Les versions de bureau utilisent [sciter](https://sciter.com/) pour l'interface, merci de télécharger la bibliothèque dynamique sciter par vos propres moyens.

[Windows](https://raw.githubusercontent.com/c-smile/sciter-sdk/master/bin.win/x64/sciter.dll) |
[Linux](https://raw.githubusercontent.com/c-smile/sciter-sdk/master/bin.lnx/x64/libsciter-gtk.so) |
[MacOS](https://raw.githubusercontent.com/c-smile/sciter-sdk/master/bin.osx/libsciter.dylib)

Les versions mobiles utilisent Flutter. Nous avons prévu d'abandonner Sciter au profit de Flutter dans le futur pour les versions bureau.

## Étapes générales pour la compilation

- Préparez votre environnement de développement Rust, et votre environnement de compilation C++

- Installez [vcpkg](https://github.com/microsoft/vcpkg), et définissez correctement la variable `VCPKG_ROOT`

  - Windows: vcpkg install libvpx:x64-windows-static libyuv:x64-windows-static opus:x64-windows-static
  - Linux/MacOS: vcpkg install libvpx libyuv opus

- Lancez `cargo run`

## [Compilation](https://rustdesk.com/docs/en/dev/build/)

## Comment compiler sous Linux

### Ubuntu 18 (Debian 10)

```sh
sudo apt install -y g++ gcc git curl wget nasm yasm libgtk-3-dev clang libxcb-randr0-dev libxdo-dev libxfixes-dev libxcb-shape0-dev libxcb-xfixes0-dev libasound2-dev libpulse-dev cmake
```

### Fedora 28 (CentOS 8)

```sh
sudo yum -y install gcc-c++ git curl wget nasm yasm gcc gtk3-devel clang libxcb-devel libxdo-devel libXfixes-devel pulseaudio-libs-devel cmake alsa-lib-devel
```

### Arch (Manjaro)

```sh
sudo pacman -Syu --needed unzip git cmake gcc curl wget yasm nasm zip make pkg-config clang gtk3 xdotool libxcb libxfixes alsa-lib pulseaudio
```

### Installer la dépendance pynput

```sh
pip3 install pynput
```

### Installer vcpkg

```sh
git clone https://github.com/microsoft/vcpkg
cd vcpkg
git checkout 2021.12.01
cd ..
vcpkg/bootstrap-vcpkg.sh
export VCPKG_ROOT=$HOME/vcpkg
vcpkg/vcpkg install libvpx libyuv opus
```

### Corriger libvpx (pour Fedora)

```sh
cd vcpkg/buildtrees/libvpx/src
cd *
./configure
sed -i 's/CFLAGS+=-I/CFLAGS+=-fPIC -I/g' Makefile
sed -i 's/CXXFLAGS+=-I/CXXFLAGS+=-fPIC -I/g' Makefile
make
cp libvpx.a $HOME/vcpkg/installed/x64-linux/lib/
cd
```

### Compiler

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
git clone https://github.com/rustdesk/rustdesk
cd rustdesk
mkdir -p target/debug
wget https://raw.githubusercontent.com/c-smile/sciter-sdk/master/bin.lnx/x64/libsciter-gtk.so
mv libsciter-gtk.so target/debug
VCPKG_ROOT=$HOME/vcpkg cargo run
```

### Remplacer Wayland par X11 (Xorg)

RustDesk ne supporte pas Wayland. Consultez [ceci](https://docs.fedoraproject.org/en-US/quick-docs/configuring-xorg-as-default-gnome-session/) pour faire de XORG votre session GNOME par défaut.

## Comment compiler avec Docker

Commencez par cloner le repository et compiler le conteneur docker :

```sh
git clone https://github.com/rustdesk/rustdesk
cd rustdesk
docker build -t "rustdesk-builder" .
```

Ensuite, à chaque fois que vous avez besoin de compiler l'application, utilisez la commande suivante :

```sh
docker run --rm -it -v $PWD:/home/user/rustdesk -v rustdesk-git-cache:/home/user/.cargo/git -v rustdesk-registry-cache:/home/user/.cargo/registry -e PUID="$(id -u)" -e PGID="$(id -g)" rustdesk-builder
```

Notez que la première compilation peut prendre plus de temps pour la mise en cache des dépendances, et que que les compilations suivantes devraient être plus rapides. De plus, si vous avez besoin de spécifier d'autres arguments à la commande de compilation, vous pouvez le faire à la fin de la commande à l'emplacement des `<OPTIONAL-ARGS>`. Par exemple, pour compiler une version optimisée pour la production, on aurait exécuté la commande ci-dessus suivie de `--release`. L'exécutable généré sera disponible dans le répertoire target de votre système, et pourra être exécuté avec :

```sh
target/debug/rustdesk
```

Ou, pour démarrer un exécutable de production :

```sh
target/release/rustdesk
```

Assurez-vous de bien exécuter toutes ces commandes depuis la racine du repository RustDesk, ou l'application pourrait ne pas être capable de trouver les ressources nécessaires. Notez aussi que les sous-commandes cargo, comme `install` ou `run` ne sont pour l'instant pas supportées avec cette méthode, car elles installeraient ou démarreraient l'application dans le conteneur plutôt que dans l'hôte.

## Structure de fichiers

- **[libs/hbb_common](https://github.com/rustdesk/rustdesk/tree/master/libs/hbb_common)**: codec vidéo, configuration, wrapper tcp/udp, protobuf, fonctions fs pour les transferts de fichiers, et quelques autres fonctions utilitaires
- **[libs/scrap](https://github.com/rustdesk/rustdesk/tree/master/libs/scrap)**: capture d'écrans
- **[libs/enigo](https://github.com/rustdesk/rustdesk/tree/master/libs/enigo)**: contrôle de clavier/souris pour chaque plateforme
- **[src/ui](https://github.com/rustdesk/rustdesk/tree/master/src/ui)**: GUI
- **[src/server](https://github.com/rustdesk/rustdesk/tree/master/src/server)**: services audio/presse papier/entrées/vidéo, et connexions réseau
- **[src/client.rs](https://github.com/rustdesk/rustdesk/tree/master/src/client.rs)**: démarre une connexion à un pair
- **[src/rendezvous_mediator.rs](https://github.com/rustdesk/rustdesk/tree/master/src/rendezvous_mediator.rs)**: Communique avec [rustdesk-server](https://github.com/rustdesk/rustdesk-server), et attends les connections directes (TCP hole punching) ou relayées
- **[src/platform](https://github.com/rustdesk/rustdesk/tree/master/src/platform)**: code spécifique à chaque plate-forme
- **[flutter](https://github.com/rustdesk/rustdesk/tree/master/flutter)**: code Flutter pour mobile
- **[flutter/web/js](https://github.com/rustdesk/rustdesk/tree/master/flutter/web/js)**: code Javascript pour le client web Flutter

## Captures

![image](https://user-images.githubusercontent.com/71636191/113112362-ae4deb80-923b-11eb-957d-ff88daad4f06.png)

![image](https://user-images.githubusercontent.com/71636191/113112619-f705a480-923b-11eb-911d-97e984ef52b6.png)

![image](https://user-images.githubusercontent.com/71636191/113112857-3fbd5d80-923c-11eb-9836-768325faf906.png)

![image](https://user-images.githubusercontent.com/71636191/135385039-38fdbd72-379a-422d-b97f-33df71fb1cec.png)
