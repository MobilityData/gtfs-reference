---
lang: pl

table_data:
  - field_name: feed_publisher_name
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **feed_publisher_name** definuje nazwę podmiatu publikującego plik GTFS. (To może być nazwa jednego z organizatorów, **agency_name**, jak podano w pliku [agency.txt](#agency)). Aplikacje korzystające z plików GTFS będą podawać tę nazwę jako odpowiedzialną za utrzymywanie rozkładów w pliku GTFS.
  - field_name: feed_publisher_url
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          Pole **feed_publisher_url** definiuje adres strony internetowej podmiotu odpowiedzialnego za plik GTFS. (To może być strona jednego z organizatorów, **agency_url**, jak podano w pliku [agency.txt](#agency)).
          Pole musi być poprawnym adresem URL który zawiera **http://** lub **https://**, a wszelkie znaki specjalne powinny być odpowiednio zakodowane. Zobacz http://www.w3.org/Addressing/URL/4_URI_Recommentations.html dla pełnego opisu jak stworzyć poprawny adres URL.
  - field_name: feed_lang
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **feed_lang** zawiera kod IETF BCP 47 języka w którym publikowany jest dany plik GTFS. To ustawienie pozwala aplikacjom korzystającym z pliku GTFS odpowiednio kapitalizować nazwy, oraz odpowiednio stosować różne inne regionalne preferencje. Aby uzyskać więcej informacji na temat IETF BCP 47, proszę odwołać się do http://www.rfc-editor.org/rfc/bcp/bcp47.txt i http://www.w3.org/International/articles/language-tags/.
  - field_name: feed_start_date
    details:
      - ID: 4
        required: false
        tags: []
        text: |
          Plik GTFS zawiera kompletne i dokładne informacje rozkładowe na okres od **feed_start_date** do **feed_end_date** (włącznie). Oba pole powinny zawierać datę w formacie YYYYMMDD, tak jak w pliku [calendar.txt](#calendar). **feed_start_date** nie może być większy od **feed_end_date**. Producenci GTFSów są zachęcani do uzupełniania rozkładów poza zadanymi datami, ale aplikacje korzystające z GTFS nie powinny traktować takich rozkładów jako pewnych. Jeśli **feed_start_date** lub **feed_end_date** nie pokrywają się z pierwszym/ostatnim dniem kursowania z plików [calendar.txt](#calendar)/[calendar_dates.txt](#calendar_dates), oznacza to, że w dniach w zakresach **feed_start_date** — „pierwszy dzień z aktywnym kalendarzem” i/lub „ostatni dzień z aktywnym kalendarzem” — **feed_end_date** nie ma żadnych aktywnych kursów.
  - field_name: feed_end_date
    details:
      - ID: 5
        required: false
        tags: []
        text: |
          (zobacz wyżej)
  - field_name: feed_version
    details:
      - ID: 6
        required: false
        tags: []
        text: |
          Producent pliku GTFS może wstawić tu tekst wskazujący na wersję archiwum GTFS. Aplikacje korzystające powinny wyświetlać tę wartość w celu identyfikacji, czy został pobrany najnowszy plik z rozkładami jazdy.
---
Plik: **Opcjonalny**

Ten plik zawiera informacje o samym GTFSie, a nie o rozkładach jazdy, które opisuje. Format GTFS posiada plik [agency.txt](#agency), aczkolwiek służy on do opisywania podmiotów odpowiedzialnych za rozkałady/taryfę na liniach. W niektórych przypadkach, pliki GTFS są publikowane przez inne podmioty (np. strony zajmujące się konwersją danych do GTFSa). Do tego, plik feed_info.txt zawiera kilka ustawień, które odnoszą się do całego archiwum.

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
