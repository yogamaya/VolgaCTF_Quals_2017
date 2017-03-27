<h1>Nested</h1>

There are too many bytes to be a simple transfer... can you investigate this?
dump.7z

Hints

1. Take a look at the source format and continue making y**our guess**es
2. gzsteg


Скачиваем архив dump.7z. В архиве один файл - dump.pcap. Откроем в Wireshark. 

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-29-34.png)

Ничего особенного.
По описанию таска понимаем, что надо обратить внимание на исходный формат файла. Копаем в направление архивов.
Поищем сигнатуры архивов в dump.pcap.
Откроем в bless. Перебрав несколько сигнатру zip-архивов, находим сигнатуру 7z-архива.

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-32-14.png)

Извлекаем файлы.

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-37-04.png)

По названию файлов (each other) догадываемся, что они как-то относятся друг к другу. Наверно они являются ключами друг для друга.
Изходя из существующих утилит для скрытия информации в JPEG и подсказки к таску, решаем, что нам нужна утилита outguess.
Устанавливаем.
Но нам нужен ключ, чтобы извлечь скрытую информацию. Догадываемся, что ключ в названии второго файла.

Выполняем команду

`outguess -k "other" -r each.jpg hidden.txt`

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-38-17.png)

Пароль к архиву other.zip.

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-38-48.png)

Извлечённый файл - gz-архив.

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-39-40.png)

И тут нам понадобится gzsteg. Чтобы им воспользоваться, необходимо пропатчить gzip версии 1.2.4. В интернете можно найти всю необходимую информацию.

Следующей командой извлекаем файл:
`gzip -cds hide.txt hide.gz`

В файле hide.txt флаг.

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-42-17.png)
