# gtfs-reference

# Editing GTFS Core Reference

The Core Reference data are written in YAML variables. More information about YAML syntax and structure may be found [here](https://learnxinyminutes.com/docs/yaml/). Each variable is defined as follows:

* `field_name`: The name of the GTFS field being described.
* `details`: An array of the details for each field_name.
  * `ID`: A unique identifying integer of the corresponding field reference.
  * `required`: A boolean variable stating whether the field in question is required or optional.
  * `tags`: An array of System Tags used to denote that the field reference will assist with the described task. Values include 'human-readability', 'trip-planners', 'timetables', and 'accessibility'.
  * `text`: The text of the field reference. This variable should begin with a vertical bar ( | ) followed by an indented newline. This will preserve any equally indented newlines in the text. Simple Markdown is allowed and any HTML should be avoided.
  * `example_table`: An optional variable, this allows for example tables (or any other HTML entity) to be placed immediately after the field reference text. This variable should begin with a vertical bar ( | ) followed by an indented newline. This will preserve any equally indented newlines in the text. Markdown will not function in this variable and should be exclusively used for HTML elements.

Elements of the Core Reference not in a table may be found below the YAML front matter and should be written in Markdown.