## Мои опыты

Пример, когда подключаемый раздел FAT32:

`sudo mount /dev/sda4 /mnt/backup -t vfat -o rw,uid=olex,gid=olex,umask=133,dmask=022,noatime,nofail`

для него можно задать пользователя и разрешения файлов, которые поменять нельзя. При

- `umask=133,dmask=022` - файлы - 0644, директории - 0755
- `umask=111,dmask=000` - файлы - 0666, директории - 0777

Если подключаемый раздел EXT4 - он всегда будет от _root_, поэтому обычный пользователь linux вносить изменения не сможет.
Но можно создать директорию(-ии) от root'а, выполнить `chown user:user dirname` - и для пользователя _user_ не будет ограничений на запись.

### Мой fstab

```
UUID=e4f020f4-f3b7-4e5a-92ed-7f8c61963a52    /       ext4   errors=remount-ro,noatime,dirnoatime 0       1
UUID=37cf61e0-a7eb-457a-9501-493832973f7e    /home   ext4   defaults,noatime,dirnoatime          0       2
UUID=b011adbb-f42c-4098-9ebc-484c9266a838    somedir ext4   noauto,noatime,dirnoatime            0       2
UUID=f4c5fc6e-9c7f-4976-be3b-63d0dcead3f1    none    swap   sw                                   0       0
```
![?](/i/qu.png) Не совсем понятно... Когда в **fstab** прописать точку монтирования `/media/somedir` - то linux (lite) показывает на рабочем столе непримонтированный диск.  
А если просто `somedir` (как в верху), то диск после загрузки не отображается. При монтировании монтируется в корень `/somedir`.

{% include f.htm f="my_exp.md" %}
