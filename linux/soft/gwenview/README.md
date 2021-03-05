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

Файл **my_keys.shortcuts**, який можна імпортувати у програму

```ini
[Shortcuts]
add_folder_to_places=none
browse=Esc
crop=Shift+C
deletefile=Shift+Del
edit_copy=Ctrl+C; Ctrl+Ins
edit_cut=Ctrl+X
edit_location=F6
edit_paste=Ctrl+V; Shift+Ins
edit_redo=Ctrl+Shift+Z
edit_tags=Ctrl+T
edit_undo=Ctrl+Z
file_copy_to=C
file_create_folder=F7
file_link_to=F9
file_move_to=X
file_open=Ctrl+O
file_open_containing_folder=none
file_open_recent=none
file_open_with=none
file_print=Ctrl+P
file_quit=Q
file_rename=F2
file_restore=none
file_save=Ctrl+S
file_save_as=Ctrl+Shift+S
file_show_properties=none
file_trash=Del
flip=F
fullscreen=Ctrl+Shift+F; F11
go_first=Home; A
go_last=End; Z
go_next=Space; PgDown
go_previous=Backspace; PgUp
go_start_page=Alt+Home; Home Page
go_up=Alt+Up
help_about_app=none
help_about_kde=none
help_contents=F1
help_donate=none
help_report_bug=none
help_whats_this=Shift+F1
kipi_export=none
leave_fullscreen=none
mainToolBar=none
mirror=M
options_configure=Ctrl+Shift+,
options_configure_keybinding=none
options_configure_toolbars=none
options_show_menubar=Ctrl+M
options_show_statusbar=F3
rate_0=0
rate_1=1
rate_2=2
rate_3=3
rate_4=4
```
