# xMatters REST API's for Postman
This repository provides you with a Postman collection that contains all xMatters Rest API end points as of May 3 / 2018. It also includes Postman Runners that allow you to chain API requests together to do cool things.

* 176 xMatters API requests.
* JavaScript and JSON payloads for each API.
* Runner Collections to automate processes that require multiple API request.
* Build your own custom Runners to string together multiple API requests.
* Automatically adds Postman environment variables with returned results from API requests. This allows you to chain multiple API's together without needing to manually move UUID's from one request to the next.
* Make multiple API requests using postman Runners to import large datasets into xMatters from a csv files.
* Use the xMatters API without being an API expert.

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

# Pre-Requisites
* [Postman](https://www.getpostman.com)
* xMatters account - If you don't have one, [get one](https://www.xmatters.com)!

# Files

[Download the Postman Collection](xMatters-Rest-API.postman_collection.json.zip) - Unzip then import into postman. Instructions provided below.

**Runner Data Import Example Files**


* [postman-Groups.csv](postman-Groups.csv) - Use with "Create Groups from Data File" runner. Adds a list of Groups to xMatters.
* [postman-Shifts.csv](postman-Shifts.csv) - Use with "Create Shifts from Data File" runner. Adds a list of Shifts to existing xMatters Groups.
* [postman-Members-Shifts.csv](postman-Members-Shifts.csv) - Use with "Add Members to Shifts from Data File" runner. Adds a list of existing users to existing xMatters Shifts.
* [postman-Members-Roster.csv](postman-Members-Roster.csv) - Use with "Add Members to Group Roster from Data File" runner. Adds a list of existing users to existing xMatters Groups as a member of the roster but not part of a shift.
* [postman-Group-Export.csv](postman-Group-Export.csv) - Use with "Create Groups From xMatters Group Export using Data File" runner. Adds Groups, Shifts and Members to xMatters using the Group Export file. Users must already be in xMatters. All information in the Group Export is used but the group export does not contain all shift information that may exist in xMatters for a particular group.
* [postman-Sites.csv](postman-Sites.csv) - Use with "Import Sites from Data File" runner. Adds a list of sites to xMatters.

# Installation

## Postman Setup
1. **Download and install Postman from [here](https://www.getpostman.com/apps)** 

2. **Download the Postman Collection [here](xMatters-Rest-API.postman_collection.json.zip)** 

3. **Unzip** then Postman Collection downloaded in step 2.  

4. **Import** the Postman collection. Instructions [here](https://www.getpostman.com/docs/v6/postman/collections/data_formats#exporting-and-importing-postman-data)

5. **Add Authorization to the xMatters REST API collection.** [Postman Instructions](https://www.getpostman.com/docs/v6/postman/sending_api_requests/authorization)

     a. Click on the ellipsis (…) next to the collection name (xMatters Rest API), and select “Edit” to open the EDIT COLLECTION modal.

     b. Click the Authorization Tab.

      Add Authentication parameters to authenticate into xMatters. To learn more about authentication for xMatters Rest API go [here](https://help.xmatters.com/xmAPI/#authentication)

6. **Define [Collection Variables](https://www.getpostman.com/docs/v6/postman/environments_and_globals/variables#defining-collection-variables)**
Collection variables can be defined by editing the collection details. 

     a. Click on the ellipsis (…) next to the collection name (xMatters Rest API), and select “Edit” to open the EDIT COLLECTION modal. 

     b. Select the Variables tab to edit collection variables.

Below is a list of collection variable, what API's they are used in and sample values

| Variable             | Description          | Example Data         |
|----------------------|----------------------|----------------------|
| Host_Name            | xMatters base url. Used in endpoint of all API's.   | company.xmatters.com/ |
| recipient_name       | user name to use when initiating new events. | mmcbride |
| propertyName         | Name of a form property to use when searching events by property. | Severity |
| propertyValue        | Value of form property to search for when searching events using Events API. | Sev-2 |
| list_property_UUID   | UUID of a List form property. Used with the Forms API to update property values. | 53a6300-43jf3-d343-d434322ab |
| hi_property_UUID     | UUID of a Hierarchy form property. Used with the Forms API to update property values. | 33a6300-43jf3-d343-d434322ab |
| groupID              | Group name to use with Groups API. | Executives |
| rest_user_UUID       | The UUID of the xMatters user configured to Authenticate postman API calls. This is the UUID of the user defined in Authorization tab of the collection.  This uuid/user is set as a group supervisor when creating groups. This allows you to also edit a group after it has been created using postman. |5fs98300-43jfs3-d343-d4sdf2ab |
| personID             | A user ID to be used with the People API. This user does not need to exist in xMatters. The Create person API can create this user for you. | mmcbride | 
| client_id            | xMatters Client ID used for OAuth API's. You can get this from Developer > oAuth. | 9304300-43ffjf3-d343-d4sdf34ab |
| oauth_username       | xMatters userID for the user that will authenticate using oAuth. | rest |
| oauth_password       | xMatters user password used for the userID provided in oauth_username. | hardtorememberpassword |
| supervisorID         | xMatters userID for a supervisor that will be created using People API for Create a person Supervisor. | bigboss |
| web_service_UUID     | The web service UUID of a form that has Access Web Services URL enabled. This is for creating new xMatters events. | 1dsd34300-4asjf3-d363-g23dedd233 |
| inbound_UUID         | The UUID of an inbound integration for triggering new events in xMatters via an inbound integration. |1dsd34300-4asjf3-d363-g23dedd233 |
| siteID               | Defines the name of a Site for the Site API. | Default Site |
| subscriptionformUUID | The UUID of a subscription form. This is used for the subscription API. | 77sds2d98-s2323-dssa23-ddsd4553cd |
| profilePropertName   | The name of a custom field that you want to search when using Get people Search API. | IT Knowledge |
| profilePropertValue  | The value of a custom field that you want to search when using Get people Search API. | CSS |

Depending on what API's you intend to use, not all values above are required. For best results I suggest populating all values.

7. **Have fun and enjoy!**

## xMatters Setup
Create an xMatters user that can authenticate using REST API.
(https://help.xmatters.com/xmAPI/#authentication)

# How it works
Provided in this Postman collection are all xMatters API's available as of May 3 / 2018. It also includes Postman Runners that allow you to chain API requests together to do cool things.

To use this, update the collection variables as explained above to your specific use case.  Once the variables are set, all APIs will work together.

Each API call made in postman will save an environment variable related to the API just used. This will allow you to make subsequent API calls that use the results of the previous API.

This means you can do things like the following:


| API                                  | Collection Variable Used  | Environment Variable used | Environment Variable Created |
|--------------------------------------|---------------------------|---------------------------|------------------------------|
| 1. Create a new Site                 | siteID                    |                           | siteUUID                     |
| 2. Create a new Person Supervisor    | supervisorID              | siteUUID                  | supervisorUUID               |
| 3. Create a new User                 | personID                  | siteUUID, supervisorUUID  | personUUID                   |
| 4. Modify a User                     | personID,profilePropertName,profilePropertValue | personUUID, supervisorUUID  | personUUID |
| 5. Add device to user (from step 3)  |                           | personUUID                | deviceUUID                   |
| 6. Create a new Group                | groupID                   |                           | groupUUID                    | 
| 7. Create new shift (Group from 5)   | groupID                   |                           | shiftID, shiftUUID           | 
| 8. Add member to shift (Shift from 6)| groupID                   |                           |                              | 
| 9. Add member to shift (Shift from 6)| groupID                   |                           |                              | 
| 10. Create a new Group               | groupID                   |                           | groupUUID                    | 


* All API Call are available is JavaScript and JSON format.

## JavaScript Format
JavaScript format uses Postman Pre-Request Scripts to build a json object and save it into a Postman environment variable {{data}}. This gets posted as raw body in application/json format.

The JavaScript formatted request allow you to add your own code and customize the API as required.

The last couple lines of Postman Pre-Request Scripts use Postman functions to set environment variables and log the payload that is used in the post body.

*Example:*
```
// Set Postman environment variable named data.
pm.environment.set("data", JSON.stringify(data));

// Log the data json object so you can easily copy the format. 
// Access Postman logs from *View -> Show Postman Console.*
console.log("Data",JSON.strinify(data))
```

Many of the API's will also use Postman Tests to save part of the response into an environment variable for easy API chaining. Typically this will save the UUID.

*Example:*
```
let jsonData = JSON.parse(responseBody);

tests['Get Device Successfull: ' + jsonData.id];
postman.setEnvironmentVariable('deviceUUID', jsonData.id);
```


## Json Format
JSON formatted request are provided in raw body application/json format and do not allow any JavaScript. If you want to customize this format you will need to change the json body directly. No JavaScript logic can be used for this format.



## Runners
Runners are groups of API calls that will run one after another. You can use these to create a site, create a user, and then add a user device all in one action.

Several Runners have been included that are ready to use:

- Create User with Devices
- Create Group with Shifts and Members

- Create Groups from a Data File
- Create Shifts from Data File 
- Add Members to Shift from Data File
- Add member to group roster from Data File

- Create Groups From xMatters Group Export using Data File
- Import Sites from Data File

## Runner General Use Instructions
You can access Runners by Clicking the **Runner** button in top left corner of Postman.
[Runner Help](https://www.getpostman.com/docs/v6/postman/collection_runs/starting_a_collection_run)

Some runners require a csv data file. Postman will run through the API's in the selected runner once for each row of provided data.

This allows you to import a list of groups, add members to a group or import sites from postman.

Postman will process each row of data provided and use each column as variables for the API.

You can easily create your own runners along with your own custom data.

## Runner Explanations:

### Create User with Devices
This runner will create a user along with devices from Collection Variables. It does not use a csv data file.

**Steps:**
  - *Get a Site* (Gets the UUID of the site specified in the API call that a person will be added to.)
  - *Create a person Supervisor* (Creates a person supervisor. This user will be the supervisor for the person created in the next step.)
  - *Create a person* (Creates a person.)
  - *Create a device* (Adds a device to the person created in the last step. Add additional Create device API calls to add more than one device and specify sequence and delays between then.)




### Create Group with Shifts and Members
This runner will create a group, shifts and members from Collection Variables.

**Steps:**
- Create a person Supervisor
- Create a person
- Create a group
- Create a shift (recurring)
- Create a shift (24x7)
- Add a member to a shift (Peer)
- Add a member to a shift (Management)



###The Next 4 Runners are designed to use together one after another:###

Before using these runners please ensure users have been added to xMatters. If users do not exist these will fail.

1. Create Groups from Data file
2. Add Shifts from Data File

  3. Add Members to Shift from Data File
    or (Use 3 or 4 depending on what you want to do.)
  4. Add Members to Group Roster from Data File



### Create Groups from Data file
This runner will Add Multiple Groups from a csv data file.

**Data File Format**: [Create Groups](postman-Groups.csv)

The following data format would create 3 new groups in xMatters and set a specific user supervisor to each group.


|  Group Name     |	Group Description                    |	supervisorUUID                      |
|-----------------|--------------------------------------|--------------------------------------|
| DBA Team       	| A Team for opening new tickets       | 374551cb-76f9-41c7-bffc-723d9b6b6e34 |
| Network Admin	  | A team of slackers                   | 374551cb-76f9-41c7-bffc-723d9b6b6e34 |
| CCV Daily Sync	|                                      | 374551cb-76f9-41c7-bffc-723d9b6b6e34 |




### Add Shifts from Data File
- This runner will Add shifts to Groups from a data file.
- This runner is best used after the *Create Groups from Data File* runner above.
- This runner can be used to add all the shifts to the groups added in the previous runner.
- Groups must already exist in xMatters.
- This is a complicated data file and the headings will mean very little to you without reading xMatters API Document on Shift Object.
- Not all columns are needed for each type of shift.
- The sample files come with 24 shifts types and sample data for each type. Blank values mean it's not needed for the particular shift type.

Please read the xMatters API documentation for Shift Object to understand what values can be put in this file.
[Shift Object] (https://help.xmatters.com/xmAPI/?javascript#shift-objects)

**Data File Format**: [Add Shifts](postman-Shifts.csv)

Add new lines one for each shift you want to add. You can have multiple shifts per group and can add shifts to more than one group at a time.


| Group Name |	Shift Name	          | Shift Description	      | start                 	 | end                  	  | frequency |	endBy   	  |	date  	  |	repetitions	| repeatEvery |	onDays    |	on	         | Months               	   | dayOfWeekClassifier |	dayOfWeek	    |dateOfMonth |
|------------|------------------------|-------------------------|--------------------------|--------------------------|-----------|-------------|-----------|-------------|-------------|-----------|--------------|---------------------------|---------------------|----------------|------------|
| Open Desk  | MONTHLY ENDBY: NEVER   | Shift to cover first..  |	2018-03-05T13:00:00.000Z | 2018-03-05T22:00:00.000Z	| MONTHLY	  | NEVER       |           |	            |             |           | DAY_OF_WEEK  | MAR", "JUN", "SEP", "DEC  |	FIRST              |	MO            |            |




### Add Members to Shift from Data File
- This runner will add members to the shifts created in the previous runner (Add Shifts from Data File).
- This runner is best used after the *Create Groups from Data file* and *Add Shifts from Data File* runners above.
- This runner can be used to add all the members to a shift or multiple shifts and includes, position, delays, escalations and rotations.
- Users/Members must already exist in xMatters.
- Groups must already exist in xMatters.
- Shifts must already exist in xMatters.
- If a user, shift or group is not already in xMatters, the shift member will not be added.

**Data File Format**: [Add Members to Shift](postman-Members-Shifts.csv)

| Group Name | Shift Name             | Position  | Delay  | escalationType  | In Rotation | Member ID   |
|------------|------------------------|-----------|--------|-----------------|-------------|-------------|
| Open Desk  | Quarterly Monday Stock | 1         |	0      | None            | True        | mmcbride    |	
| Open Desk  | Quarterly Monday Stock | 2         |	10     | Peer            | True        | lskywalker  |	
| Open Desk  | Quarterly Monday Stock | 3         |	15     | Management      | False       | hhandyman   | 	




### Add Members to Group Roster from Data File
- This runner will Add members to the Group Roster. 
- Group Roster are people in the group but not on any shift.
- If you would like to add people to a shift you will need to use the *Add Members to Shift from Data File* runner above.
- Users/Members must already exist in xMatters.
- Groups must already exist in xMatters.

**Data File Format**: [Add members to Group Roster](postman-Members-Roster.csv)

|  groupID        |	personID     |
|-----------------|--------------|
| DBA Team       	| jhanden      |
| DBA Team       	| mmcbride     |
| DBA Team       	| ckimal       |
| Network Admin	  | mmcbride     | 
| Network Admin	  | mchammer     | 
| CCV Daily SYnc	| jsmith       |
| CCV Daily SYnc	| lskywalker   |
| CCV Daily SYnc	| rbrans       |
| CCV Daily SYnc	| kbundy       |



### Create Groups From xMatters Group Export Using Data File
- This runner will use the xMatters Group Export csv file as a Data File input to add groups and members to xMatters. 
- The use case here would be to export groups from Non-Production environment and use this runner to import groups into Production.
- Export this file from your xMatters environment as follows: Login to xMatters > Groups > Export Groups (Button on far right)

[Export Groups From xMatters](https://help.xmatters.com/OnDemand/groups/groups-create-delete-export.htm)


**Data File Format**: [Create Groups from xMatters Group Export](postman-Group-Export.csv)

**Requirements**
- Users must already be in xMatters. 
This runner does not add members who are not already in your xMatters environment.

- You may run into some complications with nested groups. If the group does not already exist, it will fail. 
Depending on the order of your group export file, it may work for some nested groups and not others. 
This will depend if the group was already created before attempting to add the group as a member.



### Import Sites from Data File
This runner will import a list of sites contained in a data file.

**Data File Format**: [Import Sites](postman-Sites.csv)

**Requirements**
- Language must be enabled to create a site with a particular language.
- Time Zone must be enabled in Admin > Time Zones. Proper format is just the name and does not include the UTC time. Ex: US/Mountain
- Country must be enabled in Admin > Countries. Proper format is exact name listed in selected country. 
- Include Latitude and Longitude if you want the site to automatically be Geocoded.
- Site Names must be unique.


| Site Name    | Status	      | Language     | Time Zone    |	Address 1    | Address 2    |	City         | State        | Country       | Zip          | Latitude     | Longitude    |
|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|---------------|--------------|--------------|--------------|
| Calgary      | Active	      | English      | US/Pacific   |	10 Avenue SE |              |	Calgary      | AB           | Canada        | T2G 0W2      | 51.0416473   | -114.0383162 |
| Texas        | Active	      | English      | US/Eastern   |	6 Ashley Dr  |              |	Tyler        | TX           | United States | 75703        | 32.2556612   | -95.3207069  |






## Misccellaneous
Some miscellaneous information.

### Variables
{{value}} indicates a reference to a collection or environment variable in Postman be careful when changing these. It is advised to change the variable value not the reference. You can only set Collection Variables as instructed [here](https://www.getpostman.com/docs/v6/postman/collections/data_formats#exporting-and-importing-postman-data)

Environment variables need to be set from the Pre-Request or Test section of Postman.

### Tests
All requests, no matter the format, set environment variables in the Tests tab of Postman.

### Typical Data File Error
When editing a data file with Excel you must save the file as a csv.  Excel sometimes formats this poorly and adds an extra line at the end.
This will result in the last item in your data file failing.
Usually you will see a "/r" at the end of your last data parameter. This indicates an extra blank line was added to your csv file and it will cause a problem.

To resolve this just open the csv file in a text editor and remove the last blank line and save.