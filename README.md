# SSHoneypot1
Low interaction ssh honeypot results


## Project
AWS lightsail based low interaction [pshitt](https://github.com/regit/pshitt) ssh honeypot  project.

### Time frame 
Started sample on 4/2/2021, ended on 4/10/2021.

### Results
Had a total of 9229 login attempts from 101 unique clients.   Captured the source ip, the attempted user-name and password, the software version advertised by the attacking client and other connection details.

Overview of the aggregated results:
![Overview of the aggregated results](https://github.com/jLevere/SSHoneypot1/blob/main/DashboardOverview.jpg)

### Setup
Used python based pshitt honeypot to log the requests ssh login attempts in json to text file. Then used filebeat to scrape the entries in the file as they were written and forwarded them through vpn connection to graylog stack, where I parsed the messages with a json extractor and aggregated them in custom dashboard.


### Observations
It took a few hours before the first login attempts started arriving.  The initial attempts where short and had more targeted credentials that appeared to be defaults for things.  As the sample time progressed it started to be hit with larger and larger numbers of consecutive attempts and more and more attacking clients per day.  The credentials also became less specific and more typical of password lists.  The other interesting observation was that the advertised software version of the clients varied less over time.  With more exotic and specific ones like WinSCP_release5.7.5, leading to more general like just plain "Go".


### Files
Here are some examples of the messages that were collected:

![Here are some examples of the messages that were collected](https://github.com/jLevere/SSHoneypot1/blob/main/ExamplesOfAttemptMessages.jpg)
I have included a csv with the password and credentials that were used in request. [Credentials List](https://github.com/jLevere/SSHoneypot1/blob/main/AttemptedCredentials.csv)

### Analysis

Below are some different graphs of the data collected.
![Some relations of unique values over time](https://github.com/jLevere/SSHoneypot1/blob/main/SomeStats1.jpg)

### Summary
If you have something exposed, know it will be tested.

- I would like to go back and add geographic information in at some point.  I had issues with bugs in graylogs web interface when attempting to configure processing pipelines to do this.