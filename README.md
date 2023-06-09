# lab02
## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [ ] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Выполнить инструкцию учебного материала
- [ ] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```

```sh
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

```sh
$ mkdir projects/lab02 && cd projects/lab02
$ git init
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
$ touch README.md
$ git status
$ git add README.md
$ git commit -m"added README.md"
$ git push origin master
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```

```sh
$ git pull origin master
$ git log
```

```sh
$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```sh
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```sh
$ edit README.md
```

```sh
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).

2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
```sh
mkdir lab02
$ echo "# lab02" >> README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git branch -M master
$ git remote add origin https://github.com/Alinoos/lab02.git
$ git push -u origin master
Username for 'https://github.com': Alinoos
Password for 'https://Alinoos@github.com': 
Перечисление объектов: 9, готово.
Подсчет объектов: 100% (9/9), готово.
При сжатии изменений используется до 8 потоков
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (9/9), 657 байтов | 657.00 КиБ/с, готово.
Всего 9 (изменений 0), повторно использовано 3 (изменений 0), повторно использовано пакетов 0
To https://github.com/Alinoos/lab02.git
 * [new branch]      master -> master
Ветка «master» отслеживает внешнюю ветку «master» из «origin».
```
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
```sh
$ cat >> hello_world.cpp <<EOF
> EOF
$ nano hello_world.cpp 

    Содержимое файла hello_world.cpp :
#include <iostream>

using namespace std;

int main(int argc, char** argv) {
   cout << "Hello world" << endl;
}
```

4. Добавьте этот файл в локальную копию репозитория.
```sh
$ git add hello_world.cpp
```

5. Закоммитьте изменения с *осмысленным* сообщением.
```sh
$ git commit -m "This is first file"
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Смотрите «git help gc» руководства по ручной очистке.
warning: The last gc run reported the following. Please correct the root cause
and remove .git/gc.log
Automatic cleanup will not be performed until the file is removed.
[master 94ea9b0] This is first file
 1 file changed, 7 insertions(+)
 create mode 100644 lab02/hello_world.cpp

```

6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
```sh
$ alias edit=subl
$ edit hello_world.cpp
      Новое содержание:
#include <iostream>
#include <string>
 
using namespace std;

int main(int argc, char** argv) {
   string name;
   cin >> name;
   cout << "Hello world from " << name << endl;
}      
```

7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
```sh
$ git commit -a -m "Changed cpp file"
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Смотрите «git help gc» руководства по ручной очистке.
warning: The last gc run reported the following. Please correct the root cause
and remove .git/gc.log
Automatic cleanup will not be performed until the file is removed.
[master 27f8a17] Changed cpp file
 1 file changed, 5 insertions(+), 2 deletions(-)
```

8. Запуште изменения в удалёный репозиторий.
```sh
$ git push -u origin master
Username for 'https://github.com': Alinoos
Password for 'https://Alinoos@github.com': 
Перечисление объектов: 9, готово.
Подсчет объектов: 100% (9/9), готово.
При сжатии изменений используется до 8 потоков
Сжатие объектов: 100% (6/6), готово.
Запись объектов: 100% (8/8), 781 байт | 781.00 КиБ/с, готово.
Всего 8 (изменений 1), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/Alinoos/lab02.git
   bfe71ed..27f8a17  master -> master
Ветка «master» отслеживает внешнюю ветку «master» из «origin».
```
9. Проверьте, что история коммитов доступна в удалёный репозитории.
```sh
The history of changes is available in the repository
```
### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
```sh
$ git checkout -b patch1
Переключились на новую ветку «patch1»

```
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
```sh
$ edit hello_world.cpp

    Новое содержание:
#include <iostream>
#include <string>
 
int main(int argc, char** argv){
  string name;
  std::cin >> name;
  std::cout << "Hello world from " << name << std::endl;
}
```

3. **commit**, **push** локальную ветку в удалённый репозиторий.
```sh

$ git commit -a -m "Fixed cpp file"
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Смотрите «git help gc» руководства по ручной очистке.
warning: The last gc run reported the following. Please correct the root cause
and remove .git/gc.log
Automatic cleanup will not be performed until the file is removed.
[patch1 6bdbb35] Fixed cpp file
 1 file changed, 5 insertions(+), 7 deletions(-)

