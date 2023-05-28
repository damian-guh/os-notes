# Systemy operacyjne kolos


## Obsługa katalogów

- Tworzenie nowego katalogu 
```bash
mkdir nazwaKatalogu 
```
- Zmiana bieżącego katalogu
```bash
cd nazwaKatalogu
```
- Wyświetlenie zawartości katalogu
```bash
ls
```
- Usuwanie katalogu (jeśli jest pusty)
```bash
rmdir nazwaKatalogu 
```
- Usuwanie katalogu wraz z jego zawartością
```bash
rmdir -r nazwaKatalogu 
```

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

## Prawa dostępu

  ```bash
drwxrwxr-x 3 guh guh 4096 lis  8  2022 CLionProjects
 ```

Pierwsza litera oznacza typ , **d** w tym przypadku oznacza, że jest to katalog. 
**-** oznaczałby że jest to zwykły plik
Kolejne trzy litery oznaczają dostęp właściciela, który może odczytać plik zapisać lub uruchomić.
**r** oznacza że osoba której dotyczy blok znaków może odczytać plik
**w** oznacza że może zapisać zmiany
**x** oznacza że może urchomić
Kolejne trzy litery oznaczają że grupa użytkownika może również dokonać zmian takich jak on sam
Ostatnie litery dotyczą pozostałych użytkowników którzy w tym przypadku mogą jedynie odczytać katalog i go uruchomić

Przykład
```bash
chmod u+rwx nazwaPliku
```
oznacza że użytkownik otrzymuje wszystkie prawa, jeśli zostałby użyty **-** oznaczałoby to że te uprawnienia zostałyby zabrane

Zamiast liter możemy używać również cyfr gdzie:
**r** = 4
**w** = 2
**x** = 1
**rwx** = 4 + 2 + 1 = 7
Przykład
```bash
chmod 755 nazwaPliku
```
oznacza że właściciel ma pełne uprawnienia, a grupa i pozostali tylko do odczytu i uruchomienia

## Procesy
Proces w systemie Linux to działający program lub zadanie. Może to być pojedyncza aplikacja, usługa systemowa, skrypt lub inny rodzaj zadania, które jest wykonywane w systemie operacyjnym.

W systemie Linux każdy proces ma swój unikalny identyfikator procesu (PID), który służy do jego identyfikacji i zarządzania. Procesy działają niezależnie od siebie, posiadając swoje własne zasoby, takie jak pamięć, czas procesora i otwarte pliki.

Procesy mogą być uruchamiane w tle lub w trybie interaktywnym. Procesy uruchomione w tle działają w tle, nie wymagając bezpośredniego interakcji użytkownika. Z kolei procesy uruchomione w trybie interaktywnym są uruchamiane w określonym terminalu i oczekują na wejście od użytkownika.

Procesy w systemie Linux mają różne statusy, które odzwierciedlają ich aktualne działanie. Niektóre z najważniejszych statusów to:

1.  Uruchomiony (Running): Proces jest aktywnie wykonywany przez procesor.
    
2.  Zatrzymany (Stopped): Proces został tymczasowo zatrzymany i oczekuje na dalsze działanie lub wznawienie.
    
3.  Uspiony (Sleeping): Proces jest w trybie uśpienia, nie wykorzystuje zasobów procesora i oczekuje na jakieś zdarzenie.
    
4.  Zombie: Proces, który zakończył działanie, ale nie został jeszcze usunięty z listy procesów. Zombie zajmuje niewielką ilość zasobów i czeka na powiadomienie od systemu operacyjnego o zakończeniu swojego działania.

5.  Oczekiwanie na sygnał (Waiting): Proces oczekuje na sygnał od innego procesu. Może to być oczekiwanie na zakończenie innego procesu lub oczekiwanie na sygnał zewnętrzny.
    
6.  Zakończony (Exited): Proces zakończył swoje działanie i został usunięty z listy procesów. Po zakończeniu procesu jego zasoby zostają zwolnione.

