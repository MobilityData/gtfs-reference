---
table_data:
  - field_name: service_id
    details:
      - ID: 1
        required: true
        tags: []
        text: The **service_id** contains an ID that uniquely identifies a set of dates when service is available for one or more routes. Each service_id value can appear at most once in a calendar.txt file. This value is dataset unique. It is referenced by the [trips.txt](#tripstxt) file.
  - field_name: monday
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The monday field contains a binary value that indicates whether the service is valid for all Mondays.

          * A value of **1** indicates that service is available for all Mondays in the date range. (The date range is specified using the **start_date** and **end_date** fields.)
          * A value of **0** indicates that service is not available on Mondays in the date range.

          **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file.
  - field_name: tuesday
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The tuesday field contains a binary value that indicates whether the service is valid for all Tuesdays.

          * A value of **1** indicates that service is available for all Tuesdays in the date range. (The date range is specified using the **start_date** and **end_date** fields.)
          * A value of **0** indicates that service is not available on Tuesdays in the date range.

          **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file.
  - field_name: wednesday
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The wednesday field contains a binary value that indicates whether the service is valid for all Wednesdays.

          * A value of **1** indicates that service is available for all Wednesdays in the date range. (The date range is specified using the **start_date** and **end_date** fields.)
          * A value of **0** indicates that service is not available on Wednesdays in the date range.

          **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file.
  - field_name: thursday
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The thursday field contains a binary value that indicates whether the service is valid for all Thursdays.

          * A value of **1** indicates that service is available for all Thursdays in the date range. (The date range is specified using the **start_date** and **end_date** fields.)
          * A value of **0** indicates that service is not available on Thursdays in the date range.

          **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file.
  - field_name: friday
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The friday field contains a binary value that indicates whether the service is valid for all Fridays.

          * A value of **1** indicates that service is available for all Fridays in the date range. (The date range is specified using the **start_date** and **end_date** fields.)
          * A value of **0** indicates that service is not available on Fridays in the date range.

          **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file.
  - field_name: saturday
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The saturday field contains a binary value that indicates whether the service is valid for all Saturdays.

          * A value of **1** indicates that service is available for all Saturdays in the date range. (The date range is specified using the **start_date** and **end_date** fields.)
          * A value of **0** indicates that service is not available on Saturdays in the date range.

          **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file.
  - field_name: sunday
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The sunday field contains a binary value that indicates whether the service is valid for all Sundays.

          * A value of **1** indicates that service is available for all Sundays in the date range. (The date range is specified using the **start_date** and **end_date** fields.)
          * A value of **0** indicates that service is not available on Sundays in the date range.

          **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file.
  - field_name: start_date
    details:
      - ID: 1
        required: true
        tags: []
        text: The **start_date** field contains the start date for the service. The **start_date** field's value should be in YYYYMMDD format.
  - field_name: end_date
    details:
      - ID: 1
        required: true
        tags: []
        text: The **end_date** field contains the end date for the service. This date is included in the service interval. The **end_date** field's value should be in YYYYMMDD format.
---
File: **Required**

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
      <td>{{ detail.text | markdownify }}{{ detail.example_table }}</td>
    </tr>
      {% endfor %}
    {% endfor %}
  </tbody>
</table>

|  Field Name | Required | Details |
|  ------ | ------ | ------ |
|  service_id | **Required** | The **service_id** contains an ID that uniquely identifies a set of dates when service is available for one or more routes. Each service_id value can appear at most once in a calendar.txt file. This value is dataset unique. It is referenced by the [trips.txt](#tripstxt) file. |
|  monday | **Required** | The monday field contains a binary value that indicates whether the service is valid for all Mondays. |
|   |  | * A value of **1** indicates that service is available for all Mondays in the date range. (The date range is specified using the **start_date** and **end_date** fields.) |
|   |  | * A value of **0** indicates that service is not available on Mondays in the date range. |
|   |  | **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file. |
|  tuesday | **Required** | The tuesday field contains a binary value that indicates whether the service is valid for all Tuesdays. |
|   |  | A value of **1** indicates that service is available for all Tuesdays in the date range. (The date range is specified using the **start_date** and **end_date** fields.) |
|   |  | A value of **0** indicates that service is not available on Tuesdays in the date range. |
|   |  | **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file. |
|  wednesday | **Required** | The wednesday field contains a binary value that indicates whether the service is valid for all Wednesdays. |
|   |  | A value of **1** indicates that service is available for all Wednesdays in the date range. (The date range is specified using the **start_date** and **end_date** fields.) |
|   |  | A value of **0** indicates that service is not available on Wednesdays in the date range. |
|   |  | **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file. |
|  thursday | **Required** | The thursday field contains a binary value that indicates whether the service is valid for all Thursdays. |
|   |  | A value of **1** indicates that service is available for all Thursdays in the date range. (The date range is specified using the **start_date** and **end_date** fields.) |
|   |  | A value of **0** indicates that service is not available on Thursdays in the date range. |
|   |  | **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file. |
|  friday | **Required** | The friday field contains a binary value that indicates whether the service is valid for all Fridays. |
|   |  | A value of **1** indicates that service is available for all Fridays in the date range. (The date range is specified using the **start_date** and **end_date** fields.) |
|   |  | A value of **0** indicates that service is not available on Fridays in the date range. |
|   |  | **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file |
|  saturday | **Required** | The saturday field contains a binary value that indicates whether the service is valid for all Saturdays. |
|   |  | A value of **1** indicates that service is available for all Saturdays in the date range. (The date range is specified using the **start_date** and **end_date** fields.) |
|   |  | A value of **0** indicates that service is not available on Saturdays in the date range. |
|   |  | **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file. |
|  sunday | **Required** | The sunday field contains a binary value that indicates whether the service is valid for all Sundays. |
|   |  | A value of **1** indicates that service is available for all Sundays in the date range. (The date range is specified using the **start_date** and **end_date** fields.) |
|   |  | A value of **0** indicates that service is not available on Sundays in the date range. |
|   |  | **Note:** You may list exceptions for particular dates, such as holidays, in the [calendar_dates.txt](#calendar_datestxt) file. |
|  start_date | **Required** | The **start_date** field contains the start date for the service.  The start_date field's value should be in YYYYMMDD format. |
|  end_date | **Required** | The **end_date** field contains the end date for the service. This date is included in the service interval.  The **end_date** field's value should be in YYYYMMDD format. |
