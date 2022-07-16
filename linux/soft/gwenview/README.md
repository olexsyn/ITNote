# Gwenview

Gwenview - функціональний, з гнучким налаштуванням переглядач зображень від KDE. Але його можна встановити і в інших оточеннях, наприклад, у XFCE.

https://userbase.kde.org/Gwenview/uk

## Встановлення

{% include cl.htm cmd="sudo apt install gwenview" %}

Якщо ваше оточення не KDE, будьте готові, що разом з Gwenview буде встановлено багато KDE-бібліотек, необхідних для фунціювання програми.

## KImageFormats

[Бібліотека плагінів](https://api.kde.org/frameworks/kimageformats/html/index.html), які дозволяють програмам підтримувати додаткові формати файлів.

Підтримується читання таких форматів зображень:

- Animated Windows cursors (ani)
- Gimp (xcf)
- OpenEXR (exr)
- Photoshop documents (psd, psb, pdd, psdt)
- Sun Raster (ras)

Наступні формати зображень підтримують як читання, так і запис:

- AV1 Image File Format (AVIF)
- Encapsulated PostScript (eps)
- JPEG XL (jxl)
- Personal Computer Exchange (pcx)
- SGI images (rgb, rgba, sgi, bw)
- Softimage PIC (pic)
- Targa (tga): supports more formats than Qt's version
- XView (xv)

В деяких дистрибутивах Linux вона **не встановлюється за умовчанням**, тому за потреби її необхідно встановити.

Спочатку треба з'ясувати, яку назву вона має у вашому оточенні:

{% include cl.htm cmd="apt search kimageformat"
out="<b>kimageformat-plugins</b>/jammy,now 5.92.0-0ubuntu1 amd64 [installed]
  Додаткові втулки форматів зображень для QtGui" %}

наприклад, в Ubuntu ця бібліотека має назву **kimageformat-plugins**. І встановити її:

{% include cl.htm cmd="sudo apt install kimageformat-plugins" %}

Після встановлення, також і Okular (переглядач .PDF з KDE), почав відкривати файли, створені Photoshop.

## Гарячі клавіші

У Linux Lite 6.0, (не знаю, як справи у батьківської Ubuntu 22.04) Gwenview встановлюється без жодної "гарячої" комбінації і працює лише через меню та панелі кнопок. Це можна виправити, створивши і завантаживши файл-схему (`Параметри` -> `Налаштувати клавіатурні скорочення` -> `Керування схемами` -> `Додаткові дії` -> `Імпортувати схему`)

Файл **gwenview.shortcuts**, який можна імпортувати у програму:

```ini
[Shortcuts]
add_folder_to_places=none
align_with_sidebar=none
browse=Esc
crop=Shift+C
deletefile=Shift+Del
edit_copy=Ctrl+C; Ctrl+Ins
edit_cut=Ctrl+X; Shift+Del
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
file_print=none
file_quit=Q
file_rename=F2
file_restore=none
file_save=Ctrl+S
file_save_as=Ctrl+Shift+S
file_show_properties=Alt+Return
file_trash=Del
flip=Shift+H
fullscreen=Ctrl+Shift+F; F11
go_first=Home; A
go_last=End; Z
go_next=Space; PgDown
go_previous=Backspace; PgUp
go_start_page=Alt+Home; Home Page
go_up=Alt+Up
hamburger_menu=none
help_about_app=none
help_about_kde=none
help_contents=F1
help_donate=none
help_report_bug=none
help_whats_this=Shift+F1
leave_fullscreen=none
mainToolBar=none
mirror=Ctrl+H
open_kcommand_bar=Ctrl+Alt+I
options_configure=Ctrl+Shift+,
options_configure_keybinding=Ctrl+Alt+,
options_configure_toolbars=none
options_show_menubar=Alt+M
options_show_statusbar=F3
rate_0=none
rate_1=none
rate_2=none
rate_3=none
rate_4=none
rate_5=none
red_eye_reduction=Shift+E
reload=F5; Refresh
replace_location=none
resize=Shift+R
rotate_left=Ctrl+L
rotate_right=Ctrl+R
share=none
sort_desc=none
switch_application_language=none
synchronize_views=Ctrl+Y
toggle_operations_sidebar=none
toggle_sidebar=F4
toggle_slideshow=none
toggle_thumbnailbar=Ctrl+B
view=none
view_actual_size=0
view_background_colormode_auto=none
view_background_colormode_dark=none
view_background_colormode_light=none
view_background_colormode_neutral=none
view_toggle_birdeyeview=none
view_zoom_in=Ctrl++; Ctrl+=
view_zoom_out=Ctrl+-
view_zoom_to_fill=Shift+F
view_zoom_to_fit=F
```

див.
- /home/olex/.config/gwenviewrc
- /home/olex/.local/share/kxmlgui5/gwenview/gwenviewui.rc


