---
lang: pl

table_data:
  - field_name: trip_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **trip_id** zaweira unikalny identyfikator linii do której przynależy to określenie częstotliwości kursowania. Wartość ta musi być zgodna z plikiem [trips.txt](#trips).
  - field_name: start_time
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          Pole **start_time** zawiera czas odjazdu pierwszego pojazdu z pierwszego przystanku dla danego zakresu częstotliwości. Czas jest odliczany względem "południe minus 12 godzin" (generalnie północ, z wyjątkiem dni, w które następuje zmiana czasu letni↔zimowy) na początku dnia kalendarzowego. Dla czasów po północy (należących do poprzedniego dnia kalendarzowego) wartość będzie większa od 24:00:00; w formacie HH:MM:SS czasu liczonego od południa minus 12h dnia poprzedniego, np. 25:30:00.
  - field_name: end_time
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **end_time** zawiera czas zmiany częstotliwości kursowania (lub zaprzestania kursowania). Czas jest odliczany względem "południe minus 12 godzin" (generalnie północ, z wyjątkiem dni, w które następuje zmiana czasu letni↔zimowy) na początku dnia kalendarzowego. Dla czasów po północy (należących do poprzedniego dnia kalendarzowego) wartość będzie większa od 24:00:00; w formacie HH:MM:SS czasu liczonego od południa minus 12h dnia poprzedniego, np. 25:30:00.
  - field_name: headway_secs
    details:
      - ID: 4
        required: true
        tags: []
        text: |
          Pole **headway_secs** definiuje czas pomiędzy odjazdami kursów z jednego przystanku (częstotliwość) dla danego schematu kursu, w zakresie czasowym od **start_time** do **end_time**. Wartość częstotliwości podawana jest w sekundach.

          Zakresy częstosliwości (wiersze w pliku frequencies.txt) nie powinny nakładać się dla jednego trip_id, gdyż nie jest jasne jak interpretować nakładające się zakresy częstotliwości. Z drugiej strony, czas końca jednego zakresu może pokrywać się z czasem rozpoczęcia następnego:

          | `trip_id,start_time,end_time,headway_secs` |
          | `A,05:00:00,07:00:00,600` |
          | `A,07:00:00,12:00:00,1200` |
  - field_name: exact_times
    details:
      - ID: 5
        required: false
        tags: []
        text: |
          Pole **exact_times** określa, czy kurs opisany za pomocą częstotliwości powinien być interpretowany jako ścisły odstęp między kursami, czy jako ogólna informacja o częstotliwości kursowania. Pole to przyjumje następujące wartości:

          * **0** (lub puste) - Częstotliwość stanowi ogólną informację dla podróżnych — Jest to domyślne zachowanie.
          * **1** - Kursy opisane za pomocą częstotliwości mają ścisły odstęp między odjazdami. Dla wiersza w pliku frequencies.txt obliczany jest czas rozpoczęcia każdego kursu według schematu: czas_rozpoczecia_kursu = start_time + (headway_secs * n) dla każdej liczby naturalnej n (0, 1, 2, …) podczas gdy czas_rozpoczecia_kursu < end_time (ostro mniejsze!).

          Wartość **exact_times** powinna być taka sama dla każdego **trip_id**. Jeśli **exact_times**=1 i **start_time**==**end_time**, żaden kurs nie odbywa się w podanym zakresie (gdyż czas_rozpoczecia_kursu == end_time, a czas_rozpoczecia_kursu powinen być ostro mniejszy od **end_time**). Gdy **exact_times** przyjmuje wartość 1, trzeba zwrócić uwagę, aby **end_time** było większe niż czas rozpoczęcia ostatniego kursu oraz żeby nie zawierała odjazdu następnego, nieistniejącego, kursu.
---
Plik: **Opcjonalny**

Ta tabela używana jest w celu reprezenacji rozkładów bez ścisłej listy czasów odjazdów z przystanków. Kiedy kursy są zdefiniowane w frequencies.txt, planery podróży będą ignorowały wartości podane w kolumnach **arrival_time** i **departure_time** dla danego **trip_id** w pliku [stop_times.txt](#stop_times). Zamiast tego **stop_times.txt** powinno zawierać czasy przejazdu między przystankami na danej trasie.

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
