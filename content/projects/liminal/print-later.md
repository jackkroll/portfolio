---
title: "PrintLater"
showDate: false
summary: "Provides an overview and technical recap of the PrintLater function"
showSummary: True
showDescription: True
showReadingTime: False
---
### Main Concepts
- PrintLater Object
- Liminal scheduled print list
- Print Watcher background task

PrintLater objects are added to the schedule, and then monitored by PrintWatcher to be executed in the background
____
# PrintLater
## Variables

### Time <kbd>Date</kbd>
- Time to execute print

### FileContents <kbd>String</kbd>
- String of file contents to execute (stored in memory)

### Printer <kbd>Printer</kbd>
- Printer object to print on

### BGCODE <kbd>Bool</kbd>
- If the file is a BGCODE or not

### Preheating <kbd>Bool</kbd>
- If the printer is currently preheating due to being ready to print
____
## Methods
### Preheat
1. It will fetch the printer type
   1. If Mk3 or has serial connection
        1. Will preheat printer through appropriate method
        2. If printer is Mk3, will display message on display
        {{< badge >}}
        Developer note: As of writing, 7/29/2024, the Mk4 cannot display messages on the LCD through the API
        {{< /badge >}}
   2. Can't preheat but will acknowledge it tried

### Ready2Print
1. Determines the printer type
    1. Mk4 (PrusaLink)
        1. Get current state, check if printing (or paused printing)
        2. Prints the file already uploaded to USB
        {{< badge >}}
        Developer note: The reason why Mk4 has additional logic is due to Mk4 file uploads historically taking a long time, this was fixed in a later patch
        {{< /badge >}}
    2. Mk3 (Octoprint)
        
    
   {{< alert >}}
   In the event of any of any of these failing, it will stand down and cooldown
   {{< /alert >}}
____
# Liminal Scheduled Print List <kbd>[PrintLater]</kbd>
- List on the main class of objects to print later
____
# PrintWatcher
- Threaded background process
- Fetches current time
- Cycles through every scheduled print
    - If 5 minutes before, call preheat method
    - If current time, call ready2print & remove from scheduled prints
- Sleeps for 10 seconds
____
# Website Appearance
## Main Page <kbd>GET</kbd>
Togglable through button on the top, adding a flag to the page, when toggled it modifies the page adding a date picker
## /printLater <kbd>POST</kbd>
1. Determines which printer to print on based off of user form
    - Cycles through printers, if user selected printer doesn't exist it safely exits and returns an error
2. Goes through attached print data and creates a PrintLater object
3. Adds PrintLater object to Liminal scheduled prints list