## Как пользоваться


<br>

ACL (`Access Control Lists`) в Linux — инструмент для гибкого управления правами доступа. Он позволяет предоставлять разрешения нескольким пользователям и группам для одного и того же файла или каталога.

**Для установки `ACL`** применяется команда `setfacl`:

```ruby
setfacl [options] operation entity:entityname:permissions file
```

Некоторые опции команды: `-d` — устанавливает ACL по умолчанию, который наследуется подкаталогами и файлами; `-k` — удаляет список ACL по умолчанию; `-R` — рекурсивно применяет настройки ACL.

Для получения информации о списках ACL применяется команда getfacl, которой передаётся имя файла или каталога:

```ruby
getfacl file
```

Пример установки ACL для каталога `"/somedir"`:

```ruby
setfacl -m g:users:rwx /somedir
```

В этом случае для группы `"users"` `(g)` устанавливаются разрешения `"rwx"`, то есть разрешения на чтение, запись и выполнение.

Также можно установить ACL сразу для нескольких пользователей/групп:

```ruby
setfacl -d -m g:users:rwx,g:developers:rx /somedir
```

Эта команда устанавливает ACL по умолчанию для папки `"/somedir"`, причём группа `"users"` получает разрешения `"rwx"`, а группа `"developers"` — `"rx"`.

<br>

**Для удаления правил ACL** в Linux используется команда `setfacl`.

Параметр `-x` позволяет удалить правило для пользователя или группы. Например, чтобы убрать права доступа к файлу `secretfile` для пользователя `test`, нужно выполнить команду 
```ruby
setfacl -x u:test secretfile
```

Опция `-b` предназначена для удаления всех ACL-правил. После выполнения команды с этим параметром, если проверить ACL каталога с помощью `getfacl`, то не будет никаких записей `ACL`. Пример команды: 

```ruby
setfacl -b /company/shared
```
