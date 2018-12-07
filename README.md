# CSV Export from eCX using a Date Range

The eCX API has a few date ranging query parameters already built in - date modified, and date discovered.

Both modified and discovered take an integer epoch date value, more on epoch dates, as well as converters and other language specific tools, can be found at https://www.epochconverter.com/ 

When data is submitted to eCX we keep a `created` epoch date value in the database, as well as a `modified` epoch date value - both being set to the same timestamp on creation.  

The eCX API allows users to update various values in an entity via a PATCH operation, and when a PATCH query is performed the `created` date value is left unchanged, but the `modified` epoch is updated to now().  Because the eCX API default output sort order is in `modified` descending, this change to `modified` on PATCH allows the newly updated data to "bubble" to the top of the API output, which gets changes out to the community immedietly.  

### Ranging Options: ###

Within the eCX Modules (APWG fed and supported) there are both date discovered and date modified query parameters.  Within Workgroups (APWG member created, fed and supported) there, at a minimum, will be date modified, with the potential for other date fields.  Any date field will have a ranging option available for it.  All possible eCX API query parameters are in the [eCX API Documentation](https://ecrimex.net/api) tab off the main menu, or on a menu tab within each Workgroups home area. 

The query parameter names for date modified are mod_date_start and mod_date_end.  For date discovered the query parameter names are dd_date_start and dd_date_end, again all of these parameters take an integer epoch date value - ie `dd_date_start=1544211463` (converts to  Friday, December 7, 2018 11:37:43 AM GMT-08:00)

### CSV Output: ###
The eCX API supports CSV for the `/phish` eCX API endpoint when using the `container=csv` query parameter


### Step 1: ###
Know the date ranges (date, time, and timezone) for beginning and ending values.  Know which date value you want to query, date discovered and/or date modified, you can use both.  Convert these datetime values to epochs.  Every programming language has a function to perform this conversion, also known as "Unix time".

### Step 2: ###
Know your eCX API token key.  Your eCX API token key can be found on your [eCX profile page](https://ecrimex.net/users/update) by clicking on your name in the header menu.  This eCX API token will go in the header of your GET request using a key/value pair 
```javascript
    "Authorization: <your eCX API otken key goes here",
    "Content-Type: application/json"
```
Note that we set the Content-Type in the header as well, we're sending the eCX API JSON data, and getting CSV back.


### Step 4: ###

