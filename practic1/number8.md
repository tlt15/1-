## Задача 8  Написать программу, которая находит все файлы в данном каталоге с расширением, указанным в качестве аргумента и архивирует все эти файлы в архив tar.
 ```
 import os import tarfile import argparse
def find_files_with_extension(directory, extension): """Находит все файлы с заданным расширением в указанном каталоге.""" matched_files = [] for root, _, files in os.walk(directory): for file in files: if file.endswith(extension): matched_files.append(os.path.join(root, file)) return matched_files
def create_tar_archive(files, archive_name): """Создает архив tar из списка файлов.""" with tarfile.open(archive_name, 'w') as tar: for file in files: tar.add(file, arcname=os.path.relpath(file, start=os.path.dirname(files[0])))
if name == "main": parser = argparse.ArgumentParser(description="Архивирует файлы с заданным расширением.") parser.add_argument("directory", help="Путь к каталогу для поиска файлов.") parser.add_argument("extension", help="Расширение файлов для архивации (например, .txt).") parser.add_argument("archive_name", help="Имя выходного архива (например, archive.tar).")
args = parser.parse_args()
files_to_archive = find_files_with_extension(args.directory, args.extension)
if files_to_archive:
    create_tar_archive(files_to_archive, args.archive_name)
    print(f"Архив '{args.archive_name}' успешно создан с {len(files_to_archive)} файлами.")
else:
    print("Файлы с указанным расширением не найдены.")
```
![image](https://github.com/user-attachments/assets/840a3741-cf01-4b96-93ea-d891a48c3db0)
