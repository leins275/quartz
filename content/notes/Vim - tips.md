---
title: Vim - tips
aliases: 
date: 2023-11-15
---

 - Текстовый объект `aw`. Удобен для удаления или редактирования всего слова.
 - Команды `<C-a>`  и `<C-x>` Выполняют сложение и вычитание. Число под курсором или после. Если используются со счетчиком, то складывают или вычитают, иначе просто инкремент/декремент. 
 - `"*y` - чтобы скопировать в регистр системного буфера

# Сохранить файл открытый без sudo
```
:w !sudo tee % > /dev/null
```
# Paste last yanked data after delete another
```bash
"0p
```

# Paste register to file
If you want to put in file content of the a register, do
```vim
"ap
```

# Apply macros to range of lines
```
:1,3normal @q
:%normal @q
```

# Выравнивание
`>, <, =` - отвечают за выравнивание в vim. При этом ,при помощи команды `gg=G` можно легко выровнять все содержимое файла автоматом!

# To copy selection to register a, select text and execute
```
"ay
```

- [[Текстовый редактор VIM]]
- [[Митап по Vim]]
- https://vim.fandom.com/wiki/Macros#Saving_a_macro