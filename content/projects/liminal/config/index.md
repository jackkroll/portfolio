---
title: "Configuration File"
showDate: false
summary: "Explains how the config file is organized and what setup/corruption protections are in place"
showSummary: True
showReadingTime: False
---

## Main Concepts
The configuration file holds all the important information on setup, however there are protections in place to guide setup and protect against possible errors
___

# Printers

{{< alert "circle-info" >}}
Note the difference in the IP Address bar to determine if it's Octoprint or Prusalink
{{< /alert >}}

### Example of a Mk3 printer
{{< highlight json "linenos=table,hl_lines=2" >}}
"Printer Name": {
        "ipAddress": "http://ipaddr.local",
        "prefix": "PF",
        "apiKey": "ABCDEFGHIJKLMNOPQURSTUVWXYZ12345"
}
{{< /highlight >}}
____
### Example of a Mk4 printer

{{< highlight json "linenos=table,hl_lines=2" >}}
"Printer Name": {
        "Mk4IPAddress": "http://ipaddr.local",
        "prefix": "PF",
        "apiKey": "ABCDEFGHIJKLMNOPQURSTUVWXYZ12345"
    }
{{< /highlight >}}

____
# Student Accounts
{{< highlight json "linenos=table,hl_lines=3 7 11" >}}
"students": {
        "DeveloperName": {
            "hash": "scrypt:32768:8:1$EubZXSjE1SGoJITu$f5f7e8640c6f7a9f2261dba0b3f2f9936558dafcebf9b2e32242733e4025290c46f923ddf43a8524be057ce5d02ab726267b6eeb8ed4c3415197fb138063b0af",
            "role": "developer"
        },
        "ManagerName": {
            "hash": null,
            "role": "manager"
        },
        "StudentName": {
            "hash": null,
            "role": "student"
        }
    }
{{< /highlight >}}

Hash indicates the hash for the users password. If it is `null` it indicates the user is actively resetting their password and it will be set upon next login

You <mark>cannot determine a users password</mark> through the hash, nor can you change a password through the config file as it must be hashed first.

{{< button href="https://www.geeksforgeeks.org/what-is-hashing/" >}}
Learn more about hashing
{{< /button >}}

{{< button href="/projects/liminal/accounts" >}}
Learn more about accounts
{{< /button >}}
___

# Setup
Setup will be run if 1 of the following conditions are met
1. `/ref/config.json` does not exist
2. There are no accounts in `config`
3. There are no printers in `config`

You will be automatically redirected from the home page if you do not have all of those items fulfilled\
\
Additionally you will be unable to setup more root users through setup, however to add additional printers you can access that page again
____
