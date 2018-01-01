---
lang: de

table_data:
  - field_name: service_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The **service_id** contains an ID that uniquely identifies a set of dates when a service exception is available for one or more routes. Each (service_id, date) pair can only appear once in calendar_dates.txt. If the a service_id value appears in both the calendar.txt and calendar_dates.txt files, the information in calendar_dates.txt modifies the service information specified in [calendar.txt](#calendar). This field is referenced by the [trips.txt](#trips) file.
  - field_name: date
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          The **date** field specifies a particular date when service availability is different than the norm. You can use the **exception_type** field to indicate whether service is available on the specified date. The **date** field's value should be in YYYYMMDD format.
  - field_name: exception_type
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          The **exception_type** indicates whether service is available on the date specified in the date field.

          * A value of **1** indicates that service has been added for the specified date.
          * A value of **2** indicates that service has been removed for the specified date.

          For example, suppose a route has one set of trips available on holidays and another set of trips available on all other days. You could have one **service_id** that corresponds to the regular service schedule and another **service_id** that corresponds to the holiday schedule. For a particular holiday, you would use the calendar_dates.txt file to add the holiday to the holiday **service_id** and to remove the holiday from the regular **service_id** schedule.
---
File: **Optional**

The calendar_dates table allows you to explicitly activate or disable service IDs by date. You can use it in two ways.

* Recommended: Use calendar_dates.txt in conjunction with [calendar.txt](#calendar), where calendar_dates.txt defines any exceptions to the default service categories defined in the [calendar.txt](#calendar) file. If your service is generally regular, with a few changes on explicit dates (for example, to accommodate special event services, or a school schedule), this is a good approach.
* Alternate: Omit [calendar.txt](#calendar), and include ALL dates of service in calendar_dates.txt. If your schedule varies most days of the month, or you want to programmatically output service dates without specifying a normal weekly schedule, this approach may be preferable.

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
