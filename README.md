# SSHoneypot1
Low interaction ssh honeypot results


## Project
An AWS lightsail based, low interaction ssh honeypot using [pshitt](https://github.com/regit/pshitt).

### Time frame 
Started sample on 4/2/2021, ended on 4/10/2021.  About 8 days.

### Results
Had a total of 9229 login attempts from 101 unique clients.   Captured the source ip, the attempted user-name and password, the software version advertised by the attacking client and other connection details.

Overview of the aggregated results:
![Overview of the aggregated results](https://github.com/jLevere/SSHoneypot1/blob/main/DashboardOverview.jpg)

### Setup
Used a python based pshitt honeypot to log ssh login attempts in json to a text file. Then used a filebeat to scrape the entries in the file, and forwarded them through vpn connection to a graylog stack.  There, the messages were parsed with a json extractor and aggregated in a custom dashboard.


### Observations
It took a few hours before the first login attempts started arriving.  The initial attempts where short and had more targeted credentials.  As the sample time progressed, it started to be hit with a larger number of consecutive attempts, and more attacking clients per day. 
![Attempts by time](https://github.com/jLevere/SSHoneypot1/blob/main/AttemptsOverTime.jpg)
 The credentials also became less specific and more typical of password lists.  The other interesting observation was that the advertised software version of the clients varied less over time.  With more exotic and specific ones like "WinSCP_release5.7.5", leading to more general, with the most popular being "Go".


### Files
Here are some examples of the messages that were collected:

![Here are some examples of the messages that were collected](https://github.com/jLevere/SSHoneypot1/blob/main/ExamplesOfAttemptMessages.jpg)
I have included a csv with the password and credentials that were used in request. [Credentials List](https://github.com/jLevere/SSHoneypot1/blob/main/AttemptedCredentials.csv)

### Analysis

Below are some different graphs of the data collected.
![Some relations of unique values over time](https://github.com/jLevere/SSHoneypot1/blob/main/SomeStats1.jpg)

Additionally, the top attempts by country and city.  These are the top 15 of each, there were 23 different countries in total.
![Countries and cities](https://github.com/jLevere/SSHoneypot1/blob/main/GeoLocationResults.jpg)


### Summary
- If you have something exposed, it will be tested.
