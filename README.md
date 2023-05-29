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
Zdefiniuj zmienną IMIE i przypisz jej swoje imię. Wyświetl zawartość tej zmiennej. Wyeksportuj tą zmienną i sprawdź, czy jest dostępna w nowym (potomnym) interpreterze.
```bash
export IMIE="Twoje Imię"
echo $IMIE
```
Wyświetl listę zmiennych eksportowanych.
```bash
export
```
Zmień własny znak zachęty, modyfikując zmienną PS1.
```bash
PS1="NowyZnakZachęty> "
```
Napisz skrypt, który dla każdego z plików podanych jako argumenty wywołania posortuje jego zawartość.
```bash
#!/bin/bash

for file in "$@"; do
    if [ -f "$file" ]; then
        echo "Sortowanie pliku: $file"
        sort "$file" -o "$file"
        echo "Plik został posortowany."
        echo
    else
        echo "Błąd: $file nie jest plikiem."
        echo
    fi
done
```
Napisz skrypt, który dla każdego z plików podanych jako argumenty wywołania wyświetli w kolejnych liniach 3 najczęściej powtarzające się w nim słowa.
```bash
#!/bin/bash

for file in "$@"; do
    if [ -f "$file" ]; then
        echo "Najczęściej powtarzające się słowa w pliku: $file"
        echo "=============================================="

        cat "$file" | tr -s '[:space:]' '\n' | tr -d '[:punct:]' | tr '[:upper:]' '[:lower:]' | awk '{ count[$1]++ } END { for (word in count) print count[word], word }' | sort -rn | head -n 3

        echo "=============================================="
        echo
    else
        echo "Błąd: $file nie jest plikiem."
        echo
    fi
done
```
## Mips
Pola rejestru koprocesora 0
1.  **Status (Status Register)**: Pole to przechowuje informacje o stanie systemu, takie jak bity rejestru Status (SR), które kontrolują tryb pracy procesora (tryb użytkownika, tryb jądra, tryb monitora), maskowanie przerwań, bit umożliwiający lub blokujący przerwania oraz bity informujące o aktualnym trybie pracy procesora.
    
2.  **Przyczyna wyjątku (Cause)**: Pole to zawiera informacje o przyczynie ostatniego wyjątku (np. przerwania, wyjątku związanego z odwołaniem do pamięci), w tym numer wyjątku oraz bity informujące o źródle wyjątku.
    
3.  **Adres błędu (ErrorEPC)**: Pole to przechowuje adres instrukcji, która spowodowała wyjątek lub błąd.
    
4.  **Kontrola przekształceń adresowych (Address Translation Control)**: Pole to zawiera informacje dotyczące kontroli przekształceń adresowych, takie jak tryb pracy MMU (Memory Management Unit), tryb cache, tryb tłumaczenia adresów.
    
5.  **Obszar odwołań do wyjątków (Exception Handling Region)**: Pole to określa obszar pamięci, w którym znajdują się obszary odwołań do wyjątków i procedury obsługi wyjątków.

Instrukcje związane z koprocesorem 0

1.  **Zgłaszanie wyjątku (Exception Handling)**:
    
    -   `eret` (Exception Return): Instrukcja `eret` jest używana do powrotu z procedury obsługi wyjątku. Powoduje przełączenie kontekstu z trybu obsługi wyjątku do trybu, w którym wystąpił wyjątek. Instrukcja `eret` odczytuje zawartość rejestru koprocesora 0, aby przywrócić stan procesora sprzed wyjątku.
2.  **Przenoszenie wartości (Move Value)**:
    
    -   `mfhi` (Move From HI): Instrukcja `mfhi` służy do przeniesienia zawartości rejestru HI do innego rejestru ogólnego. Rejestr HI przechowuje wynik operacji mnożenia lub dzielenia.
    -   `mflo` (Move From LO): Instrukcja `mflo` służy do przeniesienia zawartości rejestru LO do innego rejestru ogólnego. Rejestr LO przechowuje resztę z operacji dzielenia lub wynik operacji modulo.
3.  **Zapisywanie słowa (Store Word)**:
    
    -   `sw` (Store Word): Instrukcja `sw` służy do zapisywania słowa z rejestru ogólnego do pamięci. Adres docelowy jest obliczany na podstawie zawartości rejestru bazowego i przesunięcia. Na przykład: `sw $s1, offset($s2)` zapisuje wartość ze rejestru `$s1` do pamięci o adresie `$s2 + offset`.

Obsługa wyjątków
```asm
# Obsługa wyjątku na procesorze MIPS

.data
exception_message: .asciiz "Wyjątek zarejestrowany.\n"

.text
.globl main

main:
    # Konfiguracja wektora przerwań
    lui $k0, 0xFFFF # Adres bazy wektora przerwań
    ori $k0, $k0, 0xFFF0

    # Rejestracja procedury obsługi wyjątku
    lui $k1, exception_handler
    ori $k1, $k1, exception_handler

    # Przypisanie adresu procedury obsługi wyjątku do wektora przerwań
    sw $k1, 0($k0) # Wyjątek ogólny

    # Wywołanie instrukcji, która spowoduje wyjątek
    li $v0, 10
    syscall

    # Koniec programu
    li $v0, 10
    syscall

exception_handler:
    # Obsługa wyjątku - wypisanie komunikatu
    li $v0, 4
    la $a0, exception_message
    syscall

    # Powrót z obsługi wyjątku
    jr $ra
```
Powyższy kod demonstruje obsługę ogólnego wyjątku na procesorze MIPS. Przykład zakłada, że wektor przerwań znajduje się na adresie bazy 0xFFFFFFF0, a procedura obsługi wyjątku jest zarejestrowana w wektorze pod tym adresem.

Procedura `main` najpierw konfiguruje wektor przerwań, przypisując mu adres bazy i procedury obsługi wyjątku. Następnie wywołuje instrukcję, która spowoduje wyjątek (w tym przypadku, syscall o kodzie 10). Po obsłużeniu wyjątku, program wypisuje komunikat i kończy działanie.

Procedura obsługi wyjątku `exception_handler` wypisuje komunikat za pomocą syscallu o kodzie 4 i zwraca się do procedury wywołującej za pomocą instrukcji `jr $ra`.

Ważne jest, aby zaznaczyć, że obsługa wyjątków na procesorze MIPS może się różnić w zależności od implementacji i konkretnego systemu operacyjnego. Powyższy kod stanowi tylko ogólny przykład i może wymagać dostosowania do konkretnych potrzeb i środowiska pracy.
