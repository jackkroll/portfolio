---
title: "Map Timer Technical Writeup"
showDate: False
showReadingTime: False
showAuthor: False
---
TLDR:
- Frameworks Utilized: WidgetKit, Vapor, Cloudflare Tunnels
- Core technical challenge: [Client + Server Fusion](#client--server-fusion)

{{< button href="https://github.com/jackkroll/MapTimer" target="_blank" >}} 
{{< icon "github" >}} App Source Code
{{< /button >}}
{{< button href="https://github.com/jackkroll/MapTimerServer" target="_blank" >}}
{{< icon "github" >}} Server Source Code
{{< /button >}}
## Purpose
I wanted to develop a basic client for the Apex Legends map rotation for a few reasons
- Some maps I would rather just not play on
- Maps are available at different times each day
- It felt like a lot of friction to visit a website, having a widget would just be easier
    - The website was often out of date and didn't support the challenging LTM + Takeover system in game
    - **LTM**: A limited time mode, that is in addition to the standard game modes
    - **Takeover**: An LTM that **replaces** a standard mode (eg. Casual, Ranked)

## Client Development
### WidgetKit
Widgets were a natural choice for this application
- Map rotations are predictable (standard rotation of 1.5 hours)
  - WidgetKit is most efficient when you can pre-render Widgets for many hours in advance
- Most desired information can be viewed at a glance
- Allows users to place the information wherever they want
  - Not only on the home screen, but also as an accessory widget on your lockscreen
### Learnings from previous developments
I've been personally leaning on the side of utilizing Apple components when possible which comes from several decisions
- Keeps a consistent iOS design language
  - While for an individual app this may seem pointless, this comes as there have been major shifts in Apples design 
language which mark a significant departure from prior design languages (eg. VisionOS, Apple Intelligence)
    - Adjustments already to TabView on iPadOS, expected upcoming changes in the next OS
  - This keeps the app feeling fresh with minimal UI updates from a developer perspective, while I could
create custom components in relation to a UI trend, it can easily become dated
- Intuitive UI based on Apple R&D, keeps more in line with Human Interface Design Guidelines
- Better support for non-standard display types
  - Landscape, Large Type, Built in support for light/dark modes

## Server Development
This was my first attempt at integrating a self deployed server to keep an app up to date which was really exciting
### Backend Design
Vapor, a swift based back end, felt like a natural choice for this application to keep a similar codebase and avoid 
rewriting massive chunks of code and keeping them precisely inline with every update
### Networking
I opted to host it locally on a Raspberry Pi and route it securely utilizing CloudFlare Tunnels allowing full control on 
my own hardware alongside reducing hosting fees for a small project for fun

## Client + Server Fusion
### Local Caching
For a project like this, it's important to have a balance of both up-to-date information and a reduction in unnecessary network traffic\
There are several approaches I had considered
- Request data every single time
  - **Issues**
    - Higher network usage on both client and server usage
    - Doesn't reasonably allow for low-internet situations or when the server is down
- Request data at a set interval, reducing requests to a set lower amount
  - **Issues**
    - Updates may be made within whatever time period I select
    - No easy way with this method to *force* an update
    - No way to add LTMs with this same architecture
- Provide a "best by" date for data
  - **Issues**
    - Accuracy requires preset expiration dates, which can be absolute guesses
    - No way to add LTMs with this same architecture
    - Cannot guarantee accuracy with the server, but better than before being dynamic
- Hash the data, and store locally
  - **Why I went with this**
    - Slightly reduce network strain
    - You can be 100% sure if the data is or is not accurate
      - If the web request succeeds, you know it is accurate without a doubt
      - Otherwise, you still have data but with the knowledge it may be stale
  - **Issues**
    - You still end up making *a* web request every time data is required

Below is the logic flowchart of how up-to-date map data is fetched
{{< mermaid >}}
graph TB;
A[Request for a schedule]-->B[Attempt to fetch live hash];
B-->C[Failed request]
B-->D[Successfully fetched live hash]
A-->E[Attempt to fetch stored schedules + stored hash];
E-->F[No stored schedule/hash]
E-->G[Successfully fetched stored schedule]
C-->H[RETURN hardcoded schedule]
L-->P[Warn data may be outdated]
G-->L[RETURN stored schedule]
H-->P
F-->H
D-->I[Compare live and stored hash]
G-->I
I-->J[Hashes do not match, storage is stale]
I-->K[Hashes match, storage is accurate]
C-->L
J-->M[Update stored data and hash]
M-->N[RETURN updated data]
K-->O[RETURN stored data]
{{< /mermaid >}}
