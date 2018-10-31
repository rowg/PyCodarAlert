# PyCodarAlert

*PyCodarAlert AAAA BBBB CCCC DDDD*

Python program (run on combined server) that finds the latest radial files from each site and emails an alert per site if **_file age > trigger_** hours old. This program only knows if a site hasn't uploaded files to the combined server in the configured interval.

Tested on OS X with Python 2.6. No external dependencies. It should be Python 3 friendly but I don't have a combined server with Python 3 to test it. 

The program will write a small text file in the configured directory (default is ./) for each site that it sends an email about named *XXXX_last_email.txt* where XXXX is the site. The file contains the date and time the e-mail was sent so that the next run of the program won't send another e-mail unless the *email_frequency* interval has been met for that site. This allows the script to be run frequently without a barrage of e-mails coming in. If you know a site is down and don't wish to continue receving e-mails about it, remove it from the command line invocation.

*Call this script periodically with cron.*

**Every 15 minutes example crontab line (to check sites AAAA BBBB CCCC DDDD):**

`00,15,30,45     *       *       *       *       /Users/codar/PyCodarAlert AAAA BBBB CCCC DDDD >/dev/null 2>&1`

### Customization Requirements: ###
You will need to customize this script to fit the setup and needs of your organization. The variables that should be changed are at the top of the script. You may need to make some changes to the code for the e-mail function depending on your org's smtp servers. Configuration information below:

##### E-mail parameters (fill in with your organization's settings) #####

`smtp_server = 'smtp.organization.edu'`

`body_text = 'PyCodarAlert message:\n'` (You should probably leave this as-is)

`sender_name = 'your.name@organization.edu'`

`recipients_list = ['your.name@organization.edu', 'person2@organization.edu', 'person3@organization.edu']`

`email_subject = '[CODAR ALERT] Site:'`(Leave this as-is too)

##### How often (in hours) an email can be sent (so you don't spam yourself) ##### 

`email_frequency = 4`

##### How stale (in hours) a radial file must be to trigger an alert #####

`alert_trigger = 12`

##### Radial files root directory. Script will walk directory tree from here. #####

`radial_root = '/Codar/SeaSonde/Data/RadialSites'`

##### Put 4 character site names here. This can be overridden at runtime. #####

`site_names = ['AAAA', 'BBBB', 'CCCC', 'DDDD', 'EEEE']`(These will **ONLY** be used if **NO** command line sites are invoked)
