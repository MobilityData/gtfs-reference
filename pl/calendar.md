---
lang: pl

table_data:
  - field_name: service_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **service_id** zawiera unikalny identyfikator pozawalający rozróżnić typy kursowania (kalendarze). Jeden identyfikator może się pojawić tylko raz w pliku calendar.txt. To pole jest unikatowe w skali pliku. To pole jest wykorzystywane przez plik [trips.txt](#trips).
  - field_name: monday
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          Pole **monday** zawiera wartość binarną informującą czy dany kalendarz jest aktywy w każdy poniedziałek.

          * Wartość **1** wskazuje, że dany kalendarz jest aktywny w każdy poniedziałek zakresu. (Zakres dat jest definiowany za pomocą pól **start_date** i **end_date**.)
          * Wartość **0** wskazuje, że dany kalendarz nie jest aktywny w każdy poniedziałek zakresu.

          **Uwaga:** Odstępstwa od standardowych schematów, takie jak święta, są definioawne w pliku [calendar_dates.txt](#calendar_dates).
  - field_name: tuesday
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **tuesday** zawiera wartość binarną informującą czy dany kalendarz jest aktywy w każdy wtorek.

          * Wartość **1** wskazuje, że dany kalendarz jest aktywny w każdy wtorek zakresu. (Zakres dat jest definiowany za pomocą pól **start_date** i **end_date**.)
          * Wartość **0** wskazuje, że dany kalendarz nie jest aktywny w każdy wtorek zakresu.

          **Uwaga:** Odstępstwa od standardowych schematów, takie jak święta, są definioawne w pliku [calendar_dates.txt](#calendar_dates).
  - field_name: wednesday
    details:
      - ID: 4
        required: true
        tags: []
        text: |
          Pole **wednesday** zawiera wartość binarną informującą czy dany kalendarz jest aktywy w każdą środę.

          * Wartość **1** wskazuje, że dany kalendarz jest aktywny w każdą środę zakresu. (Zakres dat jest definiowany za pomocą pól **start_date** i **end_date**.)
          * Wartość **0** wskazuje, że dany kalendarz nie jest aktywny w każdą środę zakresu.

          **Uwaga:** Odstępstwa od standardowych schematów, takie jak święta, są definioawne w pliku [calendar_dates.txt](#calendar_dates).
  - field_name: thursday
    details:
      - ID: 5
        required: true
        tags: []
        text: |
          Pole **thursday** zawiera wartość binarną informującą czy dany kalendarz jest aktywy w każdy czwartek.

          * Wartość **1** wskazuje, że dany kalendarz jest aktywny w każdy czwartek zakresu. (Zakres dat jest definiowany za pomocą pól **start_date** i **end_date**.)
          * Wartość **0** wskazuje, że dany kalendarz nie jest aktywny w każdy czwartek zakresu.

          **Uwaga:** Odstępstwa od standardowych schematów, takie jak święta, są definioawne w pliku [calendar_dates.txt](#calendar_dates).
  - field_name: friday
    details:
      - ID: 6
        required: true
        tags: []
        text: |
          Pole **friday** zawiera wartość binarną informującą czy dany kalendarz jest aktywy w każdy piątek.

          * Wartość **1** wskazuje, że dany kalendarz jest aktywny w każdy piątek zakresu. (Zakres dat jest definiowany za pomocą pól **start_date** i **end_date**.)
          * Wartość **0** wskazuje, że dany kalendarz nie jest aktywny w każdy piątek zakresu.

          **Uwaga:** Odstępstwa od standardowych schematów, takie jak święta, są definioawne w pliku [calendar_dates.txt](#calendar_dates).
  - field_name: saturday
    details:
      - ID: 7
        required: true
        tags: []
        text: |
          Pole **saturday** zawiera wartość binarną informującą czy dany kalendarz jest aktywy w każdą sobotę.

          * Wartość **1** wskazuje, że dany kalendarz jest aktywny w każdą sobotę zakresu. (Zakres dat jest definiowany za pomocą pól **start_date** i **end_date**.)
          * Wartość **0** wskazuje, że dany kalendarz nie jest aktywny w każdą sobotę zakresu.

          **Uwaga:** Odstępstwa od standardowych schematów, takie jak święta, są definioawne w pliku [calendar_dates.txt](#calendar_dates).
  - field_name: sunday
    details:
      - ID: 8
        required: true
        tags: []
        text: |
          Pole **sunday** zawiera wartość binarną informującą czy dany kalendarz jest aktywy w każdą niedzielę.

          * Wartość **1** wskazuje, że dany kalendarz jest aktywny w każdą niedzielę zakresu. (Zakres dat jest definiowany za pomocą pól **start_date** i **end_date**.)
          * Wartość **0** wskazuje, że dany kalendarz nie jest aktywny w każdą niedzielę zakresu.

          **Uwaga:** Odstępstwa od standardowych schematów, takie jak święta, są definioawne w pliku [calendar_dates.txt](#calendar_dates).
  - field_name: start_date
    details:
      - ID: 9
        required: true
        tags: []
        text: |
          Pole **start_date** definiuje datę rozpoczęcia danego schematu kursowania. Wartość pola **start_date** powinna być w postaci YYYYMMDD, np. 20151230.
  - field_name: end_date
    details:
      - ID: 10
        required: true
        tags: []
        text: |
          Pole **end_date** definiuje datę zakończenia danego schematu kursowania. Data ta też jest częścią kalendarza. Wartość pola **start_date** powinna być w postaci YYYYMMDD, np. 20160220.
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
