# Notatki sytemy operacyjne


## Identyfikator użytkownika
Wyświetla informacje o aktualnym użytkowniku
```bash
 id -u 
 ```
 Wyświetla informacje o podanym użytkowniku
 ```bash
 id nazwaUżytkownika 
 ```
  Wyświetla indetyfikator grupy aktualnego użytkownika
 ```bash
 id -g 
 ```

## Wyszukiwanie plików

Wyszukiwanie na podstawie nazwy w określonej ścieżce
 ```bash
 find ścieżka -name "nazwaPliku" 
 ```
 Wyszukiwanie na podstawie rozszerzenia w określonej ścieżce
  ```bash
 find ścieżka -name "*.rozszerzenie" 
 ```
 Wyszukiwanie na podstawie rozmiaru pliku w tym przypadku plik większy niż 10 MB
  ```bash
 find ścieżka -size +10M
 ```
 jeśli wyszukujemy mniejszy plik niż podana wartość używamy **-** lub nic jeśli wartość ma być równa

