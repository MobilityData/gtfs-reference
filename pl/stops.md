---
lang: pl

table_data:
  - field_name: stop_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **stop_id** zawiera identyfikator, który unikalnie identyfikuje przystanek, stację, stację-matkę i wejście. Wiele linii może korzystać z tego samego przystanku. Pole **stop_id** jest traktowane jako klucz unikatowy tego wpisu, więc musi być traktowane jako „unikatowe w skali pliku”.
  - field_name: stop_code
    details:
      - ID: 2
        required: false
        tags: []
        text: |
          Pole **stop_code** zawiera krótki tekst, który **unikatowo** identyfikuje przystanek dla pasażerów. Takie kody są często wykorzystywane w systemach informacji pasażerskiej na telefon i w rozkładach drukowanych aby ułatwić pasażerom uzyskanie informacji „na-żywo” o odjazdach pojazdów z przystanku. Pole **stop_code** może być takie samo jak **stop_id**, jeśli jest ono powszechnie stosowane przez pasażerów. To pole powinno zostać puste jeśli nie ma takiego kodu.
  - field_name: stop_name
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **stop_name** zawiera nazwę przystanku/stacji, stacji-matki, wejścia. Proszę użyć nazwy która będzie zarówno rozumiana przez miejscowych, jak i turystów. Ponieważ to pole może być wykorzystywane przez systemy Text-To-Speach, staraj się nie umieszczać skrótów w tym polu (**skrótowce** powinny zostać, jeśli tak są prezentowane użytkownikom).
  - field_name: stop_desc
    details:
      - ID: 4
        required: false
        tags: []
        text: |
          Pole **stop_desc** zawiera opis przystanku/stacji. Proszę podać opisowe, wysokiej jakości informacje, a nie duplikować nazwy przystanku/stacji.
  - field_name: stop_lat
    details:
      - ID: 5
        required: true
        tags: []
        text: |
          Pole **stop_lat** zawiera szerokość geograficzną przystanku/stacji, stacji-matki lub wejścia. Pole musi być prawidłowe w systemie odniesienia WGS 84.
  - field_name: stop_lon
    details:
      - ID: 6
        required: true
        tags: []
        text: |
          Pole **stop_lon** zawiera długość geograficzną przystanku/stacji, stacji-matki lub wejścia. Pole musi być prawidłowe w systemie odniesienia WGS 84, tj. musi być w zakresie 180 — -180.
  - field_name: zone_id
    details:
      - ID: 7
        required: false
        tags: []
        text: |
          Pole **zone_id** definuje identyfikator strefy biletowej do której przynależy dany przystanek. Identyfikatory stref biletowych są wykorzystywane przez plik [fare_rules.txt](#fare_rules); jeśli taryfa polega na strefach biletowych. Jeśli wiersz reprezentucje stację (zobacz location_type), pole **zone_id** jest ignorowane.
  - field_name: stop_url
    details:
      - ID: 8
        required: false
        tags: []
        text: |
          Pole **stop_url** zawiera adres strony internetowej z informacjami o danym przystanku. Wartość tego pola powinna różnić się od **agency_url** i od **route_url**. Pole musi być poprawnym adresem URL który zawiera **http://** lub **https://**, a wszelkie znaki specjalne powinny być odpowiednio zakodowane. Zobacz http://www.w3.org/Addressing/URL/4_URI_Recommentations.html dla pełnego opisu jak stworzyć poprawny adres URL.
  - field_name: location_type
    details:
      - ID: 9
        required: false
        tags: []
        text: |
          Pole **location_type** rozróżnia wpisy w pliku stops.txt na przystanki, stacje i wejścia do stacji. Jeśli kolumna **location_type** nie jest zdefiniowana, lub wartość tego pola jest pusta, ten wiersz będzie traktowany jak zwykły przystanek. Stacje mają inne właściwości od przystanków podczas wyświetlania w aplikacjach korzystających z formatu GTFS. Pole to przyjmujue następujące wartości:

          * **0** (lub puste) - Przystanek. Miejsce, gdzie pojazdy się zatrzymują, a pasażerowie mogą wsiąść/wysiąść.
          * **1** - Stacja. Fizyczna struktura lub obszar zawierający więcej niż jeden przystanek, które są postrzegane przez pasażerów jako jeden obiekt.
          * **2** - Wejście/Wyjście. Miejsce na poziomie ulicy, z którego pasażer może zejść/wejść na poziom z którego odbywają odjazdy. Taki wiersz musi również zawierać zdefiniowany **parent_station**.

          **Uwaga:** Dwa przystanki naprzeciwko siebie nie tworzą „stacji” — zatem zespoły przystanków **nie powinny** być łączone za pomocą stacji-matki. W polskich realiach jedynie wieloperonowe stacje/przystanki kolejowe oraz dworce autobusowe powinny być łączone za pomocą stacji-matki. Po więcej informacji zobacz: https://support.google.com/transitpartners/answer/6377423?ref_topic=6377359
  - field_name: parent_station
    details:
      - ID: 10
        required: false
        tags: []
        text: |
          Dla przystanków należących do stacji, pole **parent_station** definuje idenyfikator stacji-matki. Taka stacja-matka powinna zawierać location_type=1.
        example_table: |
          <table>
            <thead>
              <tr>
                <th>Ten wiersz reprezentuje…</th>
                <th>location_type wpisu…</th>
                <th>parent_station wpisu</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Przystanek należący do stacji</td>
                <td>0 (lub puste)</td>
                <td>Identyfikator stacji-matki, której location_type to „1”.</td>
              </tr>
              <tr>
                <td>Przystanek nienależący do większej struktury</td>
                <td>0 (lub puste)</td>
                <td>Pusty wpis — ten prystanek nie przynależy do żadnej stacji-matki.</td>
              </tr>
              <tr>
                <td>Stacja</td>
                <td>1</td>
                <td>Pusty wpis — stacje-matki nie mogą przynależeć do innych stacji-matek.</td>
              </tr>
            </tbody>
          </table>
  - field_name: stop_timezone
    details:
      - ID: 11
        required: false
        tags: []
        text: |
          Pole **stop_timezone** informuje o strefie czasowej w której znajduje się dany przystanek. Proszę odwołać się do http://en.wikipedia.org/wiki/List_of_tz_zones po listę prawidłowych wartości. Jeśli pole to jest pominięte (lub zawiera pustą wartość), zakłada się, że przystanek należy do strefy czasowej zdefiniowanej w **agency_timezone**, w pliku [agency.txt](#agency). Jeśli przystanek przynależy do stacji-matki, pod uwagę brana jest tylko wartość pola **stop_timezone** stacji-matki. Jeśli stacja-matka nie ma zdefiniowanego **stop_timezone**, wszystkie należące do niej przystanki definiuje się jako należące do strfy czasowej z **agency_timezone**, nawet jeśli każdy pojedyńczy przystanek ma zdefiniowaną wartość w polu **stop_timezone**. Innymi słowy, jeśli przystanek ma zdefiniowaną wartość w polu **parent_station**, cokolwiek wpisane w **stop_timezone** jest ignorowane. Nawet jeśli podawane są wartości w **stop_timezone**, czasy w pliku [stop_times.txt](#stop_times) muszą być liczone od „południe-12h” strefy podanej w **agency_timezone** in agency.txt. Dzięki temu wartości czasów zawsze rosną z biegiem kursu, nawet jeśli pojazd przemierza wiele stref czasowych.
  - field_name: wheelchair_boarding
    details:
      - ID: 12
        required: false
        tags: []
        text: |
          Pole **wheelchair_boarding** informuje czy stacja/przystanek/wejście jest dostępne dla osób poruszających się na wózkach inwalidzkich. Pole to przyjmuje następujące wartości:

          * **0** (lub puste) - Nie ma informacji odnośnie dostępności danego przystanku
          * **1** - Przystanek jest dostępny dla osb poruszających się na wózkach
          * **2** - Przystanek nie jest dostępny dla osób poruszających się na wózkach

          Jeśli przystanek należy do większej struktury i ma zdefiniowaną wartość w polu **parent_station**, **wheelchair_boarding** przystanku ma następującą semantykę:

          * **0** (lub puste) - Informacja o dostępności przystanku jest dziedziczona po polu **wheelchair_boarding** stacji-matki
          * **1** - Istnieje ścieżka dojścia do przystanku z poziomu ulicy dla osób niepoełnosprawnych
          * **2** - Osoby poruszające się na wózku nie mogą dostać się na przystanek z poziomu ulicy

          Natomiast dla wejść/wyjść, **wheelchair_boarding** jest interpretowane następująco:

          * **0** (lub puste) - Informacja o dostępności przystanku jest dziedziczona po polu **wheelchair_boarding** stacji-matki
          * **1** - Za pomocą tego wejścia osoby poruszające się na wózkach mogą dostać się do miejsca odjazdu pojazdów z poziomu ulicy, np. za pomocą wind.
          * **2** - Za pomocą tego wejścia osoby niepełnosprawne nie mogą dostać się do miejsca odjazdu pojazdów.
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