7. Proces sierota (ang. orphan process) to proces, który został utworzony przez inny proces, ale jego rodzic (proces macierzysty) zakończył działanie przed nim lub przed zakończeniem pracy procesu potomnego. W wyniku tego proces sierota zostaje przypisany do specjalnego procesu o identyfikatorze PID równym 1, który jest zazwyczaj inicjalizowany jako pierwszy proces w systemie (znany jako proces init lub systemd w nowoczesnych dystrybucjach Linuxa).

	Główne cechy procesu sieroty to:

	-  Brak rodzica: Proces sierota traci swojego rodzica, ponieważ ten zakończył działanie.
    
	- Przypisanie do procesu init: Proces sierota zostaje przypisany do procesu init (PID 1), który staje się nowym rodzicem procesu sieroty.

Wyświetlenie wszystkich procesów
```bash
ps
```
Bardziej szczegółowa lista
```bash
ps aux
```
Zakończenie procesu
```bash
kill IDProcesu
```
Natychmiastowe zakończenie procesu
```bash
kill -9 IDProcesu
```
Zmiana priorytetu procesu
```bash
renice priorytet -p IDProcesu
```
gdzie priorytet to liczba od -20 (najwyższy) do 19 (najniższy)

Uruchamianie procesu w tle
```bash
komenda &
```
Wznawianie procesu
```bash
bg IDProcesu
```
Zatrzymanie procesu w tle
```bash
fg IDProcesu
```
Wyświetlenie statusów procesów
```bash
top
```
Bardziej szczegółowe wyświetlenie statusów procesów
```bash
htop
```
Wyszukiwanie procesów po kryteriach
```bash
pgrep
```
Wyszukiwanie procesów o nazwie **apache**
```bash
pgrep apache
```
Zatrzymanie procesów o nazwie apache
```bash
kill $(pgrep apache)
```
## Zadania z poleceniami lub skrypty

Wyświetl plik /etc/passwd z podziałem na strony przyjmując, że strona na 5 linii tekstu.
```bash
more -5 /etc/passwd
```

Korzystając z polecenia cat utwórz plik tekst3, który będzie składał się z zawartości pliku tekst1, ciągu znaków podanego ze standardowego wejścia (klawiatury) i pliku tekst2.
```bash
cat tekst1 - tekst2 > tekst3
```
Wyświetl linie o numerach 3, 4 i 5 z pliku /etc/passwd
```bash
head -n 5 /etc/passwd | tail -n 3
```
Wyświetl linie o numerach 7, 6 i 5 od końca pliku /etc/passwd
```bash
tail -n 7 /etc/passwd | head -n 3
```
Wyświetl zawartość /etc/passwd w jednej linii
```bash
tr  '\n'  ' ' < /etc/passwd
```
Za pomocą filtru tr wykonaj modyfikację pliku, polegającą na umieszczeniu każdego słowa w osobnej linii.
```bash
tr ' ' '\n' < plikWejściowy > plikWyjściowy
```
Zlicz wszystkie pliki znajdujące się w katalogu /etc i jego podkatalogach
```bash
find /etc -type f | wc -l
```
Napisać polecenie zliczające sumę znaków z pierwszych trzech linii pliku /etc/passwd
```bash
head -n 3 /etc/passwd | tr -d '\n' | wc -m
```
Wyświetl listę plików z aktualnego katalogu, zamieniając wszystkie małe litery na duże.
```bash
ls | tr '[:lower:]' '[:upper:]'
```
Wyświetl listę plików w aktualnym katalogu, posortowaną według rozmiaru pliku
```bash
ls -lS
```
Podaj nazwy trzech najmniejszych plików w katalogu posortowanym wg nazwy
```bash
ls -S -r | head -n 3
```
Wyświetl statystykę używanych komend (bez argumentów) w postaci posortowanej listy: ilość komenda ( wsk. należy użyć polecenia history)
```bash
history | awk '{print $1}' | sort | uniq -c | sort -nr
```
