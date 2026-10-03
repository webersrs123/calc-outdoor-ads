# Git Cheatsheet

**Автор:** Илья Ткачев  
**GitHub:** [webersrs123](https://github.com/webersrs123)  
**Email:** webersrs123@gmail.com

---

## 0. Быстрый доступ

- [1. Первичная настройка](#1-первичная-настройка)
- [2. Создание репозитория](#2-создание-репозитория)
- [3. Ежедневный цикл](#3-ежедневный-цикл)
- [4. Ветки](#4-ветки)
- [5. Слияние ветки в main](#5-слияние-ветки-в-main)
- [6. Откат изменений](#6-откат-изменений)
- [7. История](#7-история)
- [8. Работа с двумя репо](#8-работа-с-двумя-репо)
- [9. Типичные ошибки](#9-типичные-ошибки)
- [10. Минимальный цикл](#10-минимальный-цикл)

---

## 1. Первичная настройка

Выполняется **один раз** на машине.

```bash
git config --global user.name "Илья Ткачев"
git config --global user.email "webersrs123@gmail.com"
```

Проверка:

```bash
git config --global --list
```

---

## 2. Создание репозитория

Выполняется **один раз** на проект.

### Шаг 1. На GitHub

Создать **пустой** репозиторий:
- без README
- без .gitignore
- без лицензии

Скопировать URL вида `https://github.com/webersrs123/repo-name.git`.

### Шаг 2. Локально (в папке проекта)

```bash
git init
git remote add origin https://github.com/webersrs123/repo-name.git
git branch -M main
```

### Шаг 3. Первый коммит и пуш

```bash
git add .
git commit -m "Initial commit"
git push -u origin main
```

---

## 3. Ежедневный цикл

**99% работы.** Запомнить эти четыре команды.

```bash
git status
```
Посмотреть, что изменилось.

```bash
git add .
```
Добавить все изменения.

```bash
git add path/to/file.js
```
Добавить конкретный файл.

```bash
git commit -m "Описание"
```
Зафиксировать.

```bash
git push
```
Отправить на GitHub.

**Правило:** один коммит = одно логически завершённое изменение. Не «куча всего», а «добавил функцию расчёта выезда». Сомневаешься — коммить чаще.

---

## 4. Ветки

### Зачем

`main` всегда стабильна. Новую фичу делаешь в отдельной ветке, потом сливаешь.

### Создать ветку и переключиться

```bash
git checkout -b feature/travel-fee
```

### Посмотреть ветки

```bash
git branch
```
Локальные.

```bash
git branch -a
```
Включая удалённые.

### Переключиться на существующую

```bash
git checkout main
git checkout feature/travel-fee
```

### Отправить ветку на GitHub (первый раз)

```bash
git push -u origin feature/travel-fee
```

Дальше — просто `git push`.

---

## 5. Слияние ветки в main

### Способ 1: через GitHub (рекомендую)

1. Пушишь ветку:

```bash
git push -u origin feature/travel-fee
```

2. На GitHub появляется кнопка **Compare & pull request**.
3. Создаёшь PR, смотришь diff, мержишь кнопкой.
4. Локально подтягиваешь:

```bash
git checkout main
git pull
git branch -d feature/travel-fee
```

### Способ 2: локально

```bash
git checkout main
git pull
git merge feature/travel-fee
git push
git branch -d feature/travel-fee
```

---

## 6. Откат изменений

### Отменить изменения в файле (до коммита)

```bash
git checkout -- path/to/file.js
```

### Убрать файл из staging (файл остаётся)

```bash
git reset path/to/file.js
```

### Отменить последний коммит, сохранить изменения

```bash
git reset --soft HEAD~1
```

### Откатить последний коммит на GitHub

⚠️ **Опасно.** Только если работаешь один.

```bash
git reset --hard HEAD~1
git push --force
```

---

## 7. История

### Общая картина

```bash
git log --oneline --graph --all
```

### Что в конкретном коммите

```bash
git show <commit-hash>
```

---

## 8. Работа с двумя репо

Структура папок:

```
outdoor-ads-calc/
├── calc-outdoor-ads/          # код
└── calc-outdoor-ads-qa/       # документация и тесты
```

VS Code открываешь **на родительской папке**. Git-команды выполняешь из нужной подпапки.

```bash
cd outdoor-ads-calc/calc-outdoor-ads
```
Работа с кодом.

```bash
cd ../calc-outdoor-ads-qa
```
Работа с докой.

Путь видно в терминале — не перепутаешь.

---

## 9. Типичные ошибки

| Ошибка | Причина | Решение |
|---|---|---|
| `fatal: not a git repository` | Не в той папке | `cd` в папку репо |
| `failed to push some refs` | На GitHub есть коммиты, которых нет локально | `git pull --rebase`, потом `git push` |
| `Please tell me who you are` | Не настроен user.name/email | См. раздел 1 |
| `Updates were rejected` | Конфликт или защищённая ветка | `git pull`, разобрать конфликт, потом пуш |
| `nothing to commit` | Нечего коммитить | Всё уже закоммичено |

---

## 10. Минимальный цикл

Если забыл всё — вернись сюда.

```bash
git status
git add .
git commit -m "Что сделал"
git push
```

Всё остальное — по необходимости.

---

