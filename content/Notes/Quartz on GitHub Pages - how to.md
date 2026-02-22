---
title: Quartz on GitHub Pages - how to
date: 2026-02-22
draft: false
tags: []
aliases:
---

# Инструкция: Как настроить Quartz сайт с GitHub Pages

На основе ваших заметок я подготовил полную инструкцию по настройке Quartz с публикацией на GitHub Pages.

## Что такое Quartz?

Quartz — это статический генератор сайтов, который позволяет работать с блогом так же, как вы работаете с базой заметок в Obsidian. [^1] Это особенно удобно, так как вы можете писать публикации прямо в Obsidian и публиковать их в интернет одной кнопкой, не выходя из приложения.

## Пошаговая инструкция

### Шаг 1: Создание репозитория на GitHub

1. Перейдите на [официальный репозиторий Quartz](https://github.com/jackyzha0/quartz.git)
2. Нажмите кнопку "Use this template" для создания своего репозитория из шаблона [^2]
3. Назовите репозиторий и создайте его

### Шаг 2: Настройка GitHub Pages и автоматического деплоя

1. Скопируйте файл конфигурации деплоя из примера: `.github/workflows/deploy.yaml` [^2]
2. Поместите этот файл в свой репозиторий по тому же пути
3. Это обеспечит автоматическую сборку и публикацию вашего сайта при каждом обновлении контента

`.github/workflows/deploy.yaml`:

```yaml
name: Deploy Quartz site to GitHub Pages
 
on:
  push:
    branches:
      - v4
 
permissions:
  contents: read
  pages: write
  id-token: write
 
concurrency:
  group: "pages"
  cancel-in-progress: false
 
jobs:
  build:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0 # Fetch all history for git info
      - uses: actions/setup-node@v4
        with:
          node-version: 22
      - name: Install Dependencies
        run: npm ci
      - name: Build Quartz
        run: npx quartz build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: public
 
  deploy:
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
### Шаг 3: Клонирование репозитория локально

1. Скачайте и установите [GitHub Desktop](https://desktop.github.com/download/) — это самый простой способ работы с Git [^2]
2. Откройте GitHub Desktop и клонируйте ваш репозиторий на компьютер
3. Выберите удобную папку для хранения проекта

### Шаг 4: Настройка Obsidian Vault

1. Откройте склонированный репозиторий как новый Vault в Obsidian [^2]
2. Установите плагин **Git** из встроенного магазина плагинов
3. Это позволит вам публиковать изменения прямо из Obsidian

### Шаг 5: Настройка авторизации GitHub (для macOS/Linux)

Чтобы плагин Git работал корректно, выполните следующие команды в терминале: [^2]

```bash
brew install gh
gh auth login
```

В процессе:
- Выберите HTTPS в качестве протокола
- Авторизуйтесь через браузер
- Введите код из терминала в браузер

После этого команда **Git: Create backup** в Obsidian будет успешно отправлять изменения в репозиторий.

### Шаг 6: Добавление контента

1. Поместите ваши заметки в папку `content` репозитория
2. Структурируйте их так же, как в вашем Obsidian Vault
3. Используйте стандартный формат Markdown

### Шаг 7: Публикация

1. В Obsidian откройте палитру команд (Cmd/Ctrl + P)
2. Выполните команду **Git: Create backup**
3. Ваши изменения будут отправлены на GitHub
4. GitHub Actions автоматически соберет и опубликует сайт

## Дополнительные возможности

### Изменение шрифтов

Если вы хотите кастомизировать внешний вид: [^3]

1. Поместите файл шрифта в `quartz/static/fonts`
2. Добавьте в `quartz/styles/custom.css`:

```scss
@font-face {
    font-family: 'MyFont';
    src: url('/static/fonts/myfont.ttf') format('truetype');
}

body {
    font-family: 'MyFont', sans-serif;
}
```

Чтобы также изменить шрифты заголовков и блоков кода, можно добавить: [^3]

```scss
h1, h2, h3, h4, h5, h6 {
    font-family: 'MyCustomFont', sans-serif;
}

code, pre {
    font-family: 'MyMonoFont', monospace;
}
```

### Подключение собственного домена

Вы можете подключить собственный домен к GitHub Pages. Инструкции доступны в официальной документации GitHub.

## Полезные команды

Если вы работаете с Quartz через командную строку: [^4]

```bash
# Запуск локального сервера для предпросмотра
npx quartz build --serve

# Обновление Quartz
npx quartz sync
```

## Советы по использованию

- Пишите заметки в Obsidian как обычно
- Используйте обратные ссылки — Quartz их отображает
- Регулярно коммитьте изменения через Git плагин
- Проверяйте результат на GitHub Pages после каждого обновления
