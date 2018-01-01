---
lang: fr

table_data:
  - field_name: from_stop_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The **from_stop_id** field contains a stop ID that identifies a stop or station where a connection between routes begins. Stop IDs are referenced from the [stops.txt](#stops) file. If the stop ID refers to a station that contains multiple stops, this transfer rule applies to all stops in that station.
  - field_name: to_stop_id
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          The **to_stop_id** field contains a stop ID that identifies a stop or station where a connection between routes ends. Stop IDs are referenced from the [stops.txt](#stops) file. If the stop ID refers to a station that contains multiple stops, this transfer rule applies to all stops in that station.
  - field_name: transfer_type
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          The **transfer_type** field specifies the type of connection for the specified (from_stop_id, to_stop_id) pair. Valid values for this field are:

          * **0** or **(empty)** - This is a recommended transfer point between routes.
          * **1** - This is a timed transfer point between two routes. The departing vehicle is expected to wait for the arriving one, with sufficient time for a passenger to transfer between routes.
          * **2** - This transfer requires a minimum amount of time between arrival and departure to ensure a connection. The time required to transfer is specified by **min_transfer_time**.
          * **3** - Transfers are not possible between routes at this location.
  - field_name: min_transfer_time
    details:
      - ID: 4
        required: false
        tags: []
        text: |
          When a connection between routes requires an amount of time between arrival and departure (transfer_type=2), the **min_transfer_time** field defines the amount of time that must be available in an itinerary to permit a transfer between routes at these stops. The min_transfer_time must be sufficient to permit a typical rider to move between the two stops, including buffer time to allow for schedule variance on each route.

          The min_transfer_time value must be entered in seconds, and must be a non-negative integer.
---
File: **Optional**

Trip planners normally calculate transfer points based on the relative proximity of stops in each route. For potentially ambiguous stop pairs, or transfers where you want to specify a particular choice, use transfers.txt to define additional rules for making connections between routes.

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
