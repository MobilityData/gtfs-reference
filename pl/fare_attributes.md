---
lang: pl

table_data:
  - field_name: fare_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **fare_id** zawiera unikalny identyfikator biletu. Pole **fare_id** jest unikatowe w skali pliku.
  - field_name: price
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          Pole **price** definiuje cenę biletu, w walucie zdefiniwanej w kolumnie **currency_type**.
  - field_name: currency_type
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **currency_type** opisuje walutę, w której podawane są ceny biletów. Pole to musi zawierać wartość zgodną z alfabetyczną listą kodów walut, [ISO 4217](http://en.wikipedia.org/wiki/ISO_4217).
  - field_name: payment_method
    details:
      - ID: 4
        required: true
        tags: []
        text: |
          Pole **payment_method** definiuje sposób opłaty tego biletu. Pole przyjmuje następujące wartości:

          * **0** - Opłata jest pobierana w pojeździe (np. za pomocą skasowania biletu).
          * **1** - Przejazd jest opłacany z góry, np. bilet jest wydawany na konkrety odcinek konretnego kursu.
  - field_name: transfers
    details:
      - ID: 5
        required: true
        tags: []
        text: |
          Pole **transfers** definiuje możliwą liczbę przesiadek na podstawie danego biletu. Kolumna ta może przyjmować następujące wartości:

          * **0** - Na podstawie tego biletu pasażer nie może sie przesiadać
          * **1** - Pasażer może przesiąść się tylko raz
          * **2** - Pasażer może przesiąść się tylko dwa razy
          * **(puste)** - Jeśli pole jest puste, pasażer może przesiadać się do woli.
  - field_name: agency_id
    details:
      - ID: 6
        required: false
        tags: []
        text: |
          Wymagane w przypadku definiowania wielu podmiotów w pliku [agency.txt](#agency). Każdy bilet musi mieć zdefiniowaną przynależność do jakiegoś organizatora. Wartość tego pola musi być zgodna z plikiem [agency.txt](#agency).
  - field_name: transfer_duration
    details:
      - ID: 7
        required: false
        tags: []
        text: |
          Pole **transfer_duration** definiuje dozwolony czas między przsiadkami, podany w sekundach. Jeśli pole **transfers** biletu zawiera wartość „0” lub jest puste, **transfer_duration** jak długo bilet zachowuje ważność. Jeśli bilet nie ma limitu czasowego (np. bilety jednorazowe), **transfer_duration** powinno pozostać puste.
---
Plik: **Opcjonalny**

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
        <td>{% if detail.required %}Required{% else %}Optional{% endif %}</td>
        <td>{{ detail.text | markdownify }}{% if detail.example_table %}<div class="table-wrapper">{{ detail.example_table }}</div>{% endif %}</td>
      </tr>
      {% endfor %}
    {% endfor %}
    </tbody>
  </table>
</div>
