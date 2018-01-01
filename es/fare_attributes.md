---
lang: es

table_data:
  - field_name: fare_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The **fare_id** field contains an ID that uniquely identifies a fare class. The **fare_id** is dataset unique.
  - field_name: price
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          The **price** field contains the fare price, in the unit specified by **currency_type**.
  - field_name: currency_type
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          The **currency_type** field defines the currency used to pay the fare. Please use the ISO 4217 alphabetical currency codes which can be found [here](http://en.wikipedia.org/wiki/ISO_4217).
  - field_name: payment_method
    details:
      - ID: 4
        required: true
        tags: []
        text: |
          The **payment_method** field indicates when the fare must be paid. Valid values for this field are:

          * **0** - Fare is paid on board.
          * **1** - Fare must be paid before boarding.
  - field_name: transfers
    details:
      - ID: 5
        required: true
        tags: []
        text: |
          The transfers field specifies the number of transfers permitted on this fare. Valid values for this field are:

          * **0** - No transfers permitted on this fare.
          * **1** - Passenger may transfer once.
          * **2** - Passenger may transfer twice.
          * **(empty)** - If this field is empty, unlimited transfers are permit.
  - field_name: agency_id
    details:
      - ID: 6
        required: false
        tags: []
        text: |
          Required for feeds with multiple agencies defined in the agency.txt file. Each fare attribute must specify an agency_id value to indicate which agency the fare applies to.
  - field_name: transfer_duration
    details:
      - ID: 7
        required: false
        tags: []
        text: |
          The **transfer_duration** field specifies the length of time in seconds before a transfer expires.  When used with a **transfers** value of 0, the **transfer_duration** field indicates how long a ticket is valid for a fare where no transfers are allowed. Unless you intend to use this field to indicate ticket validity, **transfer_duration** should be omitted or empty when **transfers** is set to 0.
---
File: **Optional**

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