---
---
## General Transit Feed Specification Reference

**Revised August 4, 2016. See [Revision History](https://github.com/google/transit/blob/master/gtfs/CHANGES.md) for more details.**

This document explains the types of files that comprise a GTFS transit feed and defines the fields used in all of those files.

## Term Definitions

This section defines terms that are used throughout this document.

* **Field required** - The field column must be included in your feed, and a value must be provided for each record. Some required fields permit an empty string as a value. To enter an empty string, just omit any text between the commas for that field. Note that 0 is interpreted as "a string of value 0", and is not an empty string. Please see the field definition for details.
* **Field optional** - The field column may be omitted from your feed. If you choose to include an optional column, each record in your feed must have a value for that column. You may include an empty string as a value for records that do not have values for the column. Some optional fields permit an empty string as a value. To enter an empty string, just omit any text between the commas for that field. Note that 0 is interpreted as "a string of value 0", and is not an empty string.
* **Dataset unique** - The field contains a value that maps to a single distinct entity within the column. For example, if a route is assigned the ID **1A**, then no other route may use that route ID. However, you may assign the ID **1A** to a location because locations are a different type of entity than routes.

## Feed Files

This specification defines the following files along with their associated content:

|  Filename | Required | Defines |
|  ------ | ------ | ------ |
|  [agency.txt](#agencytxt) | **Required** | One or more transit agencies that provide the data in this feed. |
|  [stops.txt](#stopstxt) | **Required** | Individual locations where vehicles pick up or drop off passengers. |
|  [routes.txt](#routestxt) | **Required** | Transit routes. A route is a group of trips that are displayed to riders as a single service. |
|  [trips.txt](#tripstxt)  | **Required** | Trips for each route. A trip is a sequence of two or more stops that occurs at specific time. |
|  [stop_times.txt](#stop_timestxt)  | **Required** | Times that a vehicle arrives at and departs from individual stops for each trip. |
|  [calendar.txt](#calendartxt)  | **Required** | Dates for service IDs using a weekly schedule. Specify when service starts and ends, as well as days of the week where service is available. |
|  [calendar_dates.txt](#calendar_datestxt)  | Optional | Exceptions for the service IDs defined in the [calendar.txt](#calendartxt) file. If [calendar.txt](#calendartxt) includes ALL dates of service, this file may be specified instead of [calendar.txt](#calendartxt). |
|  [fare_attributes.txt](#fare_attributestxt)  | Optional | Fare information for a transit organization's routes. |
|  [fare_rules.txt](#fare_rulestxt)  | Optional | Rules for applying fare information for a transit organization's routes. |
|  [shapes.txt](#shapestxt)  | Optional | Rules for drawing lines on a map to represent a transit organization's routes. |
|  [frequencies.txt](#frequenciestxt)  | Optional | Headway (time between trips) for routes with variable frequency of service. |
|  [transfers.txt](#transferstxt)  | Optional | Rules for making connections at transfer points between routes. |
|  [feed_info.txt](#feed_infotxt)  | Optional | Additional information about the feed itself, including publisher, version, and expiration information. |

## File Requirements

The following requirements apply to the format and contents of your files:

* All files in a General Transit Feed Spec (GTFS) feed must be saved as comma-delimited text.
* The first line of each file must contain field names. Each subsection of the [Field Definitions](#Field-Definitions) section corresponds to one of the files in a transit feed and lists the field names you may use in that file.
* All field names are case-sensitive.
* Field values may not contain tabs, carriage returns or new lines.
* Field values that contain quotation marks or commas must be enclosed within quotation marks. In addition, each quotation mark in the field value must be preceded with a quotation mark. This is consistent with the manner in which Microsoft Excel outputs comma-delimited (CSV) files. For more information on the CSV file format, see http://tools.ietf.org/html/rfc4180.
The following example demonstrates how a field value would appear in a comma-delimited file:
  * **Original field value:** `Contains "quotes", commas and text`
  * **Field value in CSV file:** `"Contains ""quotes"", commas and text"`
* Field values must not contain HTML tags, comments or escape sequences.
* Remove any extra spaces between fields or field names. Many parsers consider the spaces to be part of the value, which may cause errors.
* Each line must end with a CRLF or LF linebreak character.
* Files should be encoded in UTF-8 to support all Unicode characters. Files that include the Unicode byte-order mark (BOM) character are acceptable. Please see the [Unicode FAQ](http://unicode.org/faq/utf_bom.html#BOM) for more information on the BOM character and UTF-8.
* Zip the files in your feed.