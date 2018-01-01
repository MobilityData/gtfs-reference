---
lang: de

table_data:
  - field_name: feed_publisher_name
    details:
      - ID: 1
        required: true
        tags: []
        text: |
          The **feed_publisher_name** field contains the full name of the organization that publishes the feed. (This may be the same as one of the **agency_name** values in [agency.txt](#agency).) GTFS-consuming applications can display this name when giving attribution for a particular feed's data.
  - field_name: feed_publisher_url
    details:
      - ID: 2
        required: true
        tags: []
        text: |
          The **feed_publisher_url** field contains the URL of the feed publishing organization's website. (This may be the same as one of the **agency_url** values in [agency.txt](#agency).) The value must be a fully qualified URL that includes **http**:// or **https**://, and any special characters in the URL must be correctly escaped. See http://www.w3.org/Addressing/URL/4_URI_Recommentations.html for a description of how to create fully qualified URL values.
  - field_name: feed_lang
    details:
      - ID: 3
        required: true
        tags: []
        text: |
          The **feed_lang** field contains a IETF BCP 47 language code specifying the default language used for the text in this feed. This setting helps GTFS consumers choose capitalization rules and other language-specific settings for the feed. For an introduction to IETF BCP 47, please refer to http://www.rfc-editor.org/rfc/bcp/bcp47.txt and http://www.w3.org/International/articles/language-tags/.
  - field_name: feed_start_date
    details:
      - ID: 4
        required: false
        tags: []
        text: |
          The feed provides complete and reliable schedule information for service in the period from the beginning of the **feed_start_date** day to the end of the **feed_end_date** day. Both days are given as dates in YYYYMMDD format as for [calendar.txt](#calendar), or left empty if unavailable. The **feed_end_date** date must not precede the **feed_start_date** date if both are given. Feed providers are encouraged to give schedule data outside this period to advise of likely future service, but feed consumers should treat it mindful of its non-authoritative status. If **feed_start_date** or **feed_end_date** extend beyond the active calendar dates defined in [calendar.txt](#calendar) and [calendar_dates.txt](#calendar_dates), the feed is making an explicit assertion that there is no service for dates within the **feed_start_date** or **feed_end_date** range but not included in the active calendar dates.
  - field_name: feed_end_date
    details:
      - ID: 5
        required: false
        tags: []
        text: |
          (see above)
  - field_name: feed_version
    details:
      - ID: 6
        required: false
        tags: []
        text: |
          The feed publisher can specify a string here that indicates the current version of their GTFS feed. GTFS-consuming applications can display this value to help feed publishers determine whether the latest version of their feed has been incorporated.
---
File: **Optional**

The file contains information about the feed itself, rather than the services that the feed describes. GTFS currently has an [agency.txt](#agency) file to provide information about the agencies that operate the services described by the feed. However, the publisher of the feed is sometimes a different entity than any of the agencies (in the case of regional aggregators). In addition, there are some fields that are really feed-wide settings, rather than agency-wide.

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