$ git push -u origin patch1
Username for 'https://github.com': Alinoos
Password for 'https://Alinoos@github.com': 
Перечисление объектов: 21, готово.
Подсчет объектов: 100% (21/21), готово.
При сжатии изменений используется до 8 потоков
Сжатие объектов: 100% (12/12), готово.
Запись объектов: 100% (21/21), 1.77 КиБ | 1.77 МиБ/с, готово.
Всего 21 (изменений 1), повторно использовано 3 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (1/1), done.
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/Alinoos/lab02/pull/new/patch1
remote: 
To https://github.com/Alinoos/lab02.git
 * [new branch]      patch1 -> patch1
Ветка «patch1» отслеживает внешнюю ветку «patch1» из «origin».
```

4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
```sh
The patch1 branch is available in the remote repository
```
5. Создайте pull-request `patch1 -> master`.
```sh
Create a pull-request patch1 -> master
```
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
```sh
$ edit hello_world.cpp
    Измененный код:
#include <iostream>
#include <string>
 
int main(int argc, char** argv){
  string name;                                           // Name of @user
  std::cin >> name;                                      // Input name of @user
  std::cout << "Hello world from " << name << std::endl; // Output name of @user
} 
```
7. **commit**, **push**.
```sh
$ git commit -a -m "Code with comments"
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Смотрите «git help gc» руководства по ручной очистке.
warning: The last gc run reported the following. Please correct the root cause
and remove .git/gc.log
Automatic cleanup will not be performed until the file is removed.

warning: Имеется слишком много объектов, на которые нет ссылок; запустите «git prune» для их удаления.

[patch1 6f7a9eb] Code with comments
 1 file changed, 4 insertions(+), 4 deletions(-)

$ git push -u origin patch1
Username for 'https://github.com': Alinoos
Password for 'https://Alinoos@github.com': 
Перечисление объектов: 7, готово.
Подсчет объектов: 100% (7/7), готово.
При сжатии изменений используется до 8 потоков
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (4/4), 483 байта | 483.00 КиБ/с, готово.
Всего 4 (изменений 0), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
To https://github.com/Alinoos/lab02.git
   6bdbb35..6f7a9eb  patch1 -> patch1
Ветка «patch1» отслеживает внешнюю ветку «patch1» из «origin».

```
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
```sh
There are new changes in the pull-request created in step 5
```
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
```sh
$ git pull origin
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (11/11), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 8 (delta 1), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (8/8), 5.87 КиБ | 1.17 МиБ/с, готово.
Из https://github.com/Alinoos/lab02
   27f8a17..ceab48b  master     -> origin/master
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Смотрите «git help gc» руководства по ручной очистке.
warning: The last gc run reported the following. Please correct the root cause
and remove .git/gc.log
Automatic cleanup will not be performed until the file is removed.
Уже актуально.

