# Gwenview

Gwenview - функциональный, гибко настраиваемый просмотрщик изображений из KDE. Но его можно установить и в других окружениях, например в XFCE - Manjaro (Arch Linux), Lite Linux (Ubuntu, Debian).

В Arch'е, вместе с Gwenview, по умолчанию устанавливается библиотека kimageformats, которая позволяет Gwenview "понимать" файлы .PSD

    kimageformats (optional) - support for dds, xcf, exr, psd, and more image formats

Но в Lite Linux (вероятно, Ubuntu тоже) она не ставится по умолчанию и, к тому же, имеет немного другое название: kimageformat-plugins. При необходимости ее нужно устанавливать дополнительно.

```
apt search kimageformat
...
kimageformat-plugins/bionic,now 5.44.0-0ubuntu1 amd64
  additional image format plugins for QtGui

sudo apt install kimageformat-plugins
Кстати, после ее установки, Okular - просмотрщик .PDF из KDE, также стал открывать файлы, созданные Photoshop.
```
