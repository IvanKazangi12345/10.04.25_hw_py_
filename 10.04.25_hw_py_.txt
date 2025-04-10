LIBRARY_FILE = "library.txt"

def add_book():
    title = input("Введите название книги: ").strip()
    author = input("Введите автора книги: ").strip()
    with open(LIBRARY_FILE, "a", encoding="utf-8") as file:
        file.write(f"{title} | {author}\n")
    print("Книга успешно добавлена.\n")

def view_books():
    try:
        with open(LIBRARY_FILE, "r", encoding="utf-8") as file:
            books = file.readlines()
            if books:
                print("Список книг в библиотеке:")
                for book in books:
                    print(book.strip())
            else:
                print("Библиотека пуста.")
    except:
        print("Библиотека пуста.")
    print()

def search_by_author():
    author = input("Введите имя автора для поиска: ").strip().lower()
    found = False
    try:
        with open(LIBRARY_FILE, "r", encoding="utf-8") as file:
            for line in file:
                parts = line.strip().split(" | ")
                if len(parts) == 2:
                    title, book_author = parts
                    if book_author.lower() == author:
                        print(f"Найдена книга: {title} | {book_author}")
                        found = True
    except:
        print("Библиотека пуста.")
    if not found:
        print("Книги данного автора не найдены.")
    print()

def delete_book():
    title_to_delete = input("Введите название книги для удаления: ").strip().lower()
    found = False
    try:
        with open(LIBRARY_FILE, "r", encoding="utf-8") as file:
            books = file.readlines()
        with open(LIBRARY_FILE, "w", encoding="utf-8") as file:
            for line in books:
                parts = line.strip().split(" | ")
                if len(parts) == 2:
                    title, author = parts
                    if title.lower() != title_to_delete:
                        file.write(line + "\n")
                    else:
                        found = True
        if found:
            print("Книга успешно удалена.")
        else:
            print("Книга не найдена.")
    except:
        print("Библиотека пуста.")
    print()

def main():
    while True:
        print("Меню:")
        print("1. Добавить новую книгу")
        print("2. Просмотреть все книги")
        print("3. Поиск книги по автору")
        print("4. Удалить книгу")
        print("5. Выход")

        choice = input("Выберите действие (1-5): ")

        if choice == "1":
            add_book()
        elif choice == "2":
            view_books()
        elif choice == "3":
            search_by_author()
        elif choice == "4":
            delete_book()
        elif choice == "5":
            print("До свидания!")
            break
        else:
            print("Неверный выбор. Пожалуйста, введите число от 1 до 5.\n")

if __name__ == "__main__":
    main()
