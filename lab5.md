Отчет по лабораторной работе №5.
===

Задача 1:
----

1. Устанавливаю Git
 ```bash
   sudo apt install git
   ```
![unnamed](https://github.com/user-attachments/assets/38a8c5e0-d76a-4668-8273-02efb49cafa5)


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

# Перебираем все файлы, которые были добавлены в коммит
for file in $(git diff --cached --name-only); do
  # Пропускаем файл version.txt
  if [[ "$file" == "version.txt" ]]; then
    continue
  fi

  # Проверяем наличие подписи автора в других текстовых файлах
  if [[ "$file" == *.txt ]]; then
    if ! grep -q "Подпись автора" "$file"; then
      echo "Ошибка: в файле $file отсутствует подпись автора."
      exit 1
    fi
  fi
done
```

![unnamed](https://github.com/user-attachments/assets/f8c47ae3-6adc-4e51-b410-1d7a04574fe4)


7. Возвращаюсь в папку репозитория и создаю текстовый файл для проверки роботоспособности хука
```bash
  cd ..
```

8. Создаю текстовый файл с верной записью (Автор: Иван Иванов)
```bash
  sudo nano example.txt
```
![unnamed](https://github.com/user-attachments/assets/fd1d21aa-569d-4385-a364-37c0b8a5e08b)


команда, чтобы проверить файлы в текущей директории:
```bash
  ls - la
```

```bash
  git add example.txt
  git commit -m "Checking the file"
  git push origin main
```

![unnamed](https://github.com/user-attachments/assets/e6bf700f-eb72-4765-b538-b2ce5bf553c8)


9. Создаю текстовый файл с неверной записью без указания авторства (Иван Иванов)
```bash
  sudo nano example2.txt
  git add example2.txt
  git commit -m "Checking file 2"
```
на этапе коммита в данном случае возникает ошибка "файл example2.txt не содержит подписи автора" и коммит не происходит, что и требовалось от меня в данной задачи

![unnamed](https://github.com/user-attachments/assets/99f9e28b-9d67-4c7d-8600-c44fcd2ac654)

если добавляем подпись автора, то ошибка решается:
![unnamed](https://github.com/user-attachments/assets/37383a6b-4740-4466-9a4f-e8fe33a5addd)


Задача 2: Использование Git Flow в проекте
----
1. Проверка, что Git Flow установлен
```bash
  sudo apt-get install git-flow
```

![unnamed](https://github.com/user-attachments/assets/19f7d9e3-5784-4c11-9ef3-e4654d601183)


2. В корне репозитория выполняю команду:
```bash
  git flow init
```

![unnamed](https://github.com/user-attachments/assets/a2fbb3f5-8592-4ee3-8f9b-9b8ca5f458d3)


3. Создаю ветку для нвоой функциональности:
```bash
  git flow feature start task-management
```

![unnamed](https://github.com/user-attachments/assets/55c882c8-e482-49b4-94e0-d6e66a74d2b1)


4. Создаю файл task_manager.py с кодом:
```bash
  def create_task(title, description):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")
```

![unnamed](https://github.com/user-attachments/assets/0630b9dc-87ad-4ba3-bdee-c86044b2f6c8)



5. Комичу изменения:
```bash
  git add task_manager.py
  git commit -m "Добавлен функционал управления задачами"
```
![unnamed](https://github.com/user-attachments/assets/df3533b3-7cb3-4036-9e84-71b8023c0ba5)
![unnamed](https://github.com/user-attachments/assets/9c184307-acf2-46b2-a1ce-5796ade6d392)



6. Завершение разработки фичи. Объединение ее с веткой develop
```bash
  git flow feature finish task-management
```


7. Создание релиза:
```bash
  git flow release start v1.0.0
```

![unnamed](https://github.com/user-attachments/assets/d9c8a8cc-b10d-425f-b5b5-faf73a9eaee2)



8. Обновление файла version.txt
```bash
  echo "v1.0.0" > version.txt
  git add version.txt
  git commit -m "Обновлена версия для релиза v1.0.0"
```

![unnamed](https://github.com/user-attachments/assets/bf358aa2-8bff-4483-976f-8bcea7598554)

![unnamed](https://github.com/user-attachments/assets/1a7479fb-6e0b-4fcb-8f94-b5b4efe07828)


9. Завершение реализа:
```bash
  git flow release finish v1.0.0
```

10. Отправка измений в удаленный репозиторий
```bash
  git push origin main
  git push origin develop
```
![unnamed](https://github.com/user-attachments/assets/a715ce77-0ec8-4c8a-b0b1-6a7ed91e70c6)



