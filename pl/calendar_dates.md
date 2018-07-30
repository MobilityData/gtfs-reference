---
lang: pl

table_data:
  - field_name: service_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **service_id** zawiera unikalny identyfikator pozawalający rozróżnić typy kursowania (kalendarze). Każda para (service_id, date) może pojawić się tylko raz w pliku calendar_dates.txt. Jeśli pole **service_id** pojawia się zarówno w pliku calendar.txt, jak i calendar_dates.txt, to informacje zawarte w calendar_dates.txt modyfikują infromacje zdefiniowane przez plik [calendar.txt](#calendar). To pole jest wykorzystywane przez plik [trips.txt](#trips).
  - field_name: date
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          Pole **date** definiuje datę, gdy występuje odchylenie od standardowego schematu kursowania. Kolumna **exception_type** definiuje typ odchylenia. Wartość pola **date** powinna być w formacie YYYYMMDD, np. 20151225.
  - field_name: exception_type
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **exception_type** definiuje typ odchylenia od standardowego schematu kursowania, tj. czy kalendarz jest aktywny w dany dzień.

          * Wartość **1** wskazuje, że ten kalendarz został dodany w podanym dniu.
          * Wartość **2** wskazuje, że ten kalendarz został usunięty w podanym dniu.

          Dla przykładu, załóżmy, że jakaś linia ma dwa kalendarze: "dni robocze", oraz "weekedny i święta". W jakieś święto, wypadające w dzień roboczy, w pliku calendar_dates.txt znalazłyby się wpis dodający **service_id** kalendarza weekendowego w dane święto, oraz wpis usuwający roboczy **service_id** danego dnia.
---
Plik: **Opcjonalny**

Tabela calendar_dates pozawala dezaktywować/aktywować kalendarze według poszczególnych dat. Można go użyć na dwa sposoby.

* Zalecany: Użycie calendar_dates.txt w parze z [calendar.txt](#calendar), gdzie calendar_dates.txt definiuje wszelkie odchylenia od pliku [calendar.txt](#calendar). Jeśli Twoje rozkłady są generalnie regularne, to użycie pliku calendar_dates.txt tylko do zaznaczania odchyleń (np. podczas świąt lub ferii), jest czytelniejsze.
* Alternatywny: Opuść plik [calendar.txt](#calendar), i dodaj WSZYSTKIE daty kursowania w pliku calendar_dates.txt. Jeśli Twoje rozkłady różnią się w skali miesiąca, lub jeśli chcesz automatycznie eksportować kalendarze bez definiowania standardowych schematów kursowania, może okazać się to lepszym podejściem.

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
