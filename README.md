# node-caldav-server
This is a CalDav server written by express.js with babel, using pure ES6 features to develop

## Features
- support multiple users with sqlite database
- much faster than radicale
- offer additional APIs for microservice
- easy to implement authentication
- easy to migrate to any other database  
- friendly with developer because of ES6/ES7 features thanks to babel
- detailed documents for both deployment and use

## Deployment
node-caldav-server relys on node-gyp, which does not work perfect on Windows

Therefore, *nux is the best deployment platform.

### Config
Open the `conf/config.js`, you can see the following statements
```
module.exports = {
    db:{
        databaseType: 'sqlite',         // database type
        databaseName: 'caldav',         // database name
        databaseFile: 'caldav.db',      // sqlite only,the storage file path
        shouldTruncateAllTables: false, // true will drop the table if it already exists when server is starting
    },
    mountedPath:{
        calDavPath: '/cal',     // the root path for caldav service
        principalPath: '/p',    // the root path for principal service
    }
}
```

Feel free to modify the config

### Deploy
Run the following command

```
npm install
npm start
```

The server is now running at localhost:3000


## Usage
### CalDav URL
>localhost:3000/cal/:user_name/:calendar_name

please replace the `:user_name` with your own name first.

Then, replace the `calendar_name` with a calendar name. If the calendar isn't exists, we will create it.

Therefore, the URL example can be: 
>localhost:3000/cal/demo/demo

Finally, you will be asked to provide an account with password to login node-caldav-server.

Don't worry about the account, if it isn't exists, we will create it, too.


### CalDav client
node-caldav-server is still in developing.

After developing, we will test every CalDav client listed here.

It won't be long, which we think is less than a month   

### Client Being tested
- [x] Mozilla Lightning
- [x] SOL Calendar
- [x] aCalendar+
- [x] DAVdroid
- [x] CalendarSync
- [x] CalDav-Sync
- [ ] IPHONE & IPAD Calendars
- [ ] OSX Calendars



### Mozilla Lightning
Mozilla Lightning is a plugin for Mozilla Thunderbird to add the CalDav support

- click on File and New Calendar
- first window:
    - choose a calendar On the Network
- next window:
    - protocol: choose CalDav
    - location: >localhost:3000/cal/:user_name/:calendar_name
    - offline support: disabled
- final window:
    - you can set whatever you want , since settings of final window is only used by Mozzila Lightning rather than CalDav server.

You can now add events and tasks to your calendar. 

### SOL Calendar
SOL Calendar is an wonderful Android app , which focus on Calendar including CalDav

- open Settings
- click on Add an account
- click on Manual entry
- Upcoming window:
    - CalDav Root URL: >localhost:3000/cal/:user_name/:calendar_name
    - ID: your username of account
    - Password: your password of account

You can now add events and tasks to your calendar. 

### aCalendar+
aCalendar+ is an Android application but can't add new CalDav server. However it can use exist calendar added by Settings/Account/New Account. 

If the platform can't add a third party CalDav Calendar, you can install SOL Calendar to complete it.

After the calendar being created, aCalendar+ can identify it automatically. Feel free to add events and tasks now

### DAVdroid
DAVdroid is an Android application. 

- press '+' button on the right bottom corner of screen
- choose Login in with URL and user name
    - Base URL : >localhost:3000/cal/:user_name/:calendar_name
        - note that: In DAVdroid, calendar_name MUST NOT have prefix or suffix like 'demo.ics'.
    - User name: your username of account
    - Password: your password of account
    - Preemptive authentication: enabled

Now the Calendar is added. In addition, DAVdroid can add new calendar using the same account.

However, DAVdroid can only add calendar. You need to download OpenTasks to edit the events and tasks of calendar

The syncing process of DAVdroid may report error to you. 
Just ignore it since DAVdroid's request isn't standard.Actually,there is no error in the saving and syncing process

### CalendarSync
CalendarSync is an Android application. 

The CalDav Setting here is a little bit different from other client. Follow these steps:

- click on right-top corner of app
- click on Create new WebiCal
- click on THE GUIDED CALDAV SETUP
- select No, I want to set it up by myself
- Upcoming Window:
    - Server url: >localhost:3000/cal/:user_name/:calendar_name
    - User name: your username of account
    - Password: your password of account
    - Sync only a limited time interval: disabled
    - click on TEST CONNECTION/CONFIGURATION TO CONTINUE
- click on SEARCH AVAILABLE CALENDARS
- click OK
- press on the showing calendar, then click on CONFIGURE SELECTED CALENDARS

CalendarSync can only sync Calendar. It doesn't have ability to edit the events and tasks.

You can add events and tasks using other client, then go back to CalendarSync to sync without errors

### CalDav-Sync
CalDav-Sync is an Android application which can add CalDav calendar. 

- open application
- choose CalDAV
- Upcoming window:
    - Server name or URL: >localhost:3000/cal/:user_name/:calendar_name
    - Username: your username of account
    - Password: your password of account
    - click on next
- choose at least a calendar, then click on NEXT. 
- finally click on FINISH

CalDav-Sync is the same as CalendarSync which doesn't support add/edit/delete events and tasks.

You can add events and tasks using other client.

## License
GPL v3

