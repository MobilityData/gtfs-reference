---
lang: pl

table_data:
  - field_name: from_stop_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **from_stop_id** zawiera identyfikator przystanku na którym rozpoczyna się połączenia dwóch linii. Wartość tego pola musi być zgodna z plikiem [stops.txt](#stops). Jeśli **from_stop_id** reprezentuje stacje-matkę, połączenia dotyczą wszystkich przystanków należących do danej stacji.
  - field_name: to_stop_id
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          Pole **to_stop_id** zawiera identyfikator przystanku na którym kończy się połączenie dwóch linii. Wartość tego pola musi być zgodna z plikiem [stops.txt](#stops). Jeśli **to_stop_id** reprezentuje stacje-matkę, połączenia dotyczą wszystkich przystanków należących do danej stacji.
  - field_name: transfer_type
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **transfer_type** opisuje typ połączenia między parą przystanków (from_stop_id, to_stop_id). Pole to przyjmuje następujące wartości:

          * **0** (lub puste) - Para przystanków stanowi rekomendowane miejsce przesiadek
          * **1** - Para przystanków jest skomunikowana — pojazdy odjeżdżające będą oczekiwać na pojazdy odjeżdżające, tak, żeby przesiadka była zawsze możliwa
          * **2** - Połączenie między kursami wymaga różnicy czasu opisanej za pomocą kolumny **min_transfer_time**
          * **3** - Połączenie między tymi przystankami nie jest możliwe
  - field_name: min_transfer_time
    details:
      - ID: 4
        required: false
        tags: []
        text: |
          Kiedy połączenie wymaga jakiegoś czasu między kursami (**transfer_type**=2), pole **min_transfer_time** definiuje czas potrzebny aby zapewnić przesiadkę między kursami. Wartość w polu **min_transfer_time** musi pozwalać na spokojną przesiadkę dla typowego pasażera wraz z uwzględnieniem buforu, jeśli któryś pojazd się spóźni.

          Wartość pola **min_transfer_time** musi być wartością wyrażoną w sekundach i być nieujemną liczbą całkowitą.
---
Plik: **Opcjonalny**

Planery podróży normalnie obliczają miejsca przesiadek na podstawie bliskości przystanków na trasach kursów. Dla potencjalnego manualnego zdefionwania polecanych miejsc przesiadek, plik transfer.txt definiuje zasady tworzenia połączeń między kursami.

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
