---
lang: pl

table_data:
  - field_name: fare_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **fare_id** zaiwera identyfikator biletu. Wartość tego pola musi być sgodna z plikiem [fare_attributes.txt](#fare_attributes).
  - field_name: route_id
    details:
      - ID: 2
        required: false
        tags: []
        text: |
          Pole **route_id** wskazuje na których liniach bilet jest ważny. Wartości tego pola muszą być zgodne z plikiem [routes.txt](#routes). Jeśli bilet jest ważny na wielu liniach, proszę stworzyć osobny wiersz w pliku fare_rules.txt dla każdej z tych linii.

          Na przykład, jeśli bilet „b” jest ważny na liniach „1”, „2” i „3”, plik fare_rules.txt zawierałby następujące wiersze:

          | `fare_id,route_id` |
          | `b,1` |
          | `b,2` |
          | `b,3` |
  - field_name: origin_id
    details:
      - ID: 3
        required: false
        tags: []
        text: |
          Pole **origin_id** definiuje bilet jako „ważny dla podróży z jakieś strefy”. Identyfikatory stref muszą być zgodne z plikiem [stops.txt](#stops). Jeśli bilet jest ważny dla podróży z kilku stref, każda z nich musi mieć osobny wiersz.

          Na przykład, jeśli bilet „c” jest ważny dla wszystkich podróży z stref „2” i „8”, plik fare_rules.txt zawierałby następujące wiersze:

          | `fare_id,route_id,origin_id` |
          | `c,,2` |
          | `c,,8` |
  - field_name: destination_id
    details:
      - ID: 4
        required: false
        tags: []
        text: |
          Pole **destination_id** definiuje bilet jako „ważny dla podróży do jakieś strefy”. Identyfikatory stref muszą być zgodne z plikiem [stops.txt](#stops). Jeśli bilet jest ważny dla podróży do kilku stref, każda z nich musi mieć osobny wiersz.

          Na przykład można użyć pól **origin_id** i **destination_id** aby określić, że bilet „d” jest ważny dla wszystkich podróży między strefami 3↔4 i 3↔5. W takim przypadku plik fare_rules.txt zawierałby następujące wiersze:

          | `fare_id,route_id,origin_id,destination_id` |
          | `d,,3,4` |
          | `d,,3,5` |
  - field_name: contains_id
    details:
      - ID: 5
        required: false
        tags: []
        text: |
          Pole **contains_id** definiuje bilet jako „ważny tylko dla podróży wewnątrz jakiejś strefy”. Identyfikatory stref muszą być zgodne z plikiem [stops.txt](#stops). Jeśli bilet jest ważny dla podróży po kilku strfach, każda z nich musi mieć osobny wiersz.

          Na przykład, jeśli bilet „e” jes ważny na linii „A” w strefach 5, 6 i 7, plik fare_rules.txt zawierałby następujące wiersze:

          | `fare_id,route_id,origin_id,destination_id,contains_id` |
          | `e,A,,,5` |
          | `e,A,,,6` |
          | `e,A,,,7` |

          Ponieważ wszytskie strefy wymienione w **contains_id** muszą należeć do podróży aby bilet był uznany za ważny na jakąś podróż, trasa linii A przejeżdżająca tylk przez strefy 5 i 6 **nie** miałaby nadanego biletu „e”. Po więcej przykładów modelowania systemów biletowych, zobacz artykuł [FareExamples](https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) na wiki projektu GoogleTransitDataFeed.

---
Plik: **Opcjonalny**

Tabela fare_rules pozwala zdefiniować jak bilety z pliku in fare_attributes.txt mogą być wykorzystywane podczas podróży. Większość systemów trafyowych korzysta z jakieś kombinacji takich zasad:

* Taryfa polega na stacjach początkowych i końcowych.
* Taryfa polega na strefach, po których odbywa się podróż.
* Taryfa zależna jest od linii po których odbywa się podróż.

Po więcej przykładów jak modelować trayfy biletowe w GTFSie za pomocą plików fare_rules.txt and fare_attributes.txt, zobacz stronę [FareExamples](https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) na wiki projektu GoogleTransitDataFeed.

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
