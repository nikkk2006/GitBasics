# Основы Git и Git Bash

**Основные команды Git Bash:**
1.  pwd - узнать где я сейчас
2.  cd ~ - перейти к домашней директории
3.  cd c:/ - перейти в корневую директорию
4.  cd - сменить директорию
5.  cd .. - вернуться в род. директорию
6.  ls - вывести содержимое
7.  ls -a - вывести расширенное содержимое touch - создать файл
8.  mkdir - создать папку
9.  cp - скопировать файл
10. mv - переместить файл
11. cat - прочитать текстовый файл
12. rm - удаление файла
13. rmdir - удаление пустой директории
14. rm -r - удаление директории с содержимым && - выполнить несколько команд
15. echo " " - выводи в консоль, что написано в кавычках
16. echo " " >> file - записывает в конец файла, что написано в кавычках
17. echo " " > file - перезаписывает файл на то, что написано в кавычках

**Основные команды Git:**
1.  git version - версия git
2.  git config --global user.name/user.email " "/
3.  git config list - содержимое файла .gitconfig
4.  git init - создание git репозитория
5.  rm -rf .git - разгитить папку
6.  git status - проверить состояние репозитория
7.  git add - добавление файла в отслеживание
8.  git add --all - добавляет все файлы для отслеживания
9.  git add . - добавление всей папки в отслежку
10. git commit -m " " - добавление коммита с комментом
11. git log - история коммитов
12. ssh-keygen -t ed25519 -C "<my_email>" - генерация ssh-пары
13. clip < ~/.ssh/id_rsa.pub - копирование ssh-ключа
14. git remote add origin <SSH_from_GITHUB> - привязка удалённого репозитория к локальному
15. git push -u origin master - загружает на удаленный репозиторий коммит,
в первый раз эту команду надо вызывать с флагом -u(связывает локальную ветку с удалённой) и origin, master
16. git log --oneline - история коммитов, но в одну строку
17. git commit -a -m " " - добавление коммита с комментом минуя staging area
18. git diff - сравнивает поселднюю версию закоммиченного файла с той, что в modified
19. git diff --staged - покажет изменения в staged-файлах от-но последних закоммиченных версий
20. git diff hash_first hash_second - покажет разницу между двумя коммитами
21. git status --ignored - проверить состояние репозитория с игрорируемыми файлами
22. git clone <SSH> - клонирует удалённый репозиторий.
23. git branch - узнать кол-во веток(звёздочкой отмечено в какой ветке я нахожусь).
24. git branch <BRANCH_NAME> - создать ветку с именем BRANCH_NAME.
25. git checkout <BRANCH_NAME> - перейти в ветку с именем BRANCH_NAME.
26. git checkout -b <BRANCH_NAME> - создать ветку BRANCH_NAME и перейти в неё.
27. git merge <BRANCH_NAME> - объединение ветки.
28. git branch -D <BRANCH_NAME> - удаление ветки BRANCH_NAME.
29. git branch -d <BRANCH_NAME> - удаление ветки в случае если она объединена с другой.
30. git merge --no-ff <BRANCH_NAME> - слияние веток с отключением fast forward
31. git config [--global] merge.ff false - отключение слияния fast forward навсегда.
32. git log --graph - отображение коммитов и веток звёздочками и палочками(типо граф).
33. git push --force - форсированный пуш.

## Хеш
**Хеш - это идентификатор коммита.** Каждый коммит имеет свой уникальный хеш, состоящий из 40 символов.
При помощи команды git log мы наблюдали историю коммитов. Так вот в этой истории у каждого коммита 
есть свой хеш, автор коммита, дата коммита и сообщение коммита.
При вызове команды git log с флогом --oneline хеш будет выводить в сокращенной форме, который тоже уникален.
Вместо полного хеша можно спокойно использовать сокращённый.

## Статусы в GIT
Бывают статусы: **untracked/tracked, staged, modified**
- Файл имеет статус **untracked** если он не отслеживается, т.е. git не видит все его изменения
- Файл имеет статус **staget** если он был добавлен при помощи команды git add. 
После этого файл переходит в staging area т.е. он готов к коммиту
- Файл имеет статус **tracked** если он либо был добавлен в staging area, либо уже был закомичен.
- Файл имеет статус **modified** если он уже отслеживается git-ом и был изменен.

