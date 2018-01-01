---
lang: es

table_data:
  - field_name: stop_id
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The **stop_id** field contains an ID that uniquely identifies a stop, station, or station entrance. Multiple routes may use the same stop. The **stop_id** is used by systems as an internal identifier of this record (e.g., primary key in database), and therefore the **stop_id** must be dataset unique.
  - field_name: stop_code
    details:
      - ID: 2
        required: false
        tags: []
        text: |
          The **stop_code** field contains short text or a number that uniquely identifies the stop for passengers. Stop codes are often used in phone-based transit information systems or printed on stop signage to make it easier for riders to get a stop schedule or real-time arrival information for a particular stop.  The **stop_code** field contains short text or a number that uniquely identifies the stop for passengers. The **stop_code** can be the same as **stop_id** if it is passenger-facing. This field should be left blank for stops without a code presented to passengers.
  - field_name: stop_name
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          The **stop_name** field contains the name of a stop, station, or station entrance. Please use a name that people will understand in the local and tourist vernacular.
  - field_name: stop_desc
    details:
      - ID: 4
        required: false
        tags: []
        text: |
          The **stop_desc** field contains a description of a stop. Please provide useful, quality information. Do not simply duplicate the name of the stop.
  - field_name: stop_lat
    details:
      - ID: 5
        required: true
        tags: []
        text: |
          The **stop_lat** field contains the latitude of a stop, station, or station entrance. The field value must be a valid WGS 84 latitude.
  - field_name: stop_lon
    details:
      - ID: 6
        required: true
        tags: []
        text: |
          The **stop_lon** field contains the longitude of a stop, station, or station entrance. The field value must be a valid WGS 84 longitude value from -180 to 180.
  - field_name: zone_id
    details:
      - ID: 7
        required: false
        tags: []
        text: |
          The **zone_id** field defines the fare zone for a stop ID. Zone IDs are required if you want to provide fare information using [fare_rules.txt](#fare_rules). If this stop ID represents a station, the zone ID is ignored.
  - field_name: stop_url
    details:
      - ID: 8
        required: false
        tags: []
        text: |
          The **stop_url** field contains the URL of a web page about a particular stop. This should be different from the agency_url and the route_url fields.  The value must be a fully qualified URL that includes **http**:// or **https**://, and any special characters in the URL must be correctly escaped. See http://www.w3.org/Addressing/URL/4_URI_Recommentations.html for a description of how to create fully qualified URL values.
  - field_name: location_type
    details:
      - ID: 9
        required: false
        tags: []
        text: |
          The **location_type** field identifies whether this stop ID represents a stop, station, or station entrance. If no location type is specified, or the location_type is blank, stop IDs are treated as stops. Stations may have different properties from stops when they are represented on a map or used in trip planning.  The location type field can have the following values:

          * **0** or blank - Stop. A location where passengers board or disembark from a transit vehicle.
          * **1** - Station. A physical structure or area that contains one or more stop.
          * **2** - Station Entrance/Exit. A location where passengers can enter or exit a station from the street. The stop entry must also specify a parent_station value referencing the stop ID of the parent station for the entrance.
  - field_name: parent_station
    details:
      - ID: 10
        required: false
        tags: []
        text: |
          For stops that are physically located inside stations, the **parent_station** field identifies the station associated with the stop. To use this field, stops.txt must also contain a row where this stop ID is assigned location type=1.
        example_table: |
          <table>
            <thead>
              <tr>
                <th>This stop ID represents...</th>
                <th>This entry's location type...</th>
                <th>This entry's parent_station field contains...</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>A stop located inside a station</td>
                <td>0 or blank</td>
                <td>The stop ID of the station where this stop is located. The stop referenced by parent_station must have location_type=1.</td>
              </tr>
              <tr>
                <td>A stop located outside a station</td>
                <td>0 or blank</td>
                <td>A blank value. The parent_station field doesn’t apply to this stop.</td>
              </tr>
              <tr>
                <td>A station</td>
                <td>1</td>
                <td>A blank value. Stations can’t contain other stations.</td>
              </tr>
            </tbody>
          </table>
  - field_name: stop_timezone
    details:
      - ID: 11
        required: false
        tags: []
        text: |
          The **stop_timezone** field contains the timezone in which this stop, station, or station entrance is located. Please refer to [Wikipedia List of Timezones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) for a list of valid values. If omitted, the stop should be assumed to be located in the timezone specified by **agency_timezone** in [agency.txt](#agency).   When a stop has a parent station, the stop is considered to be in the timezone specified by the parent station's **stop_timezone** value. If the parent has no stop_timezone value, the stops that belong to that station are assumed to be in the timezone specified by **agency_timezone**, even if the stops have their own **stop_timezone** values. In other words, if a given stop has a **parent_station** value, any **stop_timezone** value specified for that stop must be ignored.  Even if **stop_timezone** values are provided in stops.txt, the times in [stop_times.txt](#stop_times) should continue to be specified as time since midnight in the timezone specified by **agency_timezone** in agency.txt. This ensures that the time values in a trip always increase over the course of a trip, regardless of which timezones the trip crosses.
  - field_name: wheelchair_boarding
    details:
      - ID: 12
        required: false
        tags: []
        text: |
          The **wheelchair_boarding field** identifies whether wheelchair boardings are possible from the specified stop, station, or station entrance. The field can have the following values:

          * **0** (or empty) - indicates that there is no accessibility information for the stop
          * **1** - indicates that at least some vehicles at this stop can be boarded by a rider in a wheelchair
          * **2** - wheelchair boarding is not possible at this stop

          When a stop is part of a larger station complex, as indicated by a stop with a **parent_station** value, the stop's **wheelchair_boarding** field has the following additional semantics:

          * **0** (or empty) - the stop will inherit its **wheelchair_boarding** value from the parent station, if specified in the parent
          * **1** - there exists some accessible path from outside the station to the specific stop / platform
          * **2** - there exists no accessible path from outside the station to the specific stop / platform

          For station entrances, the **wheelchair_boarding** field has the following additional semantics:

          * **0** (or empty) - the station entrance will inherit its **wheelchair_boarding** value from the parent station, if specified in the parent
          * **1** - the station entrance is wheelchair accessible (e.g. an elevator is available to platforms if they are not at-grade)
          * **2** - there exists no accessible path from the entrance to station platforms
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