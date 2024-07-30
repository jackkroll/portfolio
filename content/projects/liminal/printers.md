---
title: "Printers"
showDate: false
summary: "Details printer objects based on Octoprint (Mk3s) and Prusalink (Mk4) printer architecture"
showSummary: True
showReadingTime: False
---
## Main concepts
These two objects are two distinct objects interacting with two seperate APIs (Octoprint & PrusaLink) but are used together as that is what Team 302 has
____
# SinglePrinter
For printers running off of Octoprint API
## Variables

### Type <kbd>String</kbd>
- Static as "MK3"

### Nickname <kbd>String</kbd>
- Given nickname to the printer

### Code <kbd>String</kbd>
- Given 2 letter code given to printer (used in database)

### State <kbd>String</kbd>
- Current state of the printer
{{< badge >}}
Note: This has a partial implementation, recomended to reference octoprint state due to lack of updates
{{< /badge >}}

### Printer <kbd>Octoprint Printer Object</kbd>
- Used for core functions sending commands directly to the printer
{{< alert >}}
The below items are not currently implemented with full functionality
{{< /alert >}}

### User <kbd>String</kbd>
- Current user printing

### Current File <kbd>String</kbd>
- Current file printing

### Queue <kbd>[Queue Object]</kbd>
- List of objects in queue to print

____

## Methods

### Pause
- Sends a command to pause the print

### Resume
- Sends a command to resume the print

### UpdateState
- Updates the state property of the object

### Preheat
- Preheats nozzle to 120ºC and bed to 60ºC (PLA)

### Cooldown
- Sets targets to 0 (cooldown)

### UploadLocal(<kbd>File path : String</kbd>, <kbd> File name : String</kbd>, <kbd>Uploader : String</kbd>)
- Only used during local testing and uploads files on the server to the printer

### DisplayMSG(<kbd>Message : String</kbd>)
- Displays a message on the LCD displays on the printer using M117 GCODE

### Upload(<kbd>Print : IndividualPrint</kbd>, <kbd>PrintImmedietly : Bool</kbd>)
- Printing immedietly isn't mandatory and is assumed as true
- Takes file contents from print object and uploads them to the printer
- If it is to print immedietly, it selects it and sets current file and current user

### Abort
- Attempts to cancel the currently printing object 
### FetchNozzleTemp
- Returns the nozzle temperatue <kbd>Int</kbd>
### FetchBedTemp
- Returns the bed temperature <kbd>Int</kbd>
### FetchTimeRemaining
- Returns the time remaining in a print in seconds <kbd>Int</kbd>
- If there is no time left, it returns -60 (-1 minute) <kbd>Int</kbd>
    {{< badge >}}
    This can occasionally show up at the end of a print where Octoprint puts the state as printing, but does not return any time remaining
    {{< /badge >}}
### Scheduler
- Not used, old plans for an individual printer to optimize it's print queue
### PercentUsed
- Returns the percent used <kbd>Int</kbd> (0-100)
### NukeFiles
- Not currently accessible through web
- Operation used to remove all files saved on Octoprint to free up storage space on each invidual printers computer

____
# Mk4Printer

## Variables
{{< badge >}}
    This was developed much later and now most values can be None until refreshed or updated, if it can be None, is designated with a ? at the end
{{< /badge >}}
### Type <kbd>String</kbd>
- Static value returning "MK4"

### Nozzle Temp <kbd>Int?</kbd>
- Returns stored nozzle temp in ºC

### Bed Temp <kbd>Int?</kbd>
- Returns stored bed temp in ºC

### State <kbd>String?</kbd>
- Returns stored state, refer to [PrusaLink API](https://github.com/prusa3d/Prusa-Link-Web/blob/master/spec/openapi.yaml#L1269)

### CurrentPrintID <kbd>String?</kbd>
- PrusaLink determined ID of the current job

### Progress <kbd>Int?</kbd> (0-100)
- Current stored progress of transfer

{{< alert >}}
The above items aren't automatically updated when fetched, please use refreshData to get the most accurate information
{{< /alert >}}

### IP <kbd>String</kbd>
- The IP address of the given printer to connect to PrusaLink with

### PortStr <kbd>String?</kbd>
- Serial port on which to attempt a connection
{{< alert >}}
Serial support was fully implemented and tested (On Mk3) however, at the time of writing, 7/29/2024, serial connections are not supported on the Prusa Mk4
{{< /alert >}}

### Key <kbd>String</kbd>
- API Key to be used with PrusaLink

### Prefix <kbd>String</kbd>
- Two charachter prefix defined in config

### Nickname <kbd>String</kbd>
- Given nickname for the printer

### Transfer <kbd>Int?</kbd> (0-100)
- Current transfer progress
____
## Methods

### CMD(<kbd>Command : String</kbd>)
- Sends a command over serial

### Preheat(<kbd>Type : String (Both, Bed, Nozzle)</kbd>)
- Sends serial command to preheat the bed and/or nozzle

### Cooldown(<kbd>Type : String (Both, Bed, Nozzle)</kbd>)
- Sends serial command to cool the bed and/or nozzle

### ReturnHome
- Sends serial command to return the bed to the home position

{{< alert >}}
The above commands are implemented and tested (On Mk3), however at the time of writing, 7/29/2024, serial connections are not supported on the Prusa Mk4
{{< /alert >}}


### Abort
- Sends a serial command to abort if available
- Sends a PrusaLink command to stop

### RefreshData
- Refreshes all data setting them to none if data isn't available

### CheckUpdate
- Checks if the system or PrusaLink can be updated

### PushUpdate(<kbd>Type : String (System, PrusaLink)</kbd>)
- Pushes update to the system or prusalink

### FetchNozzleTemp
- Refreshes data and returns nozzle temp

### FetchBedTemp
- Refreshes data and returns bed temp

### Upload(<kbd>File Text : String</kbd>, <kbd>Nickname : String</kbd>, <kbd>BGCODE : Bool</kbd>, <kbd>PrintRightAway : Bool</kbd>)
- Sets path based off of nickname and BGCODE status
- Sets upload state based on printRightAway
- Sends request to Mk4

### PrintFileOnUSB(<kbd>Nickname : String</kbd>, <kbd>BGCODE : Bool</kbd>, <kbd>Storage : String</kbd>)
- Selects print on USB to print

### TransferStatus
- Refreshes data and sends transfer status (0-100)

### Stop
- Sends request to stop current print job

### Pause
- Sends request to pause current print job

### Resume
- Sends request to pause current print job

### State
- Refreshes data and sends current state, refer to [PrusaLink API](https://github.com/prusa3d/Prusa-Link-Web/blob/master/spec/openapi.yaml#L1269)