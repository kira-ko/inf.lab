Отчет по лабораторной работе №5.
===

Задача 1:
----

1. Устанавливаю Git
 ```bash
   sudo apt install git
   ```

начальные установки:
```bash
 touch ~/.gitconfig
 git config --global user.name "Ваше Имя"
 git config --global user.email "ваш_email@example.com"
 git config --global --list
 git config --local user.name "Ваше Имя"
 git config --local user.email "ваш_email@example.com"

  ```

 2. Клонирую репозиторий
```bash
  sudo git clone https://github.com/kira-ko/git-practice.git
```

3. Переключаемся в папку с репозиторием
```bash
  cd git-practice
```

```bash
  touch .git/hooks/pre-commit
  chmod +x .git/hooks/pre-commit
```


4. Переходим в скрытую папку Hooks. Эта папка содержит шаблоны хуков, которые мы можем настроить
```bash
  cd .git/hooks
```

5. 
```bash
  nano pre-commit
```

6.
```bash
    #!/bin/bash
    for file in $(git diff --cached --name-only); do
      if [[ "$file" == *.txt ]]; then
          if ! grep -q "Автор" "$file"; then
              echo "Ошибка: файл $file не содержит подписи автора"
              exit 1
          fi
      fi
    done
    exit 0
  
```

7. Возвращаюсь в папку репозитория и создаю текстовый файл для проверки роботоспособности хука
```bash
  cd ..
```

8. Создаю текстовый файл с верной записью (Автор: Иван Иванов)
```bash
  sudo nano example.txt
```

команда, чтобы проверить файлы в текущей директории:
```bash
  ls - la
```


```bash
  git add example.txt
  git commit -m "Checking the file"
  git push origin main
```

9. Создаю текстовый файл с неверной записью без указания авторства (Иван Иванов)
```bash
  sudo nano example2.txt
  git add example2.txt
  git commit -m "Checking file 2"
```
на этапе коммита в данном случае возникает ошибка "файл example2.txt не содержит подписи автора" и коммит не происходит, что и требовалось от меня в данной задачи

Задача 2: Использование Git Flow в проекте
----
1. Проверка, что Git Flow установлен
```bash
  sudo apt-get install git-flow
```

2. В корне репозитория выполняю команду:
```bash
  git flow init
```

3. Создаю ветку для нвоой функциональности:
```bash
  git flow feature start task-management
```
4. Создаю файл task_manager.py с кодом:
```bash
  def create_task(title, description):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")
```

5. Комичу изменения:
```bash
  git add task_manager.py
  git commit -m "Добавлен функционал управления задачами"
```

6. Завершение разработки фичи. Объединение ее с веткой develop
```bash
  git flow feature finish task-management
```


7. Создание релиза:
```bash
  git flow release start v1.0.0
```

8. Обновление файла version.txt
```bash
  echo "v1.0.0" > version.txt
  git add version.txt
  git commit -m "Обновлена версия для релиза v1.0.0"
```

9. Завершение реализа:
```bash
  git flow release finish v1.0.0
```

10. Отправка измений в удаленный репозиторий
```bash
  git push origin main
  git push origin develop
```


