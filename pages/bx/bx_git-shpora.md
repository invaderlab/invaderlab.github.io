---
title: Git Шпаргалка | Список часто используемых команд
keywords: sample homepage
sidebar: bx_sidebar
folder: bx
permalink: bx_git-shpora.html
summary: false
toc: true
---

## Git Список часто используемых команд

=== Пошаговый учебник ===
https://githowto.com/ru/

=== Видеокурс ===
"Git для профессионалов" от http://pr-of-it.ru найдете при желании )

https://www.digitalocean.com/community/tutorials/git-ubuntu-14-04-ru

1) установка
sudo apt-get update
sudo apt-get install git

2) Первоначальная настройка
// установка данных пользователя
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"

// установка редактора по умолчанию
git config --global core.editor "subl -n -w"

// установка средства сравнения (https://nathanhoad.net/how-to-meld-for-git-diffs-in-ubuntu-hardy)
0.1) устанавливаем
# sudo aptitude install meld
0.2) создаем скрипт питона
#cd ~/scriptHelpers
#touch diff.py
-------------
#!/usr/bin/python

import sys
import os

os.system('meld "%s" "%s"' % (sys.argv[2], sys.argv[5]))
-------------
0.3) прописываем в настройках гита
git config --global diff.external ~/scriptHelpers/diff.py
#### что бы отменить эту настройку используем git config --global --unset diff.external

Проверить что настройки применились
git config --list

3) создание репозитория
git init

добавление удаленного репозитория к текушему
git remote add origin https://github.com/gdecider/tscc.git

проталкивание изменений в удаленный репозиторий
git push -u origin master

клонирование репозитория в текущую папку
git clone https://github.com/gdecider/tscc.git .

удаление файлов из подготовленных к коммиту
git rm --cached <file name>
если это папка, то добавляем флаг -r для рекурсивного удаления

(http://uleming.github.io/gitbook/4_%D0%9E%D1%82%D0%BC%D0%B5%D0%BD%D0%B0_%D0%B2_git_-_%D0%A1%D0%B1%D1%80%D0%BE%D1%81,_%D0%98%D0%B7%D0%B2%D0%BB%D0%B5%D1%87%D0%B5%D0%BD%D0%B8%D0%B5_%D0%B8_%D0%9E%D1%82%D0%BA%D0%B0%D1%82.html)
(https://www.prolinux.org/post/korotkii-spravochnik-po-git-komandam/)

git reset --hard HEAD
git clean -f

Это отбросит все сделанные изменения которые вы возможно добавили в индекс git, а также все другие изменения в вашей рабочем дереве. Другими словами, результат этого - вывод команд "git diff" и "git diff --cached" будет пустым.

About MELD http://meldmerge.org/help/

1) Installing Meld on Ubuntu (http://linuxpitstop.com/install-meld-on-ubuntu-and-mint-linux/)

sudo apt-get update
sudo apt-get install meld

--------------
настройки можно внести в глобальный файл настроек гита, который находится ~/.gitconfig
[user]
	name = decider_op
	email = decider@ya.ru
[core]
	editor = subl -n -w
[diff]
	tool = meld
[difftool]
	prompt = false
[merge]
	tool = meld
[mergetool]
	keepBackup = false

--------------------
или через команды

git config --global diff.tool meld
git config --global merge.tool meld
.
.
.
и т.д.


--- !!!то что ниже не проверено

git config --global mergetool.meld.trustExitCode false

// Fix git mergetool meld --help error
git config mergetool.meld.hasOutput true


Для доступа к репозиторию нужно добавить SSH ключ в настройках аккаунта github
https://help.github.com/articles/connecting-to-github-with-ssh/

0) Проверим есть ли ключ на ПК с которого нужно соединиться
ls -al ~/.ssh

1) Сгенерируем ключ, если нет существующего
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

На вопрос об имени файла можно оставить имя по умолчанию

На вопрос о пароле введите пароль или оставьте его пустым

2) Привязка ключа в аккаунт github
Для получения содержимомо ключа выведем его на экран

cat ~/.ssh/id_rsa.pub

Копируем то что вывелось в буфер обмена

Можно воспользоваться утилитой xcopy

В Вашем аккаунте GitHub идем в настройки, пункт SSH and GPG keys - New SSH key, вставляем скопированный ключ.


### Добавление информации о публичном ключе на сервер

#### Вариант 1

```sh
ssh-copy-id <user_name>@<server_ip_on_domain>
```

#### Вариант 2

```sh
cat ~/.ssh/<your_ssh_key_name>.pub | ssh <user_name>@<server_ip_on_domain> "mkdir -p ~/.ssh && cat >>  ~/.ssh/authorized_keys"
```


=== Обучающие видео
http://monsterlessons.com/project/categories/git

===
// Полезные алиасы git команд
https://habrahabr.ru/company/mailru/blog/318508/?utm_campaign=email_digest&utm_source=email_habrahabr&utm_medium=email_week_20170110&utm_content=link2post

// Моя шпаргалка по работе с Git
http://eax.me/git-commands/

https://githowto.com/ru/

* инициализация
git init

* добавление к будущему комиту
git add .
git add --all

* коммит
git commit -m"комментарий к комиту"

* пуш коммита в удаленный репозиторий
git push origin master

* получение данных из удаленного репозитория
git pull

* откатить не проиндексированный файл (до добавления в список перед коммита)
git checkout <filename>

* откатить проиндексированный файл (до коммита)
git reset HEAD <filename> // это сбросит проиндексированные файлы, но изменения в файле не откатятся
git checkout <filename> // это откатит сами изменения

* просмотр списка удаленных репозиториев
git remote -v

* изменение адреса удаленного репозитория
git remote set-url origin https://github.com/USERNAME/OTHERREPOSITORY.git

* просмотр веток
git branch

* просмотр всех веток вместе с удаленными
git branch -a

* просмотр только удаленных веток
git branch -r

* привязать локальную ветку к удаленной
git branch --set-upstream-to=origin/<branch> <local_branch_name>

* Удаление неотслеживаемых файлов ПРОСМОТР списка удалений
git clean -d -n

* Удаление неотслеживаемых файлов + те которые добавлены в игнор ПРОСМОТР списка удалений
!!! осторожно . удалит и файлы настроек, т.к. они всегда в игноре
git clean -d -n -x



* просмотр лога
https://git-scm.com/book/ru/v1/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%9F%D1%80%D0%BE%D1%81%D0%BC%D0%BE%D1%82%D1%80-%D0%B8%D1%81%D1%82%D0%BE%D1%80%D0%B8%D0%B8-%D0%BA%D0%BE%D0%BC%D0%BC%D0%B8%D1%82%D0%BE%D0%B2
git log
git log -p
git log --pretty=oneline --graph
git log --pretty=format:"%h - %an, %ar : %s"
gitk //это GUI утилита, в линукс потребуется установка через sudo apt-get install gitk

* список коммитов, сделанных за последние две недели
git log --since=2.weeks 
// так же можно указать дату например "2008-01-15", 
// Опция --author позволяет фильтровать по автору, опция --grep позволяет искать по ключевым словам в сообщении

