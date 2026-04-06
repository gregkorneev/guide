
---
# 🔐 Лабораторная 1 — Права доступа

## 🎯 Цель

Изучить:

- права доступа к файлам и каталогам
    
- владельцев и группы
    
- влияние root и пользователя
    
- механизм sticky bit (файлообменник)
    

---

## 🔹 1. Создание файлов

```bash
cd ~
touch file1 file2 file3
```

📊 **Результат:**  
Созданы три пустых файла в домашнем каталоге.

---

## 🔹 2. Получение списка файлов

```bash
ls -l > home_files1
cat home_files1
```

📊 **Анализ:**  
Пример строки:

```
-rw-r--r-- 1 testuser testuser 0 file1
```

- `-rw-r--r--` — права доступа (644)
    
- владелец: `testuser`
    
- группа: `testuser`
    

📌 **Вывод:**  
Файлы принадлежат пользователю, запись разрешена только владельцу.

---

## 🔹 3. Работа от root

```bash
su -
cd /home/USERNAME
touch rfile1 rfile2 rfile3
ls -l >> home_files1
exit
```

---

## 🔹 4. Сравнение

```bash
cat home_files1
```

📊 **Анализ:**

|Файл|Владелец|
|---|---|
|file1|testuser|
|rfile1|root|

📌 **Вывод:**  
Файлы, созданные root, принадлежат суперпользователю.

---

## 🔹 5. Изменение файлов

```bash
nano file1
nano rfile1
```

📊 **Анализ:**

- file1 → редактируется ✅
    
- rfile1 → обычно не редактируется ❌ (зависит от прав)
    

📌 **Вывод:**  
Право записи зависит от прав доступа, а не только от владельца.

---

## 🔹 6. Изменение прав

```bash
su -
cd /home/USERNAME

chmod u-w,g-w file1
chmod a+w rfile1
```

---

## 🔹 7. Проверка

```bash
exit
nano file1
nano rfile1
```

📊 **Результат:**

|Файл|Результат|
|---|---|
|file1|❌ нельзя редактировать|
|rfile1|✅ можно редактировать|

📌 **Вывод:**  
Даже владелец не может редактировать файл без права записи.

---

## 🔹 8. Изменение владельца

```bash
su -
cd /home/USERNAME

chown root:users file1
chown root:users file2
```

---

## 🔹 9. Проверка

```bash
exit
nano file2
```

📊 **Результат:**  
❌ запись запрещена

📌 **Вывод:**  
Пользователь не может изменять файл, владельцем которого он не является.

---

# 📁 Работа с каталогами

---

## 🔹 10. Создание

```bash
su -
mkdir -p /home/shared/pub
mkdir -p /home/shared/upload
mkdir -p /home/shared/temp
```

---

## 🔹 11. Права

### pub

```bash
chown root:users /home/shared/pub
chmod 775 /home/shared/pub
```

### upload

```bash
chown nobody:users /home/shared/upload
chmod 130 /home/shared/upload
```

### temp

```bash
chown USERNAME:users /home/shared/temp
chmod 777 /home/shared/temp
```

---

## 🔹 12. Проверка

```bash
exit

cp file1 /home/shared/pub
cp file1 /home/shared/upload
cp file1 /home/shared/temp
```

📊 **Результаты:**

|Каталог|Результат|
|---|---|
|pub|❌ отказ в доступе|
|upload|❌ нет доступа|
|temp|✅ работает|

---

## 🔹 13. Анализ каталогов

📌 **pub (775):**

- запись только для владельца и группы
    
- пользователь вне группы → ❌
    

📌 **upload (130):**

- нет прав для остальных
    
- почти полный запрет доступа
    

📌 **temp (777):**

- полный доступ для всех
    

---

## 🔹 14. Sticky bit (файлообменник)

```bash
su -
chmod 1777 /home/shared/temp
ls -ld /home/shared/temp
```

📊 **Результат:**

```
drwxrwxrwt
```

📊 **Проверка:**

|Действие|Результат|
|---|---|
|создать файл|✅|
|удалить свой|✅|
|удалить чужой|❌|

📌 **Вывод:**  
Sticky bit ограничивает удаление чужих файлов.

---

# ⚙️ Лабораторная 2 — Процессы

---

## 🔹 1. Справка

```bash
man ps
```

---

## 🔹 2. Процессы

```bash
ps
echo $$
```

📊 **Результат:**  
PID bash совпадает с `echo $$`

---

## 🔹 3. Все процессы

```bash
ps aux
```

---

## 🔹 4. Анализ

```bash
ps aux --sort=-%cpu | head
ps aux --sort=-%mem | head
```

📊 **Ответ:**

- max CPU → packagekitd
    
- max RAM → gnome-shell
    

---

## 🔹 5. init

```bash
ps -e | grep systemd
```

📊 **Ответ:**

- PID = 1
    
- пользователь = root
    

📌 **Вывод:**  
systemd — главный процесс системы.

---

## 🔹 6. nano

(во втором терминале)

```bash
nano
```

---

## 🔹 7. Найти nano

```bash
ps aux | grep nano
```

📊 **Результат:**  
определён PID nano

---

## 🔹 8. Убить nano

```bash
killall nano
```

📌 **Вывод:**  
процесс завершён

---

## 🔹 9. Мониторинг

```bash
top
```

📊 **Вывод:**

- ps → статично
    
- top → динамика
    

---

## 🔹 10. Приостановка

```bash
find / -name "*.html"
```

Ctrl + Z

```bash
man bash
```

Ctrl + Z

---

## 🔹 11. Задачи

```bash
jobs
```

📊 показывает номера задач

---

## 🔹 12. Продолжить

```bash
fg %1
```

---

## 🔹 13. Завершить

```bash
kill %2
```

---