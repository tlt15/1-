##Задача 6 Написать программу для проверки наличия комментария в первой строке файлов с расширением c, js и py.
```
import os

def check_comment(file_path): with open(file_path, 'r') as file: first_line = file.readline().strip()
    if file_path.endswith('.c'):
        if first_line.startswith('//') or first_line.startswith('/*'):
            return f"{file_path}: комментарий найден"
        else:
            return f"{file_path}: комментарий не найден"
    
    elif file_path.endswith('.js'):
        if first_line.startswith('//'):
            return f"{file_path}: комментарий найден"
        else:
            return f"{file_path}: комментарий не найден"
    
    elif file_path.endswith('.py'):
        if first_line.startswith('#'):
            return f"{file_path}: комментарий найден"
        else:
            return f"{file_path}: комментарий не найден"
    
    else:
        return f"{file_path}: неподдерживаемый формат"

```

##Перебираем все файлы с заданными расширениями в текущем каталоге
```
for filename in os.listdir('.'): if filename.endswith(('.c', '.js', '.py')): result = check_comment(filename) print(result)
```
![image](https://github.com/user-attachments/assets/ec56d6f2-3d3f-491c-a246-76cfb3b41b4a)
