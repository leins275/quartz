# fugitive vim 

[Самый популярный](https://vimawesome.com/) плагин для вима
https://github.com/tpope/vim-fugitive

# Фичи
## Можно вызывать команды гит в виме`:Git`
## Поддержка алиасов из `.gitconfig`
## Автокомплит веток
## Удобные сокращения команд 
```vim
:Gremove # :Git rm %
:Gmove   # :Git mv % target_path
:Gwrite  # :Git add %
:Gread   # :Git checkout %
```
## Команды для работы с индексом
- `:Gstatus`
	- `Ctrl+n/crtl+p` - перемещает между файлами
	- `-`  позволяет добавить или исключить файлы из индекса
	- `:Git add .` автоматически обновит вывод в окошке статуса
	- `p` Запустит `git add --patch` для текущего файла
	-  `C` - тоже что и `Gcommit`
- `Gedit` - working with index version of the file
- `Gdiff` - shows difference of working copy and index
	- `:diffput/:diffget` - Позволяют стейджить и чекаутить только патчи, а не весь файл целиком
	- `:diffupdate` - Обновляет выделение, если гит запутался
	- `'<,'>diffput` - for specific range of lines
## Резолвинг конфликтов
- `[c/]c` - перемещение в git diff между чанками
- `:only` - закрывает все окна кроме текущего
- `:ls` - показывает номера буферов для diffget