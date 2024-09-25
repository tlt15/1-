## Задача 7
## Написать программу для нахождения файлов-дубликатов (имеющих 1 или более копий содержимого) по заданному пути (и подкаталогам).
```
import os import hashlib from collections import defaultdict
def hash_file(file_path): """Возвращает хеш файла.""" hasher = hashlib.md5() # Используем MD5 для хеширования try: with open(file_path, 'rb') as f: while chunk := f.read(8192): hasher.update(chunk) return hasher.hexdigest() except Exception as e: print(f"Ошибка при открытии файла {file_path}: {e}") return None
def find_duplicates(directory): """Находит дубликаты файлов в заданном каталоге.""" file_hashes = defaultdict(list)
for root, _, files in os.walk(directory):
    for file in files:
        file_path = os.path.join(root, file)
        file_hash = hash_file(file_path)
        if file_hash:
            file_hashes[file_hash].append(file_path)
```
# Выводим дубликаты
```
duplicates = {hash_value: paths for hash_value, paths in file_hashes.items() if len(paths) > 1}
return duplicates
if name == "main": path_to_search = input("Введите путь для поиска дубликатов: ") duplicates = find_duplicates(path_to_search)
if duplicates:
    print("Найденные дубликаты:")
    for hash_value, paths in duplicates.items():
        print(f"\nХеш: {hash_value}")
        for path in paths:
            print(f"  {path}")
else:
    print("Дубликаты не найдены.")
```
    Мы создали 2 файла: 12.txt и 22.txt имеющие следующие строки: "12345" и "123456"
![image](https://github.com/user-attachments/assets/6588de83-0bc1-470a-a0ac-134a833ef277)
