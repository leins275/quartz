---
title: Обработка транзакций в google sheets
date: 01-09-2024
---
# Обработка транзакций из выгрузки Papara

1. При помощи следующих формул сделать все значения валидными числами
```
=SUBSTITUTE(C34, ".", "")
=SUBSTITUTE(D34, ",", ".")
```
2. Скопировать все значения из формул в новый столбец
