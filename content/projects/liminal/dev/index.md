---
title: "I want to help..."
showDate: false
summary: "Detailing who, why, and how you should contibute"
showSummary: True
showReadingTime: False
---
## Is development for me?
In my opinion, yes, **but** I recomend you have some prior experience or be ready to learn. Things that you will have to know to properly submit an addition
- Git + GitHub
- Python
- Using Linux
- Navigating command prompts
- Patience

## What should be added?
The purpose of this is to provide an easier time managing a large amount of printers, not to implement deep interactions on a single printer.\
I encourage you to consider the following before embarking on this adventure
1. Is this an addition that would be used often enough or have significant benefits
2. Is this feature reasonably applicible to all of the printers, leveraging the point of this system

## Why isn't X feature already implemented?
To be quite honest with you, it boils down to one of a few reasons
- I didn't have enough time before moving off to college
- I wasn't smart enough as you to consider that idea
- It didn't (at the time) apply to the reasons listed to above

## What features could be added in the future?
I haven't been able to get to a few things and some suggestions I have would be
- Database redo to utilize SQL instead of Firebase
- Reservation system to allow users to keep a 5 minute reservation on a printer if they need to use it
- Further investigation on serial printing for Mk4
{{< badge >}}
This would likely be after an update that releases serial commands either via api or unlocks the serial port on the printer
{{< /badge >}}

{{< alert "lightbulb">}}
With the release of the Prusa MK4s, it's possible the serial ports are enabled, but you can also get a plethora of information through the [**"hackerboard"**](https://www.prusa3d.com/product/gpio-set/) and with minimal code **can be added seamlessly to LMNL**
{{< /alert >}}
\
{{< button href="/projects/liminal/first-time" >}}
Don't know how to start? Click here
{{< /button >}}

## How should I go about contributing?
As long as you've considered all and are ready to embark, clone the [repo](https://github.com/AmazingSupDawg/Liminal).
For this I encourage you to have a similar setup to test on at home, or getting a dedicated time to test.

### I am testing on the actual hardware
I personally recomend you create a seperate folder that won't interfere with the live repository.
- You'll need to assign to a different port as the current server will be running on port `8000`, for information on ports visit [here](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)
- To start, run `dashboard.py`

### I have questions/I need help...
Fun fact this is my portfolio website so it should have the most up to date information on where to contact me! But you can email me at [me@jackk.dev](mailto:me@jackk.dev) **No promises I know everything,but I will get back to you ASAP :)**

### I almost forgot, I need to document my changes!
I absolutely put off making this documentation but it's incredibly important! Please make a pull request on [this repository](https://github.com/AmazingSupDawg/portfolio) if you need to update or add documentation and I would be happy to read over and review it <3

### I'm ready to submit my changes!
Submit a pull request on [GitHub](https://github.com/AmazingSupDawg/Liminal) with details on exactly what you did (link your new documentation :D) and confirm that you actually tested it

### I don't have permission to...
Username: `jack`\
Password: `n0tami$hchr1$`
