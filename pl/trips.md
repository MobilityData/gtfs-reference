---
lang: pl

table_data:
  - field_name: route_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **route_id** zawiera unikalny identyfikator linii do której przynależy ten kurs. Wartość ta jest musi być zgodna z plikiem [routes.txt](#routes).
  - field_name: service_id
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          Pole **service_id** zaweira unikalny identyfikator kalandarza, który określa dni w które kurs jest aktywny. Wartość ta musi być zgodna z plikiem [calendar.txt](#calendar) lub [calendar_dates.txt](#calendar_dates).
  - field_name: trip_id
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **trip_id** zawiera unikalny identyfikator kursu. Wartość ta jest unikatowa w skali pliku.
  - field_name: trip_headsign
    details:
      - ID: 4
        required: false
        tags: []
        text: |
          Pole **trip_headsign** zawiera tekst, który stosowany jest na oznakowaniu w celu określenia celu kursu. Użyj tego pola aby rozóżnić różne schematy kursów w linii. Jeśli tablica kierunkowa zmienia się podczas trwania kursu, możesz nadpisać wartość pola **trip_headsign** definiujac wartości kolumny **stop_headsign** w pliku [stop_times.txt](#stop_times).
  - field_name: trip_short_name
    details:
      - ID: 5
        required: false
        tags: []
        text: |
          Pole **trip_short_name** definiuje krótki tekst, który pojawia się w rozkładach i na tablicach informacyjnych, np. numery pociągów. Jeśli taki system identyfikacji kursów nie jest powszechnie stosowany przez pasażerów, pozostaw to pole puste. Wartość pola **trip_short_name**, jeśli podana, powinna unikatowo identyfikować kurs w każdym dniu; nie powinna być stosowana dla tablic kierunkowych i/lub rozróżnienia kursów pospiesznych od zwykłych.
  - field_name: direction_id
    details:
      - ID: 6
        required: false
        tags: []
        text: |
          Pole **direction_id** definiuje binarną wartość pozwalającą określić kierunek kursu. Kolumna ta jest stosowana w celu rozróżnienia kursów w dwóch kierunkach, ale z tym samym **route_id**. Pole to nie jest stosowane w wytyczaniu trasy — ma wpływ jedynie przy publikowaniu rozkładów całej linii. Nazwy krańców mogą być zdefiniowane za pomocą kolumny **trip_headsign**.

          * 0 - kursuje w jednym kierunku („tam”)
          * 1 - kursuje w przeciwnym kierunku („z powrotem”)

          Na przykład, możesz użyć kolumn *trip_headsign* i *direction_id* w celu przypisania nazwy do kierunku linii. Plik [trips.txt](#trips) może zawierać takie trzy wpisy:

          * `trip_id,...,trip_headsign,direction_id`
          * `1234,...,Lotnisko,0`
          * `1505,...,Centrum,1`
  - field_name: block_id
    details:
      - ID: 7
        required: false
        tags: []
        text: |
          Pole **block_id** zawiera blok do którego należy dany kurs. Blok zawiera jeden lub więcej kursów wykonywanych przez ten sam pojazd, tak, że pasażer może się przesiąść pomiędzy tymi kursami pozostając w pojeździe, definiowanych przez identyfiaktor kalendarza i block_id. Block_id może łączyć kursy z różnymi kalendarzami, tworząc różne bloki w różne dni. (Zobacz [przykład poniżej](#example-showing-blocks-and-service-day))
  - field_name: shape_id
    details:
      - ID: 8
        required: false
        tags: []
        text: |
          Pole **shape_id** zawiera unikalny identyfikator linii przejazdu, wartość ta musi być zgodna z wpisem z pliku [shapes.txt](#shapes). Plik shapes.txt pozwala ustalić, jak powinny być rysowane na mapach trasy przejazdu kursów.
  - field_name: wheelchair_accessible
    details:
      - ID: 9
        required: false
        tags: []
        text: |
          * **0** (lub puste) - wskazuje, że nie ma informacji o dostępności kursu dla osób poruszających się na wózkach inwalidzkich
          * **1** - wskazuje, że w pojeździe, który wykonuje dany kurs, znajduje się miejsce na co najmniej jeden wózek inwalidzki
          * **2** - wskazuje, że pojazd nie jest dostosowany do przewozu osób poruszających się na wózku
  - field_name: bikes_allowed
    details:
      - ID: 10
        required: false
        tags: []
        text: |
          * 0 (or empty) - wskazuje, że nie ma informacji o dostępności przewozu rowerów w danym kursie
          * **1** - wskazuje, że w pojeździe można przewieźć co najmniej jeden rower
          * **2** - wskazuje, że podczas danego kursu nie ma możliwości przewozu rowerów
---
Plik: **Wymagany**

<div class="table-wrapper">
  <table class="recommendation">
    <thead>
      <tr>
      <th>Nazwa Pola</th>
      <th>Wymagane</th>
      <th>Opis</th>
      </tr>
    </thead>
    <tbody>
    {% for field in page.table_data %}
      {% for detail in field.details %}
      <tr id="{{ page.slug }}_{{ detail.ID }}" class="anchor-row{% if forloop.first %} field-row{% endif %}{% for tag in detail.tags %} {{ tag }}{% endfor %}">
        <td>{% if forloop.first %}<code>{{ field.field_name }}</code>{% endif %}</td>
        <td>{% if detail.required %}Wymagane{% else %}Opcjonalne{% endif %}</td>
        <td>{{ detail.text | markdownify }}{% if detail.example_table %}<div class="table-wrapper">{{ detail.example_table }}</div>{% endif %}</td>
      </tr>
      {% endfor %}
    {% endfor %}
    </tbody>
  </table>
</div>

#### Przykład kombinacji kalendarzy i bloków

Poniższy przykład jest prawidłowy, z innymi blokami w różne dni tygodnia.

| route_id | trip_id | service_id | block_id | <span style="font-weight:normal">*(czas odjazdu z 1. przystanku)*</span> | <span style="font-weight:normal">*(czas przyjazdu na ostatni przystanek)*</span> |
|----------|---------|----------------------------|------------------|----------|----------|
| czerwona | kurs_1  | pon-wt-sr-czw-pt-sob-niedz | okrezna_czerwona | 22:00:00 | 22:55:00 |
| czerwona | kurs_2  | pt-sob-niedz               | okrezna_czerwona | 23:00:00 | 23:55:00 |
| czerwona | kurs_3  | pt-sob                     | okrezna_czerwona | 24:00:00 | 24:55:00 |
| czerwona | kurs_4  | pon-wt-sr-czw-pt           | okrezna_czerwona | 20:00:00 | 20:50:00 |
| czerwona | kurs_5  | pon-wt-sr-czw              | okrezna_czerwona | 21:00:00 | 21:50:00 |

Uwagi do tabeli:
* W piątki, jeden pojazd obsługuje kursy: kurs_1, kurs_2, kurs_3 i kurs_4 (od 20:00 do 00:55). Ostatni kurs jest wykonywany de facto w soboty, od północy do 00:55, ale jest cześcią kalendarza piątkowego, gdyż pola czasów przyjazdu/odjazdu to 24:00:00 i 24:55:00.
* Od poniedziałku do czwartku ten sam pojazd obsługuje kursy: kurs_4, kurs_5 i kurs_1, od 20:00 do 22:55.