```
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
```sh
$ git log master
//прикреплю скрины из-за длинного вывода
![изображение](https://github.com/Alinoos/lab02/assets/126507425/64f1d761-8e9f-4aab-98ca-ae443df7b378)
![изображение](https://github.com/Alinoos/lab02/assets/126507425/25080bfe-2a6a-4b0b-9a07-82940aedbe45)

```
12. Удалите локальную ветку `patch1`.
```sh
$ git checkout -b origin
Переключились на новую ветку «origin»
$ git branch -d patch1
Ветка patch1 удалена (была 6f7a9eb).
```
### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
```sh
$ git checkout -b patch2
Переключились на новую ветку «patch2»

$ git branch -d origin
Ветка origin удалена (была 6f7a9eb).

//В "Пункте 12" из второй части мы создали НОВУЮ ветку origin и переключились на неё, чтобы была возможноть удалить patch1
```
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
```sh
$ sudo apt install clang-format
[sudo] пароль для alina: 
Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово         
Уже установлен пакет clang-format самой новой версии (1:14.0-55~exp2).
Обновлено 0 пакетов, установлено 0 новых пакетов, для удаления отмечено 0 пакетов, и 228 пакетов не обновлено.

$ clang-format -i -style=Mozilla "hello_world.cpp"
```
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
```sh
$ git commit -a -m "Changed code style in cpp file"
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Смотрите «git help gc» руководства по ручной очистке.
warning: The last gc run reported the following. Please correct the root cause
and remove .git/gc.log
Automatic cleanup will not be performed until the file is removed.
[patch2 e63094a] Changed code style in cpp file
 1 file changed, 5 insertions(+), 3 deletions(-)

$ git push -u origin patch2
Username for 'https://github.com': Alinoos
Password for 'https://Alinoos@github.com': 
Перечисление объектов: 7, готово.
Подсчет объектов: 100% (7/7), готово.
При сжатии изменений используется до 8 потоков
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (4/4), 382 байта | 382.00 КиБ/с, готово.
Всего 4 (изменений 1), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/Alinoos/lab02/pull/new/patch2
remote: 
To https://github.com/Alinoos/lab02.git
 * [new branch]      patch2 -> patch2
Ветка «patch2» отслеживает внешнюю ветку «patch2» из «origin».
```
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
```sh
$ git checkout master
Переключились на ветку «master»

$ edit "Hello world.cpp"
    Измененный код:
#include <iostream>
#include <string>
 
int main(int argc, char** argv){
  string name;                                           // Имя пользователя
  std::cin >> name;                                      // Ввод имени пользователя
  std::cout << "Hello world from " << name << std::endl; // Вывод данных
} 

$ git pull origin master
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (3/3), 1.59 КиБ | 408.00 КиБ/с, готово.
Из https://github.com/Alinoos/lab02
 * branch            master     -> FETCH_HEAD
   ceab48b..f37af71  master     -> origin/master
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Automatic cleanup will not be performed until the file is removed.
Обновление 27f8a17..f37af71
Fast-forward
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Automatic cleanup will not be performed until the file is removed.
 README.md             | 431 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-
 lab02/hello_world.cpp |  12 +-
 2 files changed, 434 insertions(+), 9 deletions(-)

$ git push origin patch2
Username for 'https://github.com': Alinoos
Password for 'https://Alinoos@github.com': 
Everything up-to-date

```
5. Убедитесь, что в pull-request появились *конфликтны*.
![изображение](https://github.com/Alinoos/lab02/assets/126507425/9c8e3a34-f39c-411a-8893-9cef91e11f2e)

6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
```sh
$ git pull origin master
Из https://github.com/Alinoos/lab02
 * branch            master     -> FETCH_HEAD
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Обновление b910d75..1bb9f0b
Fast-forward
 lab02/hello_world.cpp | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)

$ edit hello_world.cpp
$ git commit -a -m "Update code"
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Смотрите «git help gc» руководства по ручной очистке.
warning: The last gc run reported the following. Please correct the root cause
and remove .git/gc.log
Automatic cleanup will not be performed until the file is removed.
[отделённый HEAD 8fbbbbf] Update code
 1 file changed, 1 insertion(+), 1 deletion(-)
```
7. Сделайте *force push* в ветку `patch2`
```sh
$ git checkout patch2
Переключились на ветку «patch2»
Эта ветка соответствует «origin/patch2».

$ git merge master
Обновление e63094a..ee86d04
Fast-forward
Автоматическая упаковка репозитория в фоне, для оптимальной производительности.
Смотрите «git help gc» руководства по ручной очистке.
 README.md             | 431 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-
 lab02/Hello world.cpp |   8 ++
 2 files changed, 437 insertions(+), 2 deletions(-)
 create mode 100644 lab02/Hello world.cpp

$ git add "hello_world.cpp"
$ git init
Инициализирован пустой репозиторий Git в /home/alina/lab02/.git/

$ git remote add origin https://github.com/Alinoos/lab02.git
$ git add .
$ git commit -a -m "Last fix"
[master (корневой коммит) 92c66c3] Last fix
 2 files changed, 18 insertions(+)
 create mode 100644 Hello world.cpp
 create mode 100644 hello_world.cpp

$ git checkout -b  patch2
Переключились на новую ветку «patch2»

$ git push -f origin patch2
Username for 'https://github.com': Alinoos
Password for 'https://Alinoos@github.com': 
Перечисление объектов: 4, готово.
Подсчет объектов: 100% (4/4), готово.
При сжатии изменений используется до 8 потоков
Сжатие объектов: 100% (4/4), готово.
Запись объектов: 100% (4/4), 511 байтов | 511.00 КиБ/с, готово.
Всего 4 (изменений 1), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/Alinoos/lab02.git
 + e63094a...92c66c3 patch2 -> patch2 (forced update)


```
8. Убедитель, что в pull-request пропали конфликтны. 
```sh
Conflicts have disappeared
```
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2021 The ISC Authors
```
