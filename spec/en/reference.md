## GTFS-ride

**Initial draft January 12, 2017. See [Revision History](../../CHANGES.md) for more details.**

This document explains the types of files that comprise a GTFS-ride dataset and defines the fields used in all of those files. The bolded files are those unique to GTFS-ride. They are not included in standard GTFS.

## Table of Contents

1.  [Term Definitions](#term-definitions)
2.  [Feed Files](#feed-files)
3.  [File Requirements](#file-requirements)
4.  [Field Definitions](#field-definitions)
    -   [*__board\_alight.txt__*](#board_alighttxt)
    -   [*__rider\_trip.txt__*](#rider_infotxt)
    -   [*__ridership.txt__*](#ridershiptxt)

## Term Definitions
_Retrieved from GTFS [https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md)_
>This section defines terms that are used throughout this document.
>
>* **Field required** - The field column must be included in your feed, and a value must be provided for each record. Some required fields permit an empty string as a value. To enter an empty string, just omit any text between the commas for that field. Note that 0 is interpreted as "a string of value 0", and is not an empty string. Please see the field definition for details.
>* **Field optional** - The field column may be omitted from your feed. If you choose to include an optional column, each record in your feed must have a value for that column. You may include an empty string as a value for records that do not have values for the column. Some optional fields permit an empty string as a value. To enter an empty string, just omit any text between the commas for that field. Note that 0 is interpreted as "a string of value 0", and is not an empty string.
>* **Dataset unique** - The field contains a value that maps to a single distinct entity within the column. For example, if a route is assigned the ID **1A**, then no other route may use that route ID. However, you may assign the ID **1A** to a location because locations are a different type of entity than routes.

## Feed Files

This specification includes the following files along with their associated content. **Bolded** files are unique to GTFS-ride, while the rest reference GTFS files. More information on the GTFS files may be found at [https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md).

|  Filename | Required | Defines |
|  ------ | ------ | ------ |
|  [agency.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#agencytxt) | **Required** | One or more transit agencies that provide the data in this feed. |
|  [stops.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#stopstxt) | **Required** | Individual locations where vehicles pick up or drop off passengers. |
|  [routes.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#routestxt) | **Required** | Transit routes. A route is a group of trips that are displayed to riders as a single service. |
|  [trips.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#tripstxt)  | **Required** | Trips for each route. A trip is a sequence of two or more stops that occurs at a specific time. |
|  [stop_times.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#stop_timestxt)  | **Required** | Times that a vehicle arrives at and departs from individual stops for each trip. |
|  [calendar.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#calendartxt)  | **Required** | Dates for service IDs using a weekly schedule. Specify when service starts and ends, as well as days of the week where service is available. |
|  [feed_info.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#feed_infotxt)  | Optional | Additional information about the feed itself, including publisher, version, and expiration information. |
|  [*__board_alight.txt__*](#board_alighttxt) | Optional | Tracks boardings/alightings along with associated information at stop-level. |
|  [*__rider_trip.txt__*](#rider_triptxt) | Optional | Includes anonymized data about specific riders' trip. |
|  [*__ridership.txt__*](#ridershiptxt) | Optional | Route or Trip level counts of ridership. |

## File Requirements
_Retrieved from GTFS [https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md)_

>The following requirements apply to the format and contents of your files:

>* All files in a General Transit Feed Spec (GTFS) feed must be saved as comma-delimited text.
>* The first line of each file must contain field names. Each subsection of the [Field Definitions](#Field-Definitions) section corresponds to one of the files in a transit feed and lists the field names you may use in that file.
>* All field names are case-sensitive.
>* Field values may not contain tabs, carriage returns or new lines.
>* Field values that contain quotation marks or commas must be enclosed within quotation marks. In addition, each quotation mark in the field value must be preceded with a quotation mark. This is consistent with the manner in which Microsoft Excel outputs comma-delimited (CSV) files. For more information on the CSV file format, see http://tools.ietf.org/html/rfc4180.
>The following example demonstrates how a field value would appear in a comma-delimited file:
  * **Original field value:** `Contains "quotes", commas and text`
  * **Field value in CSV file:** `"Contains ""quotes"", commas and text"`
>* Field values must not contain HTML tags, comments or escape sequences.
>* Remove any extra spaces between fields or field names. Many parsers consider the spaces to be part of the value, which may cause errors.
>* Each line must end with a CRLF or LF linebreak character.
>* Files should be encoded in UTF-8 to support all Unicode characters. Files that include the Unicode byte-order mark (BOM) character are acceptable. Please see the [Unicode FAQ](http://unicode.org/faq/utf_bom.html#BOM) for more information on the BOM character and UTF-8.
>* Zip the files in your feed.

## Field Definitions

_Only files unique to GTFS-ride are defined below. Definitions for all other files may be found at [https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md)_

### *__board_alight.txt__*

File: **Optional**

If an agency collects disaggregate, stop-level ridership data, board_alight.txt may be used to record ridership boarding counts and additional supplementary data. If only more aggregate ridership data is collected, the agency should use ridership.txt to record ridership counts.  It should be noted that unique combinations of stop_id and trip_id will not uniquely define a specific instance in time of arrival and boardings at a stop. Boardings and other counts will be aggregated across dates active as defined by a trip’s service_id. By including an optional timestamp an agency can disaggregate counts to specifics instances of stop arrivals and boardings, and provide a calculated current load.

|  Field Name | Required | Details |
|  ------ | ------ | ------ |
| stop_id | **Required** | The **stop_id** contains an ID that uniquely identifies a stop. |
| trip_id | **Required** | The **trip_id** contains an ID that uniquely identifies a trip. |
| boardings | **Required** | The **boardings** field contains the number of boardings as collected by either automated or manual methods. |
| alightings | Optional | The **alightings** field contains the number of alightings as collected by either automated or manual methods. Less common than boarding data, this field is optional. |
| bike_boardings | Optional | The **bike_boardings** field contains the number of bike boardings at the identified stop and trip. |
| bike_alightings | Optional | The **bike_alightings** field contains the number of bike alightings at the identified stop and trip. |
| wheelchair_boardings | Optional | The **wheelchair_boardings** field contains the number of wheelchair boardings at the identified stop and trip. |
| wheelchair_alightings | Optional | The **wheelchair_alightings** field contains the number of wheelchair alightings at the identified stop and trip. |
| timestamp | Optional | The **timestamp** field contains the time in POSIX time (i.e., number of seconds since January 1st 1970 00:00:00 UTC) of the associated data. |
| current_load | Optional | The **current_load** field contains a calculated vehicle load at the time indicated in the **timestamp** field. |
| source | Optional | The **source** field contains the collection method of the associated data. |
|   |  | * **0** - Manual.  |
|   |  | * **1** - APC.  |
|   |  | * **2** - AFC.  |
|   |  | * **3** - Model estimation.  |

### *__rider_trip.txt__*

File: **Optional**

If an agency has the ability to associate supplementary ridership data with a specific rider, rider_trip.txt may be used to record the rider-generated details. Care should be exercised in the creation of the rider_id field to sufficiently anonymize a rider’s identity. The rider_trip.txt file may be useful for origin/destination, rider demographic, fare structure, network configuration, transit equity, demand forecasting, and performance review studies. 

|  Field Name | Required | Details |
|  ------ | ------ | ------ |
| rider_id | **Required** | The **rider_id** field contains the ID of a unique rider. The **rider_id** is dataset unique. |
| trip_id | **Required** | The **trip_id** field contains the ID of the trip associated with the unique rider |
| boarding_stop_id | Optional | The **boarding_stop_id** field contains the ID of the boarding stop associated with the unique rider. |
| alighting_stop_id | Optional | The **alighting_stop_id** field contains the ID of the alighting stop associated with the unique rider. |
| boarding_time | Optional | The **boarding_time** field contains the time of the boarding associated with the unique rider. |
| alighting_time | Optional | The **alighting_time** field contains the time of the alighting associated with the unique rider. |
| rider_type | Optional | The **rider_type** field contains information on the rider type of the unique rider. |
|   |  | * **0** - No special rider type.  |
|   |  | * **1** - Senior.  |
|   |  | * **2** - Child.  |
|   |  | * **3** - Student.  |
|   |  | * **4** - Youth.  |
|   |  | * **5** - Disabled.  |
|   |  | * **6** - Promotional category.  |
|   |  | * **7** - Military.  |
|   |  | * **8-11** - Custom categories.  |
| rider_type_description | Optional | The **rider_type_description** field contains specific descriptions of the employed rider types. |
| fare_paid | Optional | The **fare_paid** field contains the amount of the fare paid by the unique rider. |
| fare_method | Optional | The **fare_method** field contains the method of payment used to collect the fare. |
|   |  | * **0** - Cash.  |
|   |  | * **1** - Paper transfer.  |
|   |  | * **2** - Paper pass.  |
|   |  | * **3** - AFC.  |
| accompanying_device | Optional | The **accompanying_device** field contains information on any accompanying mobility or medical devices of the unique rider. |
|   |  | * **0** - No accompanying mobility devices.  |
|   |  | * **1** - Accompanying bike.  |
|   |  | * **2** - Accompanying wheelchair.  |
|   |  | * **3** - Accompanying medical device.  |
|   |  | * **4** - Other accompanying device.  |
| transfer_status | Optional | The **transfer_status** field contains the transfer status of the unique rider. |
|   |  | * 0 - rider is not a transfer |
|   |  | * 1 - rider is a transfer |

### *__ridership.txt__*

File: **Optional**

An agency may use the ridership.txt file to record aggregate level ridership counts depending on agency capabilities and requirements. If no Route ID or Trip ID is specified, count is system wide. If stop-level ridership counts are available they should be recorded in board_alight.txt, but an agency may choose to also record the aggregated counts in ridership.txt to aid in meeting specific reporting requirements or in generating user-defined reports.  

|  Field Name | Required | Details |
|  ------ | ------ | ------ |
| count | **Required** | The **count** field contains the count desired for the selected segment of ridership count. |
| period_start | **Required** | The **period_start** field contains the start in POSIX time (i.e., number of seconds since January 1st 1970 00:00:00 UTC) of time period of time represented. |
| period_end | **Required** | The **period_end** field contains the start in POSIX time (i.e., number of seconds since January 1st 1970 00:00:00 UTC) of time period of time represented. |
| route_id | Optional | The **route_id** field contains an ID that uniquely identifies a route. This value is referenced from the [routes.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#routestxt) file. |
| trip_id | Optional | The **trip_id** field contains an ID that uniquely identifies a trip. This value is referenced from the [trips.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#tripstxt) file. |
