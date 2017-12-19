---
table_data:
  - field_name: route_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The **route_id** field contains an ID that uniquely identifies a route. This value is referenced from the [routes.txt](#routes) file.
  - field_name: service_id
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          The **service_id** contains an ID that uniquely identifies a set of dates when service is available for one or more routes. This value is referenced from the [calendar.txt](#calendar) or [calendar_dates.txt](#calendar_dates) file.
  - field_name: trip_id
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          The **trip_id** field contains an ID that identifies a trip. The **trip_id** is dataset unique.
  - field_name: trip_headsign
    details:
      - ID: 4
        required: false
        tags: []
        text: |
          The **trip_headsign** field contains the text that appears on a sign that identifies the trip's destination to passengers. Use this field to distinguish between different patterns of service in the same route. If the headsign changes during a trip, you can override the **trip_headsign** by specifying values for the **stop_headsign** field in [stop_times.txt](#stop_times).
  - field_name: trip_short_name
    details:
      - ID: 5
        required: false
        tags: []
        text: |
          The **trip_short_name** field contains the text that appears in schedules and sign boards to identify the trip to passengers, for example, to identify train numbers for commuter rail trips. If riders do not commonly rely on trip names, please leave this field blank.  A **trip_short_name** value, if provided, should uniquely identify a trip within a service day; it should not be used for destination names or limited/express designations.
  - field_name: direction_id
    details:
      - ID: 6
        required: false
        tags: []
        text: |
          The **direction_id** field contains a binary value that indicates the direction of travel for a trip. Use this field to distinguish between bi-directional trips with the same **route_id**. This field is not used in routing; it provides a way to separate trips by direction when publishing time tables. You can specify names for each direction with the **trip_headsign** field.

          * 0 - travel in one direction (e.g. outbound travel)
          * 1 - travel in the opposite direction (e.g. inbound travel)

          For example, you could use the *trip_headsign* and *direction_id* fields together to assign a name to travel in each direction for a set of trips. A [trips.txt](#trips) file could contain these rows for use in time tables:

          * `trip_id,...,trip_headsign,direction_id`
          * `1234,...,Airport,0`
          * `1505,...,Downtown,1`
  - field_name: block_id
    details:
      - ID: 7
        required: false
        tags: []
        text: |
          The **block_id** field identifies the block to which the trip belongs. A block consists of a single trip or many sequential trips made using the same vehicle, defined by shared service day and block_id. A block_id can have trips with different service days, making distinct blocks. (See [example below](#example-showing-blocks-and-service-day))
  - field_name: shape_id
    details:
      - ID: 8
        required: false
        tags: []
        text: |
          The **shape_id** field contains an ID that defines a shape for the trip. This value is referenced from the [shapes.txt](#shapes) file. The shapes.txt file allows you to define how a line should be drawn on the map to represent a trip.
  - field_name: wheelchair_accessible
    details:
      - ID: 9
        required: false
        tags: []
        text: |
          * **0** (or empty) - indicates that there is no accessibility information for the trip
          * **1** - indicates that the vehicle being used on this particular trip can accommodate at least one rider in a wheelchair
          * **2** - indicates that no riders in wheelchairs can be accommodated on this trip
  - field_name: bikes_allowed
    details:
      - ID: 10
        required: false
        tags: []
        text: |
          * 0 (or empty) - indicates that there is no bike information for the trip
          * **1** - indicates that the vehicle being used on this particular trip can accommodate at least one bicycle
          * **2** - indicates that no bicycles are allowed on this trip
---
File: **Required**

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

#### Example showing blocks and service day

The example below is valid, with distinct blocks every day of the week.

| route_id | trip_id | service_id                     | block_id | <span style="font-weight:normal">*(first stop time)*</span> | <span style="font-weight:normal">*(last stop time)*</span> |
|----------|---------|--------------------------------|----------|-----------------------------------------|-------------------------|
| red      | trip_1  | mon-tues-wed-thurs-fri-sat-sun | red_loop | 22:00:00                                | 22:55:00                |
| red      | trip_2  | fri-sat-sun                    | red_loop | 23:00:00                                | 23:55:00                |
| red      | trip_3  | fri-sat                        | red_loop | 24:00:00                                | 24:55:00                |
| red      | trip_4  | mon-tues-wed-thurs             | red_loop | 20:00:00                                | 20:50:00                |
| red      | trip_5  | mon-tues-wed-thurs             | red_loop | 21:00:00                                | 21:50:00                |

Notes on above table:
* On Friday into Saturday morning, for example, a single vehicle operates trip_1, trip_2, and trip_3 (10:00 PM through 12:55 AM). Note that the last trip occurs on Saturday, 12:00 AM to 12:55 AM, but is part of the Friday “service day” because the times are 24:00:00 to 24:55:00.
* On Monday, Tuesday, Wednesday, and Thursday, a single vehicle operates trip_1, trip_4, and trip_5 in a block from 8:00 PM to 10:55 PM.
