Отчет по лабораторной работе №5.
===

Задача 1:
----

1. Устанавливаю Git
 ```bash
   sudo apt install git
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

Задача 2:
----


