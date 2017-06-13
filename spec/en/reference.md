## GTFS-ride

**Initial draft pending. See [Revision History](../../CHANGES.md) for more details.**

This document explains the types of files that comprise a GTFS-ride dataset and defines the fields used in all of those files. The bolded files are those unique to GTFS-ride. They are not included in standard GTFS.

## Table of Contents

1.  [Term Definitions](#term-definitions)
2.  [Feed Files](#feed-files)
3.  [File Requirements](#file-requirements)
4.  [Field Definitions](#field-definitions)
    -   [*__board\_alight.txt__*](#board_alighttxt)
    -   [*__rider\_trip.txt__*](#rider_triptxt)
    -   [*__ridership.txt__*](#ridershiptxt)
    -   [*__ride\_feed\_info.txt__*](#ride_feed_infotxt)

## Term Definitions
_Retrieved from GTFS [https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md)_
>This section defines terms that are used throughout this document.
>
>* **Field required** - The field column must be included in your feed, and a value must be provided for each record. Some required fields permit an empty string as a value. To enter an empty string, just omit any text between the commas for that field. Note that 0 is interpreted as "a string of value 0", and is not an empty string. Please see the field definition for details.
>* **Field optional** - The field column may be omitted from your feed. If you choose to include an optional column, each record in your feed must have a value for that column. You may include an empty string as a value for records that do not have values for the column. Some optional fields permit an empty string as a value. To enter an empty string, just omit any text between the commas for that field. Note that 0 is interpreted as "a string of value 0", and is not an empty string.
>* **Dataset unique** - The field contains a value that maps to a single distinct entity within the column. For example, if a route is assigned the ID **1A**, then no other route may use that route ID. However, you may assign the ID **1A** to a location because locations are a different type of entity than routes.

## Feed Files

This specification includes the following files along with their associated content. **Bolded** files are unique to GTFS-ride, while the rest reference GTFS files. GTFS-ride follows, and by delfault adopts, changes in GTFS files already specified in GTFS-ride. If a new file is added to GTFS, its inclusion in GTFS-ride will follow the change process specified for any change to GTFS-ride. More information on the GTFS files may be found at [https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md).

|  Filename | Required | Defines |
|  ------ | ------ | ------ |
|  [agency.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#agencytxt) | **Required** | One or more transit agencies that provide the data in this feed. |
|  [stops.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#stopstxt) | **Required** | Individual locations where vehicles pick up or drop off passengers. |
|  [routes.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#routestxt) | **Required** | Transit routes. A route is a group of trips that are displayed to riders as a single service. |
|  [trips.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#tripstxt)  | **Required** | Trips for each route. A trip is a sequence of two or more stops that occurs at a specific time. |
|  [stop_times.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#stop_timestxt)  | **Required** | Times that a vehicle arrives at and departs from individual stops for each trip. |
|  [calendar.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#calendartxt)  | **Required** | Dates for service IDs using a weekly schedule. Specify when service starts and ends, as well as days of the week where service is available. |
|  [calendar_dates.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#calendar_datestxt)  | Optional | Exceptions for the service IDs defined in the [calendar.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#calendartxt) file. If [calendar.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#calendartxt) includes ALL dates of service, this file may be specified instead of [calendar.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#calendartxt). |
|  [fare_attributes.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#fare_attributestxt)  | Optional | Fare information for a transit organization's routes. |
|  [fare_rules.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#fare_rulestxt)  | Optional | Rules for applying fare information for a transit organization's routes. |
|  [shapes.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#shapestxt)  | Optional | Rules for drawing lines on a map to represent a transit organization's routes. |
|  [frequencies.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#frequenciestxt)  | Optional | Headway (time between trips) for routes with variable frequency of service. |
|  [transfers.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#transferstxt)  | Optional | Rules for making connections at transfer points between routes. |
|  [feed_info.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#feed_infotxt)  | Optional | Additional information about the feed itself, including publisher, version, and expiration information. |
|  [*__board_alight.txt__*](#board_alighttxt) | Optional | Tracks boardings/alightings along with associated information at stop-level. |
|  [*__rider_trip.txt__*](#rider_triptxt) | Optional | Includes anonymized data about specific riders' trip. |
|  [*__ridership.txt__*](#ridershiptxt) | Optional | Route or Trip level counts of ridership. |
|  [*__ride_feed_info.txt__*](#ride_feed_infotxt) | **Required** | Information specific to the source and attributes of the addional ridership files. |

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

If an agency collects disaggregate, stop-level ridership data, board_alight.txt may be used to record ridership boarding counts and additional supplementary data. If only more aggregate ridership data is collected, the agency should use ridership.txt to record ridership counts.  It should be noted that unique combinations of stop_id and trip_id will not uniquely define a specific instance in time of arrival and boardings at a stop. Boardings and other counts will be aggregated across dates active as defined by a trip’s service_id. By including an optional timestamp, an agency can disaggregate counts to specifics instances of stop arrivals and boardings, and provide a calculated current load.

|  Field Name | Required | Details |
|  ------ | ------ | ------ |
| trip_id | **Required** | The **trip_id** contains an ID that uniquely identifies a trip. |
| stop_id | **Required** | The **stop_id** contains an ID that uniquely identifies a stop. |
| stop_sequence| **Required** | The **stop_sequence** identifies the order of the stops for a particular trip. Matches **stop_sequence** in _stop_times.txt_. Non-negative integer. |
| boardings | Optional | The **boardings** field contains the number of boardings as collected by either automated or manual methods. Non-negative integer. |
| alightings | Optional | The **alightings** field contains the number of alightings as collected by either automated or manual methods. Less common than boarding data, this field is optional. Non-negative integer. |
| current_load | Optional | The **current_load** field contains the calculated percentage current load of a vehicle at the identified stop. The state at which **current_load** is measured, is specified by **load_type**; if no value is given in **load_type**, **current_load** is arriving load.  Non-negative integer.|
| load_type | Optional | The **load_type** field specifies the state (arriving or departing) at which **current_load** is measured. If no value is given, **current_load** indicates arriving load |
|   |  | * **0** - Arriving.  |
|   |  | * **1** - Departing.  |
| bike_boardings | Optional | The **bike_boardings** field contains the number of bike boardings at the identified stop and trip. This value represents both bikes racked externally and bikes brought inside the passenger compartment. Non-negative integer. |
| bike_alightings | Optional | The **bike_alightings** field contains the number of bike alightings at the identified stop and trip. This value represents both bikes racked externally and bikes brought inside the passenger compartment. Non-negative integer. |
| ramp_boardings | Optional | The **ramp_boardings** field contains the number of ramp or lift deployed boardings at the identified stop and trip. Non-negative integer. |
| ramp_alightings | Optional | The **ramp_alightings** field contains the number of ramp or lift deployed alightings at the identified stop and trip. Non-negative integer. |
| service_date | Optional | The **service_date** field contains the date of the associated boarding and/or alighting data at the identified stop. The format is YYYYMMDD. |
| service_arrival_time | Optional | The **service_arrival_time** field contains the time of the actual arrival at the identified stop. The format is HH:MM:SS. |
| service_departure_time | Optional | The **service_departure_time** field contains the time of the actual departure from the identified stop. The format is HH:MM:SS. |
| schedule_relationship | Optional | The **schedule_relationship** field identifies whether service was scheduled and operated, or scheduled but not operated, or operated but not scheduled. If a trip is added it must have a **trip_id** that is not scheduled to run on that day and is unique among trips added on that day.  |
|   |  | * **0** - (or empty) Service was scheduled and operated  |
|   |  | * **1** - whole scheduled trip was cancelled.  |
|   |  | * **2** - whole scheduled trip was cancelled (but replaced with an added trip.)  |
|   |  | * **3** - trip ran but this **stop_time** was cancelled.   |
|   |  | * **4** - trip ran but this **stop_time** was cancelled (but replaced with a different stop.)  |
|   |  | * **5** - whole trip was added. |
|   |  | * **6** - whole trip was added (as a replacement.)  |
|   |  | * **7** - this **stop_time** was added to a scheduled trip.    |
|   |  | * **8** - this **stop_time** was added to a scheduled trip (replacing something cancelled).    |
| source | Optional | The **source** field contains the collection method of the associated data. |
|   |  | * **0** - Manual.  |
|   |  | * **1** - APC.  |
|   |  | * **2** - AFC.  |
|   |  | * **3** - Model estimation.  |
|   |  | * **4** - Mixed source.  |

### *__rider_trip.txt__*

File: **Optional**

If an agency can associate supplementary ridership data with a specific rider, rider_trip.txt may be used to record the rider-generated details. Care should be exercised in the creation of the rider_id field to sufficiently anonymize a rider’s identity. The rider_trip.txt file may be useful for origin/destination, rider demographic, fare structure, network configuration, transit equity, demand forecasting, and performance review studies. 

|  Field Name | Required | Details |
|  ------ | ------ | ------ |
| rider_id | **Required** | The **rider_id** field contains the ID of a unique rider. The **rider_id** is dataset unique. |
| trip_id | Optional | The **trip_id** field contains the ID of the trip associated with the unique rider, if this is known. If **trip_id** is empty then the rider may have taken one of several trips, or several possible chains of trips, to travel between the origin and the destination.   |
| boarding_stop_id | Optional | The **boarding_stop_id** field contains the ID of the boarding stop associated with the unique rider. |
| boarding_stop_sequence | Optional | The **boarding_stop_sequence** field identifies the order of the stop referenced **boarding_stop_id** within a particular trip. Matches **stop_sequence** in _stop_times.txt_. Non-negative integer. |
| alighting_stop_id | Optional | The **alighting_stop_id** field contains the ID of the alighting stop associated with the unique rider. |
| alighting_stop_sequence | Optional | The **alighting_stop_sequence** field identifies the order of the stop referenced **alighting_stop_id** within a particular trip. Matches **stop_sequence** in _stop_times.txt_. Non-negative integer. |
| service_date | Optional | The **service_date** field contains the date of the boarding associated with the unique rider. |
| boarding_time | Optional | The **boarding_time** field contains the time of the boarding associated with the unique rider. |
| alighting_time | Optional | The **alighting_time** field contains the time of the alighting associated with the unique rider. |
| alighting_date | Optional | The **alighting_date** field contains the date of the alighting associated with the unique rider. |
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
| rider_type_description | Optional | The **rider_type_description** field contains specific descriptions of the employed rider types (e.g., _Senior - 65 and older_, _Child - 12 and under_, etc.) |
| fare_paid | Optional | The **fare_paid** field contains the amount of the fare paid by the unique rider. |
| fare_method | Optional | The **fare_method** field contains the method of payment used to collect the fare. |
|   |  | * **0** - Cash.  |
|   |  | * **1** - Transfer.  |
|   |  | * **2** - Pass.  |
|   |  | * **3** - Magnetic strip card.  |
|   |  | * **4** - RFID/Smart card.  |
|   |  | * **5** - Proof-of-Payment.  |
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

An agency may use the ridership.txt file to record aggregate level ridership counts depending on agency capabilities and requirements. If no Route ID or Trip ID is specified, the ridership count is system wide. If stop-level ridership counts are available, they should be recorded in board_alight.txt, but an agency may choose to also record the aggregated counts in ridership.txt to aid in meeting specific reporting requirements or in generating user-defined reports.  

|  Field Name | Required | Details |
|  ------ | ------ | ------ |
| ridership_count | **Required** | The **ridership_count** field contains the count desired for the selected segment of ridership count. |
| ridership_start_date | **Required** | The **ridership_start_date** field contains the date of the start of the rideship count. The date format is YYYYMMDD. |
| ridership_end_date | **Required** | The **ridership_end_date** field contains the date of the end of the rideship count. **ridership_end_date** may be the same date or later than **ridership_start_date**. |
| ridership_start_time | Optional | The **ridership_start_time** field contains the time of the start of the rideship count on the date specified in **ridership_start_date**. The time format is HH:MM:SS. |
| ridership_end_time | Optional | The **ridership_end_time** field contains the time of the end of the rideship count on the date specified in **ridership_end_date**. If **ridership_start_date** and **ridership_end_date** are the same, **ridership_end_time** must be later than **ridership_start_time**. |
| route_id | Optional | The **route_id** field contains an ID that uniquely identifies a route. This value is referenced from the [routes.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#routestxt) file. |
| trip_id | Optional | The **trip_id** field contains an ID that uniquely identifies a trip. This value is referenced from the [trips.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#tripstxt) file. |
| direction_id | Optional | The **direction_id** field contains an ID that identifies the direction of travel for a trip. This value is referenced from the [trips.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#tripstxt) file. |
| stop_id | Optional | The **stop_id** field contains an ID that uniquely identifies a stop. This value is referenced from the [stops.txt](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md#stopstxt) file. |

### *__ride_feed_info.txt__*

File: **Required**

This file is similar to the GTFS feed_info.txt, but with a specific focus on metadata for the additional ridership files.

|  Field Name | Required | Details |
|  ------ | ------ | ------ |
| ride_files | **Required** | The **ride_files** field indicates the files containing valid ridership data. |
|   |  | * **0** - board_alight  |
|   |  | * **1** - rider_trip  |
|   |  | * **2** - ridership  |
|   |  | * **3** - board_alight and rider_trip  |
|   |  | * **4** - board_alight and ridership |
|   |  | * **5** - rider_trip and ridership |
|   |  | * **6** - board_alight, rider_trip, and ridership |
| ride_start_date | Optional | The **ride_start_date** field indicates the earliest date for the ridership data contained in the fileset. The date may match or be later than the **feed_start_date** of _feed_info.txt_. The date format is YYYYMMDD. |
| ride_end_date | Optional | The **ride_end_date** field indicates the latest data for the ridership data contained in the fileset. It must be later than the **ride_start_date** and either match or be earlier than the **feed_end_date** of _feed_info.txt_. |
| gtfs_feed_date | Optional | The **gtfs_feed_date** indicates the date the GTFS files contained in the GTFS-ride fileset were fetched as the current GTFS feed. If **feed_version** is not included in _feed_info.txt_, **gtfs_feed_date** allows association of GTFS files to when they were supplied as current.
| ride_feed_version | Optional | The **ride_feed_version** is a feed publisher string used to determine the sequence of feed publication. It can be used to represent the most current data for feeds covering the same period.
