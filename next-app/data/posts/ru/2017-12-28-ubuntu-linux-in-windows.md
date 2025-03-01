---
title: Как работать с Linux используя Windows
subtitle: Инструкция по установке Ubuntu Linux внутри Windows с использованием различных технологий виртуализации.
description: Инструкция по установке Ubuntu Linux внутри Windows с использованием различных технологий виртуализации.
image: "/assets/images/ubuntu-linux-in-windows/virtualization_cover.png"
author: Кирилл Мокевнин
hidden: true
---

Если вы только начали свой путь разработчика и до сих используете операционную систему семейства Microsoft Windows, то уже наверняка столкнулись с ситуацией, когда ваш инструментарий отличается от того, что установлено у большинства людей из этой профессии. Чаще всего проблемы начинаются при работе в командной строке. Дело в том, что Windows не является [POSIX](https://ru.wikipedia.org/wiki/POSIX)-совместимой операционной системой, поэтому в ней отсутствует базовый набор прикладных программ, который необходим для разработки.

{% include banner.html name="intensive-devops" %}

Этот вопрос можно решить установкой какого-либо из многочисленных дистрибутивов Linux в качестве основной, либо альтернативной операционной системы. Для новичков есть способ проще и быстрее — технологии виртуализации. Об этом и поговорим.

## Ubuntu из Microsoft Store

Если вы работаете на Windows версии 10 с архитектурой x64, то можно можно воспользоваться встроенным решением и установить слой совместимости (Windows Subsystem for Linux) на основе Ubuntu Linux через магазин приложений Microsoft Store.

![Microsoft Store - Ubuntu](/assets/images/ubuntu-linux-in-windows/virtualization_1.png)

Перед тем как начать, необходимо убедиться, что системные требования соответствуют рекомендованным. Для этого запустите приложение Microsoft Store, введите в графе поиска Ubuntu и перейдите по найденной ссылке. Если ранее Windows не обновлялся, то вероятней всего вы получите соответствующее указание сделать это до начала установки Ubuntu.  Если всё OK, то нажимайте на кнопку «Получить» и через несколько минут (в зависимости от скорости интернет соединения) вы получите сигнал об успешной установке приложения.

Первый запуск может вызвать ошибку `Error: 0x8007007e` и предложение прочитать инструкцию по её решению [https://aka.ms/wslinstall](https://aka.ms/wslinstall). Если хотите сэкономить время, то просто запустите `PowerShell` (не путать с `cmd`) от имени администратора и выполните следующую команду:

```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

После этого компьютер попросит перегрузиться, а потом нужно снова запустить приложение Ubuntu.   В случае удачной установки откроется интерпретатор командной строки с предложением ввести имя пользователя и пароль. Выглядеть это будет вот так:

```
Installing, this may take a few minutes...
Installation successful!
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username:
```

Преимущество такого способа установки позволяют стереть грань между операционными системами и получить доступ ко всему инструментарию Linux (`bash`, `ssh`, `git`, `apt` и так далее) из стандартной командной строки Windows не теряя привычное окружение и оставаясь на одном файловом уровне.

Ссылки на официальную документацию:

* [Ubuntu - Microsoft Store](https://www.microsoft.com/ru-ru/store/p/ubuntu/9nblggh4msv6)
* [Install the Linux Subsystem on Windows 10 - Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

## VirtualBox

Если вы работаете на Windows версии ниже 10 или хотите получить изолированную операционную систему Linux, да ещё и с графическим окружением, то можно воспользоваться сторонним бесплатным программным продуктом под названием VirtualBox.

Вам потребуется:

* Инсталлятор Oracle VM VirtualBox для Windows Hosts
Ссылка на скачивание: [Download Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)

* Образ операционной системы Ubuntu Linux в формате ISO
Ссылка на скачивание: [Download Ubuntu Desktop](https://www.ubuntu.com/download/desktop)

Для начала необходимо установить и запустить приложение VirtualBox.

![VirtualBox главная страница](/assets/images/ubuntu-linux-in-windows/virtualization_2.png)

Нажимаем кнопку «Создать», выбираем из списка тип операционной системы «Linux», если нет своих предпочтений по дистрибутиву, то выбираем версию «Ubuntu» 32 или 64 битной архитектуры, а название можно ввести любое.

![VirtualBox создание виртуальной машины](/assets/images/ubuntu-linux-in-windows/virtualization_3.png)

Указываем объём оперативной памяти выделенной под виртуальную систему. Рекомендованный объём составляет 1024 MB.

![VirtualBox выбор размера оперативной памяти](/assets/images/ubuntu-linux-in-windows/virtualization_4.png)

Указываем объём дискового пространства выделенного под виртуальную систему. Рекомендованный объём составляет 10 GB.

![VirtualBox выбор жесткого диска](/assets/images/ubuntu-linux-in-windows/virtualization_5.png)

Тип виртуального жёсткого диска можно оставить как есть — VDI (VitrualBox Disk Image).

![VirtualBox выбор типа жесткого диска](/assets/images/ubuntu-linux-in-windows/virtualization_6.png)

Формат хранения данных выберите исходя из личных предпочтений. Динамический виртуальный жёсткий диск растёт по мере заполнения, а фиксированный создаётся сразу того размера, который был указан на предыдущем шаге.

![VirtualBox выбор формата хранения жесткого диска](/assets/images/ubuntu-linux-in-windows/virtualization_7.png)

Имя и размер файла можно оставить без изменений и сразу нажать на кнопку «Создать».

![VirtualBox выбор имени и размера жесткого диска](/assets/images/ubuntu-linux-in-windows/virtualization_8.png)

По завершению у вас будет создана виртуальная машина, но она пока без операционной системы. Для того чтобы её установить, нужно скачать Ubuntu Linux (32-bit или 64-bit, в зависимости от того, что было выбрано на шаге, где мы указывали тип ОС).

Нажатие на кнопку «Запустить» должно привести к появлению диалогового окна с предложением указать путь до скаченного ISO образа. Сделайте этого и нажмите кнопку «Продолжить»

![VirtualBox выбор загрузочного диска](/assets/images/ubuntu-linux-in-windows/virtualization_9.png)

Виртуальная машина автоматически будет выполнять часть процессов, но в некоторых операциях всё же потребуется участие пользователя.

Выберите языковую поддержку в списке слева и нажмите «Установить Ubuntu».

![ubuntu установка - выбор языка](/assets/images/ubuntu-linux-in-windows/virtualization_10.png)

Можно загрузить обновления сразу на этапе установки.

![ubuntu установка - загрузка обновлений](/assets/images/ubuntu-linux-in-windows/virtualization_11.png)

Без особых опасений выбираем пункт «Стереть диск и установить Ubuntu» и двигаемся дальше.

![ubuntu установка - очистка диска](/assets/images/ubuntu-linux-in-windows/virtualization_12.png)

Если вы выбрали русский язык на первом этапе установки, то вам предложат русскую раскладку клавиатуры в качестве дополнительной.

![ubuntu установка - выбор раскладки клавиатуры](/assets/images/ubuntu-linux-in-windows/virtualization_13.png)

Заполните поля и выберите режим входа в систему.

![ubuntu установка - ввод информации пользователя](/assets/images/ubuntu-linux-in-windows/virtualization_14.png)

Далее начнётся процедура разметки диска, переноса файлов, установка обновлений и другие процессы, которые не потребуют прямого участия пользователя.

![ubuntu процесс установки](/assets/images/ubuntu-linux-in-windows/virtualization_15.png)

По завершению виртуальный компьютер перезагрузится и вы попадёте в уже установленную среду Ubuntu Linux.

Но это ещё не всё. Весьма желательно установить так называемые «Дополнения гостевой ОС». Они содержат драйверы и прочие системные файлы, необходимые для наилучшей производительности и обеспечения дополнительных функциональных возможностей между виртуальной и гостевой операционными системами.

Выберите пункт меню «Устройства» программы VitrualBox, подпункт «Подключить образ диска Дополнений гостевой ОС…» и дождитесь предложение запустить приложение для автоматического запуска с виртуального привода.

![VitrualBox подключение образа диска дополнений](/assets/images/ubuntu-linux-in-windows/virtualization_16.png)

Виртуальная ОС Ubuntu Linux установлена и готова к работе.

Ссылка на официальную документацию: [Oracle VM VirtualBox User Manual](https://www.virtualbox.org/manual/)

---

*Дмитрий Храпонов*
