# 🚀 Создание и запуск проекта

## Создать проект
```bash
dotnet new console -n (пользовательское название проекта)
```
Перейти в проект
```bash
cd ./(пользовательское название проекта)
```

Базовый .gitignore файл который можно использовать во всех проектах. В пустом проекте сразу после создания создать файл .gitignore и вставить текст ниже:
```bash
bin/
obj/
*.user
*.suo
*.userprefs
.vscode/
.DS_Store
__MACOSX/
*.log
*.tmp
*.temp
.idea/
*.nupkg
*.snupkg
packages/
TestResults/
coverage/
```
---

## Запустить программу
```bash
dotnet run
```

---
## GitHub
Отправить все содержимое папки:
```bash
git add .
```

Отправить конкретный файл:
```bash
git add (полное имя файла)
```

Commit пуша:
```bash
git commit -m "написать текст коммита"
```

Отправить:
```bash
git push
```

# 🔨 Работа с проектом

## Сборка
```bash
dotnet build
```

---

## Очистка
```bash
dotnet clean
```

---

## Восстановление зависимостей
```bash
dotnet restore
```

---

# 📦 Работа с пакетами (NuGet)

## Установить пакет
```bash
dotnet add package Newtonsoft.Json
```

---

## Удалить пакет
```bash
dotnet remove package Newtonsoft.Json
```

---

## Связать с основным проектом
```bash
cd MyApp.Tests
dotnet add reference ../MyApp/MyApp.csproj
```

---

## Запустить тесты
```bash
dotnet test
```

---

# 📁 Полезные команды

## Список шаблонов
```bash
dotnet new list
```

---

## Автозапуск при изменениях
```bash
dotnet watch run
```

---

## Сборка релиза
```bash
dotnet publish
```

---
