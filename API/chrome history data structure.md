[chrome history file struct](https://docs.nxlog.co/integrate/browser-history.html)

Table 1. Chrome history - _urls_ table structure
The most important !!!!

|Column|Type|Description|
|---|---|---|
|`id`|`INTEGER`|Primary Key - a unique ID for the record|
|`url`|`LONGVARCHAR`|The URL that was accessed|
|`title`|`LONGVARCHAR`|The title of the website|
|`visit_count`|`INTEGER`|The number of times the URL was accessed|
|`typed_count`|`INTEGER`|The number of times the user got to this website by typing the URL in the address bar|
|`last_visit_time`|`INTEGER`|Timestamp in nanoseconds when the website was last visited|