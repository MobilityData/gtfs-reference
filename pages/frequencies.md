---
table_data:
  - field_name: trip_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The **trip_id** contains an ID that identifies a trip on which the specified frequency of service applies. Trip IDs are referenced from the [trips.txt](#tripstxt) file.
  - field_name: start_time
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          The **start_time** field specifies the time at which the first vehicle departs from the first stop of the trip with the specified frequency. The time is measured from "noon minus 12h" (effectively midnight, except for days on which daylight savings time changes occur) at the beginning of the service day. For times occurring after midnight, enter the time as a value greater than 24:00:00 in HH:MM:SS local time for the day on which the trip schedule begins. E.g. 25:35:00.
  - field_name: end_time
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          The **end_time** field indicates the time at which service changes to a different frequency (or ceases) at the first stop in the trip. The time is measured from "noon minus 12h" (effectively midnight, except for days on which daylight savings time changes occur) at the beginning of the service day. For times occurring after midnight, enter the time as a value greater than 24:00:00 in HH:MM:SS local time for the day on which the trip schedule begins. E.g. 25:35:00.
  - field_name: headway_secs
    details:
      - ID: 4
        required: true
        tags: []
        text: |
          The **headway_secs** field indicates the time between departures from the same stop (headway) for this trip type, during the time interval specified by **start_time** and **end_time**. The headway value must be entered in seconds.

          Periods in which headways are defined (the rows in frequencies.txt) shouldn't overlap for the same trip, since it's hard to determine what should be inferred from two overlapping headways. However, a headway period may begin at the exact same time that another one ends, for instance:

          | `A, 05:00:00, 07:00:00, 600` |
          | `B, 07:00:00, 12:00:00, 1200` |
  - field_name: exact_times
    details:
      - ID: 5
        required: false
        tags: []
        text: |
          The **exact_times** field determines if frequency-based trips should be exactly scheduled based on the specified headway information. Valid values for this field are:

          * **0** or **(empty)** - Frequency-based trips are not exactly scheduled. This is the default behavior.
          * **1** - Frequency-based trips are exactly scheduled. For a frequencies.txt row, trips are scheduled starting with trip_start_time = start_time + x * headway_secs for all x in (0, 1, 2, ...) where trip_start_time < end_time.

          The value of **exact_times** must be the same for all frequencies.txt rows with the same **trip_id**. If **exact_times** is 1 and a frequencies.txt row has a **start_time** equal to **end_time**, no trip must be scheduled. When **exact_times** is 1, care must be taken to choose an **end_time** value that is greater than the last desired trip start time but less than the last desired trip start time + **headway_secs**.
---
File: **Optional**

This table is intended to represent schedules that don't have a fixed list of stop times. When trips are defined in frequencies.txt, the trip planner ignores the absolute values of the **arrival_time** and **departure_time** fields for those trips in [stop_times.txt](#stop_timestxt). Instead, the **stop_times** table defines the sequence of stops and the time difference between each stop.

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
