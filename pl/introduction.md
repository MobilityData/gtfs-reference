---
lang: pl

---
# Specyfikacja General Transit Feed Specification

**Wersja z 4 Sierpnia 2016. Zobacz [historię rewizji](https://github.com/google/transit/blob/master/gtfs/CHANGES.md) po więcej szczegółów.**

Ten dokument wyjaśnia typy plików, które składają się na format GTFS oraz definuje znaczenia kolumn używanych w każdym z plików.

## Definicje Zwrotów

Ta sekcja definiuje zwroty, które będą używane w całym dokumencie.

* **Pole wymagane** - Ta kolumna musi być zawarta w pliku GTFS, oraz każdy wpis musi mieć zdefiniowaną wartość. Niektóre wymagane kolumny akcjeptują pusty tekst jako wartość, aby to wprowadzić pomiń jakikolwiek tekst między przecinakami (`,,`). Uważaj, np. wartość 0 będzie interpretowana jako „tekst o treści »0«”. Zobacz definicje pól po więcej szczegółów.
* **Pole opcjolane** - Ta kolumna nie musi być zawarta w pliku GTFS, ale jeśli jest ona zdefiniowana, każdy wpis musi mieć zdefiniowaną wartość. Niektóre wymagane kolumny akcjeptują pusty tekst jako wartość, aby to wprowadzić pomiń jakikolwiek tekst między przecinakami (`,,`). Uważaj, np. wartość 0 będzie interpretowana jako „tekst o treści »0«”.
* **Unikatowe w skali pliku** - To pole zawiera wartość, która jest przyporządkowana do tylko jednego wpisu. Na przykład, jeśli identyfikator **1A** zostanie przyporządkowany jakieś linii, to żadna inna linia nie może użyć tego idenytfikatora; Natomiast identyfikator **1A** może zostać przypisany przystankowi, gdyż przystanki są innymi obiekatmi od linii.

## Pliki w Archiwum

Specyfikacja GTFS definiuje następujące pliki wraz z ich zawartością:

|  Nazwa pliku | Wymagany | Definiuje |
|  ------ | ------ | ------ |
|  [agency.txt](#agency) | **Wymagany** | Jeden lub więcej podmiotów odpowiedzialnych za rozkłady jazdy. |
|  [stops.txt](#stops) | **Wymagany** | Pojedyńcze lokalizacje gdzie pojazdy mogą zabierać/odstawiać pasażerów. |
|  [routes.txt](#routes) | **Wymagany** | Linie komunikacyjne. Linia to zbiór kursów które są pokazywane pasażerowi jako jeden byt. |
|  [trips.txt](#trips)  | **Wymagany** | Kursy każdej linii. Kurs to sekwencja dwóch lub więcej przystanków, które odbywają się o jasno-określonym czasie. |
|  [stop_times.txt](#stop_times)  | **Wymagany** | Czasy przyjazdów i odjazdów pojazdów z przystanków w kursie. |
|  [calendar.txt](#calendar)  | **Wymagany** | Kalendarze (schemty kursowania). Określa, kiedy dany kalendarz się zaczyna i kończy, oraz w jakie dni tygodnia jest aktywny. |
|  [calendar_dates.txt](#calendar_dates)  | Opcjonalny | Odchylenia od standardowych schematów kursowania z pliku [calendar.txt](#calendar) file. Jeśli [calendar_dates.txt](#calendar_dates) zawiera WSZYTSKIE daty, to plik [calendar.txt](#calendar) może zostać pominięty. |
|  [fare_attributes.txt](#fare_attributes)  | Opcjonalny | Informacje o taryfach stosowanych na liniach podmiotów. |
|  [fare_rules.txt](#fare_rules)  | Opcjonalny | Zasady stosowania taryf biletowych na liniach. |
|  [shapes.txt](#shapes)  | Opcjonalny | Zasady rysowania linii na mapie w celu poprawnego wyświetlania tras przejazdów kursów. |
|  [frequencies.txt](#frequencies)  | Opcjonalny | Częstotliwości (maksymalne czasy między kursami) dla linii z różnymi częstotliowściami w ciągu dnia. |
|  [transfers.txt](#transfers)  | Opcjonalny | Zasady tworzenia przesiadek. |
|  [feed_info.txt](#feed_info)  | Opcjonalny | Dodatkowe informacje o samym pliku, takie jak wersja, podmiot publikujący i data obowiązywania. |

## Wymagania Plików

Poniższe wymagania stosowane są do formatu i zawartości plików w archiwum GTFS:

* Wszytskie pliki General Transit Feed Spec (GTFS) muszą zostać zapisane jako tekst-oddzielony-przecinakiami (CSV).
* Pierwsza linia każdego pliku musi zawierać nazwy kolumn. Każda podsekcja [Definicji Plików](#Field-Definitions) odpowiada jednemu plikowi i definiuje kolumny, których można używać w pliku.
* Wielkość liter w nazwach kolumn i wartości ma znaczenie!
* Wartości pól nie mogą zawierać znaków tabulacji, powrotu karetki (CR) lub nowej linii (LF).
* Wartości pól ze znakami zapytania lub przecinakami muszą zostać zamknięte w cudzysłowach. W dodatku każdu cudzysłów w wartości pola musi zostać poprzedzony drugim cudzysłowem. Jest to zgodne ze sposobem w jaki Microsoft Excel eksportuje pliki CSV. Po więcej infromacji o plikach CSV zobacz http://tools.ietf.org/html/rfc4180.
Poniższy przykład pokazuje poprawne stosowanie tych zasad:
  * **Oryginalna wartość pola:** `Zawiera "cudzysłowy", przecinki i tekst`
  * **Wartość pola w pliku CSV:** `"Zawiera ""cudzysłowy"", przecinki i tekst"`
* Wartości pól nie mogą zawierać żadnych tagów HTML, komentarzy, lub sekwencji modyfikacji/znaków ucieczki.
* Usuń niepotrzebne spacje między nazwami kolumn/wartościami pól. Aplikacje konsumujące pliki GTFS będą traktowały białe znaki jak część pola, co może powodować błędy.
* Każda linia musi być zakończona znakami końca linii CRLF lub LF.
* Pliki powinny być kodowane w systemie znaków UTF-8 aby wspierać wszystkie znaki Unicode. Pliki mogą zawierać znaczniki kolejności bajtów (BOM, byte-order mark). zobacz [Unicode FAQ](http://unicode.org/faq/utf_bom.html#BOM) po więcej informacji o znacznikach kolejności bajtów i o UTF-8.
* Pliki CSV powinny zostać zarchiwzowane w formacie ZIP, i znajdować się na najwyższym poziomie w archiwum.
