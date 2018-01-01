---
lang: fr

table_data:
  - field_name: fare_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The **fare_id** field contains an ID that uniquely identifies a fare class. This value is referenced from the [fare_attributes.txt](#fare_attributes) file.
  - field_name: route_id
    details:
      - ID: 2
        required: false
        tags: []
        text: |
          The **route_id** field associates the fare ID with a route. Route IDs are referenced from the [routes.txt](#routes) file. If you have several routes with the same fare attributes, create a row in fare_rules.txt for each route.

          For example, if fare class "b" is valid on route "TSW" and "TSE", the fare_rules.txt file would contain these rows for the fare class:

          | `b,TSW` |
          | `b,TSE` |
  - field_name: origin_id
    details:
      - ID: 3
        required: false
        tags: []
        text: |
          The **origin_id** field associates the fare ID with an origin zone ID. Zone IDs are referenced from the [stops.txt](#stops) file. If you have several origin IDs with the same fare attributes, create a row in fare_rules.txt for each origin ID.

          For example, if fare class "b" is valid for all travel originating from either zone "2" or zone "8", the fare_rules.txt file would contain these rows for the fare class:

          | `b, , 2` |
          | `b, , 8` |
  - field_name: destination_id
    details:
      - ID: 4
        required: false
        tags: []
        text: |
          The **destination_id** field associates the fare ID with a destination zone ID. Zone IDs are referenced from the [stops.txt](#stops) file. If you have several destination IDs with the same fare attributes, create a row in fare_rules.txt for each destination ID.

          For example, you could use the origin_ID and destination_ID fields together to specify that fare class "b" is valid for travel between zones 3 and 4, and for travel between zones 3 and 5, the fare_rules.txt file would contain these rows for the fare class:

          | `b, , 3,4` |
          | `b, , 3,5` |
  - field_name: contains_id
    details:
      - ID: 5
        required: false
        tags: []
        text: |
          The **contains_id** field associates the fare ID with a zone ID, referenced from the [stops.txt](#stops) file. The fare ID is then associated with itineraries that pass through every contains_id zone.

          For example, if fare class "c" is associated with all travel on the GRT route that passes through zones 5, 6, and 7 the fare_rules.txt would contain these rows:

          | `c,GRT,,,5` |
          | `c,GRT,,,6` |
          | `c,GRT,,,7` |

          Because all contains_id zones must be matched for the fare to apply, an itinerary that passes through zones 5 and 6 but not zone 7 would not have fare class "c". For more detail, see [FareExamples](https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) in the GoogleTransitDataFeed project wiki.

---
File: **Optional**

The fare_rules table allows you to specify how fares in fare_attributes.txt apply to an itinerary. Most fare structures use some combination of the following rules:

* Fare depends on origin or destination stations.
* Fare depends on which zones the itinerary passes through.
* Fare depends on which route the itinerary uses.

For examples that demonstrate how to specify a fare structure with fare_rules.txt and fare_attributes.txt, see [FareExamples](https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) in the GoogleTransitDataFeed open source project wiki.

<div class="table-wrapper">
  <table class="recommendation">
    <thead>
      <tr>
        <th>Field Name</th>
        <th>Required</th>
        <th>Details</th>
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
