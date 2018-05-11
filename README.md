# xMatters REST API's for Postman
This repository provides you with a Postman collection that contains all xMatters Rest API end points as of May 3 / 2018.

* 176 xMatters API requests.
* JavaScript and JSON generated payloads for each api.
* Runner Collections to automate processes that require multiple API request.
* Build your own custom Runners to string together multiple api requests.
* Automatically adds Postman environment variables with returned results from api reuqests. This allows you to chain multiple API's together without needing to manually move UUID's from one request to the next.
* Make multiple API requests using postman Runners to import large datasets into xMatters from a csv files.
* Test the xMatters API without being an API expert.

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

# Pre-Requisites
* [Postman](https://www.getpostman.com)
* xMatters account - If you don't have one, [get one](https://www.xmatters.com)!

# Files

[Download the Postman Collection](xMatters-Rest-API.postman_collection.json)
After unziping, this file can be imported into postman to give you access to all api resources in xMatters as of May 3 / 2018.

**Runner Data Import Example Files**
* [postman-Groups.csv](postman-Groups.csv) - Example data file to use with Postman Runner (Create Groups) for making a large number of api requests automatically.
* [postman-Shifts.csv](postman-Shifts.csv)
* [postman-Members.csv](postman-Members.csv)  - Example data file to use with Postman Runner(Add members to group) for making a large number of api requests automatically.
* [postman-Members-Roster.csv](postman-Members-Roster.csv)
* [postman-Sites.csv](postman-Sites.csv)
* [postman-Group-Export.csv](postman-Group-Export.csv)
* [Import Sites.csv](postman-Sites.csv)

# Installation

## Postman Setup
1. **Download and install Postman from here** (link: https://www.getpostman.com/apps)

2. **Unzip then Import the Postman collection downloaded from the following link**:
[Download the Postman Collection](xMatters Rest API postman_collection.zip)
This file can be imported into postman to give you access to all api resources in xMatters as of May 3 / 2018.

3. **Add authorization to the xMatters REST API collection.**
https://www.getpostman.com/docs/v6/postman/sending_api_requests/authorization

      a. Click on the ellipsis (…) next to the collection name (xMatters Rest API), and select “Edit” to open the EDIT COLLECTION modal.

     b. Click the Authorization Tab.

      Add Authentication parameters to authenticate into xMatters. To learn more about authentication for xMatters Rest api go [here]
    (https://help.xmatters.com/xmAPI/#authentication)

4. **Define [Collection variables]**(https://www.getpostman.com/docs/v6/postman/environments_and_globals/variables#defining-collection-variables)
Collection variables can be defined by editing the collection details. 

     a. Click on the ellipsis (…) next to the collection name (xMatters Rest API), and select “Edit” to open the EDIT COLLECTION modal. 

     b. Select the Variables tab to edit collection variables.

Below is a list of collection variable, what API's they are used in and sample values

| Variable             | Description          | Example Data         |
|----------------------|----------------------|----------------------|
| Host_Name            | xMatters base url. Used in endpoint of all api's   | company.xmatters.com/ |
| recipient_name       | user name to use when initiating new events | mmcbride |
| propertyName         | Name of a form property to use when searching events by property | Severity |
| propertyValue        | Value of form property to search for when searching events using Events API | Sev-2 |
| list_property_UUID   | UUID of a List form property. Used with the Forms API to update property values | 53a6300-43jf3-d343-d434322ab |
| hi_property_UUID     | UUID of a Hierarchy form property. Used with the Forms API to update property values | 33a6300-43jf3-d343-d434322ab |
| groupID              | Group name to use with Groups API | Executives |
| rest_user_UUID       | The UUID of the xMatters user configured to Authenticate postman API calls. This is the UUID of the user defined in Authorization tab of the collection.  This uuid/user is set as a group supervisor when creating groups. This allows you to also edit a group after it has been created using postman. |5fs98300-43jfs3-d343-d4sdf2ab |
| personID             | A user ID to be used with the People API. This user does not need to exist in xMatters. The Create person API can create this user for you. | mmcbride | 
| client_id            | xMatters Client ID used for OAuth Api's. You can get this from Developer > oAuth. | 9304300-43ffjf3-d343-d4sdf34ab |
| oauth_username       | xMatters userID for the user that will authenticate using oAuth. | rest |
| oauth_password       | xMatters user password used for the userID provided in oauth_username. | hardtorememberpassword |
| supervisorID         | xMatters userID for a supervisor that will be created using People Api for Create a person Supervisor | bigboss |
| web_service_UUID     | The web service UUID of a form that has Access Web Services URL enabled. This is for creating new xMatters events. | 1dsd34300-4asjf3-d363-g23dedd233 |
| inbound_UUID         | The UUID of an inbound integration for triggering new events in xMatters via an inbound integration. |1dsd34300-4asjf3-d363-g23dedd233 |
| siteID               | Defines the name of a Site for the Site API. | Default Site |
| subscriptionformUUID | The UUID of a subscription form. THis is used for the subscription API. | 77sds2d98-s2323-dssa23-ddsd4553cd |
| profilePropertName   | The name of a custom field that you want to search when using Get people Search API | IT Knowledge |
| profilePropertValue  | The value of a custom field that you want to search when using Get people Search API | CSS |

Depening on what API's you intend to use not all values above are required. For best results I suggest populating all values.

5. **Have fun and enjoy!**

## xMatters Setup
Create an xMatters user that can authenticate using REST API.
(https://help.xmatters.com/xmAPI/#authentication)

# How it works
Provided in this Postman collection are all xMatters API's available as of May 3 / 2018. 

The way to use this is to update the collection variables as explained below to your specific usecase.  Once the variables are set, all apis will work together.

Each api call made in postman will save an evironment variable related to the api just used. This will allow you to make subsiquent api calls that use the results of the previous api.

This means you can do things like the following example.


| API                                  | Collection Variable Used  | Environment Variable used | Environment Variable Created |
|--------------------------------------|---------------------------|---------------------------|------------------------------|
| 1. Create a new Site                 | siteID                    |                           | siteUUID                     |
| 2. Create a new Person Supervisor    | supervisorID              | siteUUID                  | supervisorUUID               |
| 3. Create a new User                 | personID                  | siteUUID, supervisorUUID  | personUUID                   |
| 4. Modify a User                     | personID,profilePropertName,profilePropertValue | personUUID, supervisorUUID  | personUUID |
| 5. Add device to user (from step 3)  |                           | personUUID                | deviceUUID                   |
| 6. Create a new Group                | groupID                   |                           | groupUUID                    | 
| 7. Create new shift (Group from 5)   | groupID                   |                           | shiftID, shiftUUID           | 
| 8. Add member to shit (Shift from 6) | groupID                   |                           |                              | 
| 9. Add member to shit (Shift from 6) | groupID                   |                           |                              | 
| 10. Create a new Group               | groupID                   |                           | groupUUID                    | 


* All Api Call are availiable is JavaScript and JSON format.

## JavaScript Format
Javascript format uses Postman Pre-request Scripts to build a json object that gets posted as raw body in application/json format.

The JavaScript formatted request allow you to add your own code and customize the api as requried.

The last couple lines of Postman Pre-request Scripts use Postman functions to set environment variables and log the payload that is used in the post body.

*Example:*
```
// Set Postman environment variable named data.
pm.environment.set("data", JSON.stringify(data));

// Log the data json object so you can easily copy the format. 
// Access Postman logs from *View -> Show Postman Console.*
console.log("Data",JSON.strinify(data))
```

## Json Format
JSON formatted request are provided in raw body application/Json format and do not allow any javascript.

## Runners
Runners are groups of API calls that will run one after another. You can use these to create a site, create a user, and then add a user device all in one action.

Several Runners have been included that are ready to use:

- Create User with Devices
- Create Group with Shifts and Members
- Create Groups from a Data File
- Add member to group roster from Data File
- Create Groups From xMaters Group Export using Data File
- Import Sites from Data File

## Runner General Use Instructions
You can access Runners by Clicking the **Runner** button in top left corner of Postman.
[Runner Help](https://www.getpostman.com/docs/v6/postman/collection_runs/starting_a_collection_run)

Some runners included above require a csv data file. Postman will run through the apis in the selected runner once for each row of provided data.

This allows you to do things like import a list of groups, add members to a groups or import sites from postman.

Postman will process each row of data provided and use each column as a variables for the api.

## Runner Explainations:

### Create User with Devices
This runner will create a user along with devices from Collection Variables:

**Steps:**
  - *Get a Site* (Gets the UUID of the site specified in the api call that a person will be added to.)
  - *Create a person Supervisor* (Creates a person supervisor. This user will be the supervisor for the person created in the next step.)
  - *Create a person* (Creates a person.)
  - *Create a device* (Adds a device to the person created in the last step. Add additional Create device Api calls to add more than one device and specify sequence and delays between then.)


### Create User with Devices
This runner will create a group, shifts and members from Collection Variables.

**Steps:**
- Create a person Supervisor
- Create a person
- Create a group
- Create a shift (recurring)
- Create a shift (24x7)
- Add a member to a shift (Peer)
- Add a member to a shift (Management)

### Create Groups from Data file
This runner will Add Multiple Groups from a csv data file.

**Data File Format**: [Create Groups](postman-Groups.csv)

The following data format would create 3 new groups in xMatters and set a specific user supervisor to each group.


|  Group Name     |	supervisorUUID                       |
|-----------------|--------------------------------------|
| DBA Team       	| 374551cb-76f9-41c7-bffc-723d9b6b6e34 |
| Network Admin	  | 374551cb-76f9-41c7-bffc-723d9b6b6e34 | 
| CCV Daily SYnc	| 374551cb-76f9-41c7-bffc-723d9b6b6e34 |




### Add Shifts from Data File
- This runner will Add shifts to Groups from a data file.
- This runner is best ran after the *Create Groups from Data File* Runner above.
- This runner can be used to add all of the shifts to the groups added in the previous runner.
- Atttempts to add shifts to groups that are not yet in xMatters will fail.
- This is a very complicated datafile and the headings will mean very little to you.

Please read the xMatters API documentation for Shift Object to understand what values can be put in this file.
[Shift Object] (https://help.xmatters.com/xmAPI/?javascript#shift-objects)

**Data File Format**: [Add Shifts](postman-Shifts.csv)

Add new lines one for each shift you want to add. You can have mutiple shifts per group and you can add shifts to more than one group at a time.

| Group Name | Shift Name             | Shift Description       | Start Time               | End Time                 | Frequency | On          |	Months                   | End By | DayofWeek Clarifyer | DayofWeek | 
|------------|------------------------|-------------------------|--------------------------|--------------------------|-----------|-------------|--------------------------|--------|---------------------|-----------| 
| Open Desk  | Quarterly Monday Stock | Shift to cover...       |	2018-03-05T13:00:00.000Z | 2018-03-05T22:00:00.000Z	| MONTHLY	  | DAY_OF_WEEK |	MAR", "JUN", "SEP", "DEC | NEVER |	FIRST               |	MO        |



### Add Members to Shift from Data File
- This runner will members to the shifts created in the previous runner (Add Shifts from Data File).
- This runner is best ran after the *Add Shifts from Data File* Runner above.
- This runner can be used to add all of the members to a shift or multiple shifts and includes, position, delays, escalations and rotations.
- Al users / groups must have already been added to xMatters. If a user or group is not already in xMatters, the shift member will not be added.

**Data File Format**: [Add Members to Shift](postman-Members-Shifts.csv)

| Group Name | Shift Name             | Position  | Delay  | escalationType  | In Rotation | Member ID   |
|------------|------------------------|-----------|--------|-----------------|-------------|-------------|
| Open Desk  | Quarterly Monday Stock | 1         |	0      | None            | True        | mmcbride    |	
| Open Desk  | Quarterly Monday Stock | 2         |	10     | Peer            | True        | lskywalker  |	
| Open Desk  | Quarterly Monday Stock | 3         |	15     | Management      | False       | hhandyman   | 	




### Add members to Group Roster from Data File
- This runner will Add members to the Group Roster. 
- Group Roster are people in the group but not on any shift.
- If you would like to add people to a shift you will need to use a different runner.


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


### Add members to Group Roster from Data File
- This runner will Add members to the Group Roster. 
- Group Roster are people in the group but not on any shift.
- If you would like to add people to a shift you will need to use a different runner.


**Data File Format**: [Add members to Group Roster](postman-Sites.csv)


| Site Name    | Status	      | Language     | Time Zone    |	Address 1    | Address 2    |	City         | State        | Country       | Zip          | Latitude     | Longitude    |
|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|---------------|--------------|--------------|--------------|
| Calgary      | Active	      | English      | US/Pacific   |	10 Avenue SE |              |	Calgary      | AB           | Canada        | T2G 0W2      | 51.0416473   | -114.0383162 |
| Texas        | Active	      | English      | US/Easters   |	6 Ashley Dr  |              |	Tyler        | TX           | United States | 75703        | 32.2556612   | -95.3207069  |

### Create Groups From xMatters Group Export Using Data File
- This runner will use the xMatters Group Export csv file as a Data File input to add groups and members to xMatters. 
- The usecase there would be to export groups from Non-Prod and use this runner to import groups into production.
- Export this file from your xMatters environment as follows: Login to xMatters > Groups > Export Groups (Button on far right)

[Export Groups From xMatters](https://help.xmatters.com/OnDemand/groups/groups-create-delete-export.htm)


**Data File Format**: [Create Groups from xMatters Group Export](postman-Group-Export.csv)

**Requirements**
- User must already be in xMatters. 
This runner does not add members who are not already in your xMatters environment.

- You may run into some complications with nested groups. If the group does not already exist, it will fail. 
Depending on the order of your group export file, it may work for some nested groups and not others. 
This will depend if the group was alread greated before attempting to add the group as a member.


### Import Sites from Data File
This runner will import a list of sites containied in a datafile.

**Data File Format**: [Import Sites](postman-Sites.csv)


| Site Name	 |  Status	 |  Language	 |  Time Zone	 |  Address 1	 |  Address 2	 |  City	 |  State	 |  Country	 |  Zip	  |  Latitude	 |  Longitude	   |
|------------|-----------|-------------|-------------|-------------|-------------|---------|---------|-----------|--------|-------------|--------------|
| Calgary    | Active    | English     |  US/Pacific | 123 Street  |             | Calgary | AB      | Canada    | T2G0W2 | 51.0416473  |	-114.0383162 |

You can easily create your own runners along with your own custom data.

## Misc
Some miscelaneous information.

### Variables
{{value}} indicates a reference to a collection or environment variable be careful when changing these. It is advised to change the variable value not the reference.  You cannot set environment variables. You can only set Collection variables.

### Tests
All requests, no matter the format, set environment variables in the Tests tab of Postman.

# xm-labs-PostMan-APIs
