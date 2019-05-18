# lab02
Part I

    Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
    Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
    Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку using namespace std;.

$ cd homework
$ mkdir sources
$ cd sources/
$ cat > hello_world.cpp <<EOF
> #include <string>
> #include <iostream>
> 
> using namespace std;
> 
> int main() {
>   cout << "Hello world!";
>   return 0;
> }
> EOF
$ cd ..
    Добавьте этот файл в локальную копию репозитория.

$ git status
На ветке master
Ваша ветка обновлена в соответствии с «origin/master».

Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)

	sources/

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)
$ git add sources/

    Закоммитьте изменения с осмысленным сообщением.

$ git commit -m "Meaningful message"

    Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя.

$ nano sources/hello_world.cpp 

    Закоммитьте новую версию программы. Почему не надо добавлять файл повторно git add?

$ git commit -m"Another meaningful message"
На ветке master
Ваша ветка опережает «origin/master» на 1 коммит.
  (используйте «git push», чтобы опубликовать ваши локальные коммиты)

Изменения, которые не в индексе для коммита:
	изменено:      sources/hello_world.cpp

нет изменений добавленных для коммита
$ git add sources/hello_world.cpp 
$ git commit -m"Another meaningful message"

    Запуште изменения в удалёный репозиторий.

$ git push origin master

    Проверьте, что история коммитов доступна в удалёный репозитории.

Part II

Note: Работать продолжайте с теми же репоззиториями, что и в первой части задания.

    В локальной копии репозитория создайте локальную ветку patch1.

$ git checkout -b patch1

    Внесите изменения в ветке patch1 по исправлению кода и избавления от using namespace std;.

$ nano sources/hello_world.cpp

    commit, push локальную ветку в удалённый репозиторий.

$ git add .
$ git commit -m "Codestyle fixes"
$ git push origin patch1

    Проверьте, что ветка patch1 доступна в удалёный репозитории.
    Создайте pull-request patch1 -> master.
    В локальной копии в ветке patch1 добавьте в исходный код комментарии.

$ nano sources/hello_world.cpp 

    commit, push.

$ git add .
$ git commit -m "Added commentaries"
$ git push origin patch1

    Проверьте, что новые изменения есть в созданном на шаге 5 pull-request
    В удалённый репозитории выполните слияние PR patch1 -> master и удалите ветку patch1 в удаленном репозитории.
    Локально выполните pull.

$ git pull
Ваша конфигурация указывает, что нужно слить изменения со ссылкой
«refs/heads/patch1» из внешнего репозитория, но такая ссылка не была получена.
$ git checkout master
$ git pull

    С помощью команды git log просмотрите историю в локальной версии ветки master.

$ git log master

    Удалите локальную ветку patch1.

$ git branch -d patch1

Part III

Note: Работать продолжайте с теми же репоззиториями, что и в первой части задания.

    Создайте новую локальную ветку patch2.

$ git checkout -b patch2

    Измените code style с помощью утилиты clang-format. Например, используя опцию -style=Mozilla.

$ clang-format -i -style=Mozilla sources/hello_world.cpp

    commit, push, создайте pull-request patch2 -> master.

$ git add .
$ git commit -m "Changed codestyle with clang"
$ git push origin patch2

    В ветке master в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
    Убедитесь, что в pull-request появились конфликты.
    Для этого локально выполните pull + rebase (точную последовательность команд, следует узнать самостоятельно). Исправьте конфликты.

$ git pull
$ nano sources/hello_world.cpp
$ git add .
$ git commit -m"Fix"
$ git rebase master
$ nano sources/hello_world.cpp
$ git add .
$ git rebase --continue
$ git pull origin master

    Сделайте force push в ветку patch2

$ git push -f origin patch2

    Убедитель, что в pull-request пропали конфликтны.
    Вмержите pull-request patch2 -> master.
