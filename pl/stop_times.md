---
lang: pl

table_data:
  - field_name: trip_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **trip_id** zaweira unikalny identyfikator linii do której przynależy ten przyjazd/odjazd. Wartość ta musi być zgodna z plikiem [trips.txt](#trips).
  - field_name: arrival_time
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          Pole **arrival_time** zaweira czas przyjazdu pojazdu na zdefiniowany przystanek przez zdefiniowany kurs. Czas jest odliczany względem "południe minus 12 godzin" (generalnie północ, z wyjątkiem dni, w które następuje zmiana czasu letni↔zimowy) na początku dnia kalendarzowego. Dla przyjazdów po północy (należących do poprzedniego dnia kalendarzowego) wartość będzie większa od 24:00:00; w formacie HH:MM:SS czasu liczonego od południa minus 12h dnia poprzedniego. Jeśli czas odjazdu i przyjazdu jest taki sam, pola **arrival_time** i **departure_time** powinny zawierać taką samą wartość.

          Rozkładowe przystanki, gdzie pojazd ma ściśle ustalony czas przyjazdu i odjazdu, są nazywane „punktami czasowymi”. Na przykład, jeśli pojazd przyjeżdża na przystanek, zazwyczaj będzie oczekiwał z odjazdem do zdefiniowanego czasu. Jeśli przystanek nie jest punktem czasowym, albo użyj pustej wartości w polu **arrival_time** lub użyj zinterpolowanych czasów. Dodatkowo wskaż, że przystanek nie jest punktem czasowym za pomocą kolumny **timepoint** i wartości 0. Jeśli czasy interpolowane są zankowane za pomocą **timepoint**=0, to przystanki z rozkładowymi czasami powinny zawierać wartość 1 w kolumnie **timepoint**. Czas odjazdu jest potrzebny w każdym wierszu, który oznacza punkt czasowy.

          Czas przyjazdu musi zostać podany przy pierwszym i ostatnim przystanku kursu. Czas jest definiowany za pomocą ośmiu cyfr w formacie HH:MM:SS (H:MM:SS jest też akceptowalne, jeśli godzina rozpoczyna się od 0). Nie podawaj żadnych dodatkowych zanków w polach, w szczególności dotyczy to spacji. Poniższa tabela pokazuje przykładowe czasy odjazdu pojazdu, wraz z pokazaną wartością w polu **arrival_time**:

          |        **Godzina**         | **Wartość arrival_time** |
          |         08:10:00           | 08:10:00 lub 8:10:00 |
          |         13:05:00           | 13:05:00 |
          |       07:40:00 P.M.        | 19:40:00 |
          | 01:55:00 (następnego dnia) | 25:55:00 |

          **Uwaga:** Kursy obowiązujące w kilku dniach kalendarzowych będą zawierały wartości większe niż 24:00:00. Na przykład, kurs może rozpoczynać się o 22:30:00, a kończyć o 02:15:00 następnego dnia — wtedy wartości pól w GTFSie będą odpowiednio wyglądały 22:30:00 i 26:15:00. Wprowadzenia czasów jako 22:30:00 i 02:15:00 byłoby interpretowane jako kurs cofający się w czasie, co jest oczywistym błędem.
  - field_name: departure_time
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **departure_time** zaweira czas odjazdu pojazdu z przystanku przez zdefiniowany kurs. Czas jest odliczany względem "południe minus 12 godzin" (generalnie północ, z wyjątkiem dni, w które następuje zmiana czasu letni↔zimowy) na początku dnia kalendarzowego. Dla odjazdów po północy (należących do poprzedniego dnia kalendarzowego) wartość będzie większa od 24:00:00; w formacie HH:MM:SS czasu liczonego od południa minus 12h dnia poprzedniego. Jeśli czas odjazdu i przyjazdu jest taki sam, pola **arrival_time** i **departure_time** powinny zawierać taką samą wartość.

          Rozkładowe przystanki, gdzie pojazd ma ściśle ustalony czas przyjazdu i odjazdu, są nazywane „punktami czasowymi”. Na przykład, jeśli pojazd przyjeżdża na przystanek, zazwyczaj będzie oczekiwał z odjazdem do zdefiniowanego czasu. Jeśli przystanek nie jest punktem czasowym, albo użyj pustej wartości w polu **departure_time** lub użyj zinterpolowanych czasów. Dodatkowo wskaż, że przystanek nie jest punktem czasowym za pomocą kolumny **timepoint** i wartości 0. Jeśli czasy interpolowane są zankowane za pomocą **timepoint=0**, to przystanki z rozkładowymi czasami powinny zawierać wartość 1 w kolumnie **timepoint**. Czas odjazdu jest potrzebny w każdym wierszu, który oznacza punkt czasowy.

          Czas odjazdu musi zostać podany przy pierwszym i ostatnim przystanku kursu. Czas jest definiowany za pomocą ośmiu cyfr w formacie HH:MM:SS (H:MM:SS jest też akceptowalne, jeśli godzina rozpoczyna się od 0). Nie podawaj żadnych dodatkowych zanków w polach, w szczególności dotyczy to spacji. Poniższa tabela pokazuje przykładowe czasy odjazdu pojazdu, wraz z pokazaną wartością w polu **departure_time**:

          |        **Godzina**         | **Wartość departure_time** |
          |         08:10:00           | 08:10:00 lub 8:10:00 |
          |         13:05:00           | 13:05:00 |
          |       07:40:00 P.M.        | 19:40:00 |
          | 01:55:00 (następnego dnia) | 25:55:00 |

          **Uwaga:** Kursy obowiązujące w kilku dniach kalendarzowych będą zawierały wartości większe niż 24:00:00. Na przykład, kurs może rozpoczynać się o 22:30:00, a kończyć o 02:15:00 następnego dnia — wtedy wartości pól w GTFSie będą odpowiednio wyglądały 22:30:00 i 26:15:00. Wprowadzenia czasów jako 22:30:00 i 02:15:00 byłoby interpretowane jako kurs cofający się w czasie, co jest oczywistym błędem.
  - field_name: stop_id
    details:
      - ID: 4
        required: true
        tags: []
        text: |
          Pole **stop_id** zawiera unikalny przystanku na którym pojawia się pojazd obsługujący kurs. Wartość ta jest musi być zgodna z plikiem [stops.txt](#stops). Jeśli w pliku [stops.txt](#stops) jest używana kolumna **location_type**, każdy przyjazd/odjazd musi mieć przypisany przystanek o **location_type**=0. Dopóki jest to możliwe wartość pola **stop_id** powinna być możliwie stała między iteracjami plików. Innymi słowy, jeśli przstanek A ma przypisane **stop_id=1**, w każdym następnym pliku ten przystanek powinien mieć również **stop_id=1**. Jeśli przystanek nie jest punktem czasowym, kolumny **arrival_time** i **departure_time** powinny przyjąć puste wartości.
  - field_name: stop_sequence
    details:
      - ID: 5
        required: true
        tags: []
        text: |
          Pole **stop_sequence** odzwierciedla kolejność przystanków kursu. Wartości pola **stop_sequence** muszą być nieujemnymi liczbami całokowitymi. Na przykład pierwszy przystanek kursu może przyjąć wartość pola **stop_sequence** 1, drugi **stop_sequence** 23, trzeci **stop_sequence** 40, i tak dalej.
  - field_name: stop_headsign
    details:
      - ID: 6
        required: false
        tags: []
        text: |
          Pole **stop_headsign** zawiera takst, który stosowany jest na oznakowaniu w celu określenia celu kursu. To pole nadpisuje wartość kolumny **trip_headsign** gdy tablica kierunkowa zmiena się w trakcie trwania kursu. Jeśli tekst ten jest stały na całej trasie kursu, użyj **trip_headsign**.
  - field_name: pickup_type
    details:
      - ID: 7
        required: false
        tags: []
        text: |
          Pole **pickup_type** zawiera informacje, czy pasażerowie mogą wsiąść na danym przystanku bez żadnej akcji z ich strony, lub czy wsiadanie pasażerów nie jest możliwe. Pole to również pozwala określić, czy pasażer musi zadzwonić do organizatora, lub czy też musi kooperować z kierowcą, aby móc wsiąść do pojazdu. Prawidłowe wartości tego pola:

          * **0** - Normalny przystanek
          * **1** - Brak możliwości wsiadania
          * **2** - Przed wejściem trzeba poinformować organizatora [np. Telebus]
          * **3** - Przed wejściem trzeba zasygnalizować taką potrzebę kierowcy [np. Na żądanie]

          Domyślną wartością dla tego pola jest **0**.
  - field_name: drop_off_type
    details:
      - ID: 8
        required: false
        tags: []
        text: |
          Pole **drop_off_type** zawiera informacje, czy pasażerowie mogą wysiąść na danym przystanku bez żadnej akcji z ich strony, lub czy wysiadanie pasażerów nie jest możliwe. Pole to również pozwala określić, czy pasażer musi zadzwonić do organizatora, lub czy też musi kooperować z kierowcą, aby móc wysiąść z pojazdu. Prawidłowe wartości tego pola:

          * **0** - Normalny przystanek
          * **1** - Brak możliwości wysiadania
          * **2** - Przed wyjściem trzeba poinformować organizatora [np. Telebus]
          * **3** - Przed wyjściem trzeba zasygnalizować taką potrzebę kierowcy [np. Na żądanie]

          Domyślną wartością dla tego pola jest **0**.
  - field_name: shape_dist_traveled
    details:
      - ID: 9
        required: false
        tags: []
        text: |
          Gdy użyta w pliku stop_times.txt, kolumna **shape_dist_traveled** reprezentuje odległość przystanku od pierwszego punktu kształtu. Pole **shape_dist_traveled** reprezentuje prawdziwy dystans od pierwszego punktu w stopach, kilometrach, lub innej dowolnej jednostce. Dla przykładu, jeśli pojazd od początku kursu do jakiegoś przystanku przemierza 5.25 kilometrów, pole **shape_dist_traveled** dla danego przystanku mogłoby przyjmować wartość „5.25”. Ta informacja potrzebna jest planerom podróży aby móc określić jaką część kształtu narysować dla danego odcinku kursu. Wartości pola **shape_dist_traveled** muszą zwiększać się wraz z wzrostem **stop_sequence**; nie mogą zmniejszać się w przypadku kursów powrotnych. Wartości jednostek użytych w kolumnie **shape_dist_traveled** w pliku stop_times.txt muszą **dokładnie** odzwierciedlać jednostki użyte w pliku [shapes.txt](#shapes).
  - field_name: timepoint
    details:
      - ID: 10
        required: false
        tags: []
        text: |
          Pole **timepoint** wskazuje, czy dany przystanek jest „punktem czasowym”, tj. czy przystanek ma ściśle sutalony rozkład dla tego przystanku, lub czy są to czasy interpolowane/szacunkowe. To pole pozawala producentowi GTFSów podawać czasy inerpolowane z zachowaniem wiedzy lokalnej, ale nadal oznaczać je jako „szacunkowe”. Dla pól z zdefiniowanymi **arrival_time** i **departure_time** następujące wartości są dostępne:

          * **(puste pole)** - Czasy przyjazdu/odjazdu są ściśle ustalone.
          * **0** - Czasy przyjazdu/odjazdu są interpolowane.
          * **1** - Czasy przyjazdu/odjazdu są ściśle ustalone.


          Dla przyjazdów/odjazdów bez zdefiniowanych kolumn **arrival_time** i **departure_time**, czasy przyjazdu/odjazdu będą musiały być interpolowane. Producenci GTFSów mogą oznaczać takie wpisy za pomocą timepoint=0, ale użycie timepoint=1, bez definiowania **arrival_time** i **departure_time** byłoby błędem.
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
