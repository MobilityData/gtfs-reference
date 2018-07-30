---
lang: pl

table_data:
  - field_name: shape_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **shape_id** definiuje identyfikator kształtu trasy przejazdu.
  - field_name: shape_pt_lat
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          Pole **shape_pt_lat** łączy szerokość geograficzną punktu kształtu z **shape_id**. Wartość pola musi być prawidłowa w systemie odniesienia WGS 84. Każdy wiersz w pliku shapes.txt odpowiada punktowi należącemu do jakiegoś kształtu (który reprezentuje faktyczną trasę przejazdu pojazdu).

          Na przykład, jeśli kształt „A->Lotnisko” ma mieć zdefiniowane trzy punkty, plik shapes.txt może zawierać następujące wiersze, aby taki kształt zdefiniować:

          | `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence` |
          | `A->Lotnisko,37.61956,-122.48161,0` |
          | `A->Lotnisko,37.64430,-122.41070,6` |
          | `A->Lotnisko,37.65863,-122.30839,11` |
  - field_name: shape_pt_lon
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **shape_pt_lon** łączy długość geograficzną punktu kształtu z **shape_id**. Wartość pola musi być prawidłowa w systemie odniesienia WGS 84, tj. być w zakresie 180 — -180. Każdy wiersz w pliku shapes.txt odpowiada punktowi należącemu do jakiegoś kształtu (który reprezentuje faktyczną trasę przejazdu pojazdu).

          Na przykład, jeśli kształt „A->Lotnisko” ma mieć zdefiniowane trzy punkty, plik shapes.txt może zawierać następujące wiersze, aby taki kształt zdefiniować:

          | `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence` |
          | `A->Lotnisko,37.61956,-122.48161,0` |
          | `A->Lotnisko,37.64430,-122.41070,6` |
          | `A->Lotnisko,37.65863,-122.30839,11` |
  - field_name: shape_pt_sequence
    details:
      - ID: 4
        required: true
        tags: []
        text: |
          Pole **shape_pt_sequence** definiuje kolejność punktów w kształcie. Wartości **shape_pt_sequence** muszą być nieujemnymi liczbami całkowitymi i zwiększać się wraz z przebiegiem kształtu.

          Na przykład, jeśli kształt „A->Lotnisko” ma mieć zdefiniowane trzy punkty, plik shapes.txt może zawierać następujące wiersze, aby taki kształt zdefiniować:

          | `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence` |
          | `A->Lotnisko,37.61956,-122.48161,0` |
          | `A->Lotnisko,37.64430,-122.41070,6` |
          | `A->Lotnisko,37.65863,-122.30839,11` |
  - field_name: shape_dist_traveled
    details:
      - ID: 5
        required: false
        tags: []
        text: |
          Gdy użyta w pliku shapes.txt, kolumna **shape_dist_traveled** reprezentuje odległość punktu kształtu od pierwszego punktu. Pole **shape_dist_traveled** reprezentuje prawdziwy dystans od pierwszego punktu w stopach, kilometrach, lub innej dowolnej jednostce. Dla przykładu, jeśli pojazd od początku kształtu do jakiegoś punktu przemierza 5.25 kilometrów, pole **shape_dist_traveled** dla danego punktu mogłoby przyjmować wartość „5.25”. Ta informacja potrzebna jest planerom podróży aby móc określić jaką część kształtu narysować dla danego odcinku kształtu. Wartości pola **shape_dist_traveled** muszą zwiększać się wraz z wzrostem **shape_pt_sequence**; nie mogą zmniejszać się w przypadku kursów powrotnych. Wartości jednostek użytych w kolumnie **shape_dist_traveled** w pliku [stop_times.txt](#stop_times) muszą **dokładnie** odzwierciedlać jednostki użyte w pliku shapes.txt.

          Na przykład, jeśli jakiś pojazd kursuje trasą kształtu „A->Lotnisko”, wartości dodatkowej kolumny **shape_dist_traveled** (tu w kilometrach) wyglądałyby następująco:

          | `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence,shshape_dist_traveled` |
          | `A->Lotnisko,37.61956,-122.48161,0,0` |
          | `A->Lotnisko,37.64430,-122.41070,6,6.8310` |
          | `A->Lotnisko,37.65863,-122.30839,11,15.8765` |
---
Plik: **Opcjonalny**

shapes.txt pozwala zdefiniować prawdziwą trasę przejazdu pojazdu na linii. Prześledzenie punktów kształtów po kolei tworzy całą trasę przejazdu. Punkty nie muszą pokrywać się z pozycjami przystanków.

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
