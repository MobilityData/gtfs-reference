---
lang: pl

table_data:
  - field_name: route_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          Pole **route_id** zawiera unikalny indentyfikator reprezentujący linię komunikacyjną. **route_id** jest unikatowe w skali pliku.
  - field_name: agency_id
    details:
      - ID: 2
        required: false
        tags: []
        text: |
          Pole **agency_id** linii zawiera identyfikator placówki odpowiedzialnej za rozkłady linii, zgodnie z pliku [agency.txt](#agency). Pole jest wymagane jeśli w pliku jest zdefiniowana więcej niż jedna placówka.
  - field_name: route_short_name
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          Pole **route_short_name** zawiera krótką nazwę linii. Zazwyczaj to będzie krótki, abstrakcyjny identyfikator jak "32", "100X", "EIP" lub "Zielona". Dzięki krótkiej nazwie pasażer może zidentyfikować linie, ale nazwa ta nie daje informacji o celu linii. Przynajmniej jedna z kolumn *route_short_name* lub *route_long_name* musi zostać zdefiniowana, jeśli możliwe — obie. Jeśli to pole nie może zostać zapełnione, proszę wypełnić *route_long_name* i użyć pustego tekstu w tej kolumnie.
  - field_name: route_long_name
    details:
      - ID: 4
        required: true
        tags: []
        text: |
          Pole **route_long_name** zawiera pełną nazwę linii. Nazwa ta jest generalnie bardziej opisowa od *route_short_name* i zazwyczaj zawiera informacje o krańcach linii. Pole to nie powinno zawierać krótkiej nazwy. Przynajmniej jedna z kolumn *route_short_name* lub *route_long_name* musi zostać zdefiniowana, jeśli możliwe — obie. Jeśli to pole nie może zostać zapełnione, proszę wypełnić *route_short_name* i użyć pustego tekstu w tej kolumnie.
  - field_name: route_desc
    details:
      - ID: 5
        required: false
        tags: []
        text: |
          Pole **route_desc** zawiera opis trasy. Proszę podać opisowe, wysokiej jakości informacje, a nie duplikować nazwy linii. Na przykład: "Pociągi linii **A** operują między stacjami Ulica Inwood-207 (Manhattan) i Aleją Far Rockaway-Mott (Queens) 24 godziny na dobę. Dodatkowo, od około 6 rano do północy, dodatkowe składy linii **A** kursują między Ulicą Inwood-207 a Bulwarem Lefferta (typowo, pociągi kursują na zmianę do Bulwaru Leffereta i Aleją Far Rockaway-Mott)."
  - field_name: route_type
    details:
      - ID: 6
        required: true
        tags: []
        text: |
          Pole **route_type** opsiuje typ taboru kursującej na danej linii komunikacyjnej. Prawidłowe wartości:

          * **0** - Tramwaj, Kolej Lekka. Jakakolwiek kolej lekka, lub w poziomie ulicy, wewnątrz aglomeracji.
          * **1** - Metro, Kolej Podziemna. Jakikolwiek wydzielony system kolei cechujący się wysoką częstotliowścią kursowania.
          * **2** - Kolej. Używany dla kolei międzymiastowej i aglomeracyjnej.
          * **3** - Autobus. Używany zarówno dla systemów miejskich, jak i międzymiastowych.
          * **4** - Prom. Używany zarówno dla systemów krótko- i długodystansowych.
          * **5** - Tramwaj Linowy. Używany dla systemów w poziomie ulicy, gdzie wagony są napędzane liną ukrytą pod płaszczyzną jezdni.
          * **6** - Kolej Gondolowa, Kolej Kabinowa. Typowo używana dla systemów gdzie wagony zawieszone są w powietrzu, na linie.
          * **7** - Funikular, Kolej Linowo-Terenowa. System kolei zaprojektowy do pokonowyania stromych wzniesień.
  - field_name: route_url
    details:
      - ID: 7
        required: false
        tags: []
        text: |
          Pole **route_url** adres URL strony, gdzie można znaleźć dodatkowe informacje o linii. Powinno być różne od *agency_url*. Pole musi być poprawnym adresem URL który zawiera **http**:// lub **https**://, a wszelkie znaki specjalne powinny być odpowiednio zakodowane. Zobacz http://www.w3.org/Addressing/URL/4_URI_Recommentations.html dla pełnego opisu jak stworzyć poprawny adres URL.
  - field_name: route_color
    details:
      - ID: 8
        required: false
        tags: []
        text: |
          W systemach, gdzie linie można rozróżnić za pomocą kolorów, pole **route_color** definiuje taki kolor. Wiele linii może zawierać ten sam kolor (np. w celu rozróżnienia linii zwykłych od pospiesznych). Kolor musi być zdefiniowany jako sześcio-cyfrowa liczba szesnastkowa, np. 00FFFF. Jeśli pole nie jest zdefiniowane, domyślnym kolorem jest biały (FFFFFF). Różnica kolorów między **route_color**, a **route_text_color** powinna zapewniać odpowiedni konstrast, aby dało się rozróżnić tekst od tła na wyświetlaczach czarno-białych. Narzędzie "[W3C Techniques for Accessibility Evaluation And Repair Tools document](https://www.w3.org/TR/AERT#color-contrast)" zawiera pomocny algorytm w celu kalkulowania kontrastu. Istnieją też inne narzędzia pozwalające sprawdzić taki konstrast, np. "[snook.ca Color Contrast Check application](http://snook.ca/technical/colour_contrast/colour.html#fg=33FF33,bg=333333)".
  - field_name: route_text_color
    details:
      - ID: 9
        required: false
        tags: []
        text: |
          Pole **route_text_color** zawiera specjalnie wybrany kolor, w którym wyświetlany będzie tekst na kolorze linii (route_color). Kolor musi być zdefiniowany jako sześcio-cyfrowa liczba szesnastkowa, np. FFD700. Jeśli pole nie jest zdefiniowane, domyślnym kolorem tekstu jest czarny (000000). Różnica kolorów między **route_color**, a **route_text_color** powinna zapewniać odpowiedni konstrast, aby dało się rozróżnić tekst od tła na wyświetlaczach czarno-białych.
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