## Как исправить коммит?
1. git commit --amend --no-edit - команда, которая изменит коммит при этом сообщение коммита останется неизменным.
Файлы, которые нужно добавить в изменённый коммит должны быть в staging area.
2. git commit --amend -m " " - команда, которая изменит коммит при этом сообщение тоже изменится.
Файлы, которые нужно добавить в изменённый коммит должны быть в staging area.

## Как откатиться назад?
1. git restore --staged <file> - команда, которая убирает файл из staging area
2. git restore --staged - команда, которая убирает все файлы из staging area
3. git reset --hard <commit hash> - команда, которая откатывает до коммита.
commit hash - это хеш коммита, до которого нужно откатиться.
4. git restore <file> - команда, которая откатывает изменения, которые не попали ни в staging area, ни в коммит(т.е. в modified).

## Оформление .gitignore
**.gitignore — это обычный текстовый файл. Его добавляют в корень репозитория и тоже коммитят.**
Правила из **.gitignore** применяются только к новым **(untracked)** файлам.
Если файл уже попал в **staging area** или в коммит, то правила на него не распространяются.
### Комментарий
Если строка начинается с **#**, то это комментарий, и **.gitignore** не будет его учитывать.
```Bash
# это комментарий в .gitignore, он ничего не значит
```
### Игнорирование файла
Если нужно, чтобы **.gitignore** игнорировал файл во всех папках(не только в корневой):
```Bash
# игнорирование всех файлов с названием .txt
.txt
```
### Использование *
Если нужно, чтобы **.gitignore** игнорировал файл во всех папках(не только в корневой) с каким-то расширением(напримет .txt):
```Bash
# игнорирование всех файлов с расширением .txt
*.txt
```
Если нужно, чтобы **.gitignore** игнорировал все файлы(как бы это странно не было):
```Bash
# странное правило, но всё же
# данная команда игнорирует абсолютно все файлы
*
```
### Отличие .txt и *.txt
Различие заключается в том, что **.txt** просто соответствует файлу с именем **.txt**,
в то время как ***.txt** соответствует любому файлу с расширением **.txt**.
### Вопросительный знак **(?)**
Вопросительный знак **?** соответствует одному любому символу:
```Bash
# Будет проигнорировано text1.txt, textA.txt, но text12.txt не будет проигнорирован!!
text?.txt
```
### Квадратные скобки **([…])**
Квадратные скобки соответствуют одному символу. При этом символ не любой, а только из списка, который указан в скобках.
В скобках можно либо перечислить символы **([abc])**, либо задать диапазон **([a-z])**:
```Bash
# Будет проигнорировано text1.txt, text2.txt
text[1-2].txt
# Будет проигнорировано textA.txt, textb.txt
text[Ab].txt
```
### Слеш **(/)**
Если шаблон в **.gitignore** начинается со слеша, то **Git** проигнорирует файлы или каталоги только в корневой директории.
```Bash
# игнорировать text.txt в корне репозитория
/text.txt
# для сравнение about.txt будет игнорироваться во всех папках
about.txt
```
Если шаблон заканчивается слешем, то правило применится только к папке.
```Bash
# если это папка, то она проигнорируется, но если файл то нет!!
build/
```
### Парные звёздочки (**)
Функция парных звёздочек (**) похожа на функцию одинарной (*).
Отличие в том, как они работают с вложенными папками. Двойная звёздочка может соответствовать любому количеству таких папок (в том числе нулю).
Одинарная может соответствовать только одной:
```Bash
# Будет проигнорировано docs/old/tmp, docs/a/b/tmp, docs/tmp и т.д.
docs/**/tmp
# Будет проигнорировано docs/old/tmp, но не docs/a/b/tmp(ибо вложённость > 1 папки)
docs/*/tmp 
```
### Восклицательный знак **(!)**
С помощью ! можно инвертировать:
```Bash
# Игнорировать все файлы с расширением .jpeg
*.jpeg
# Кроме doge.jpeg
!doge.jpeg
```
