# Smart India Hackathon Workshop
# Date: 18/09/2026
## Register Number: 212225220120
## Name: Vishal S
## Problem Title
SIH 1710: Enhancing Navigation for Railway Station Facilities and Locations
## Problem Description
Background: Railway stations are complex environments with numerous facilities and locations such as ticket counters, platforms, restrooms, food courts, and waiting areas. Passengers often face difficulties in navigating these spaces, especially in large or unfamiliar stations. Efficient and user-friendly navigation systems are crucial for improving passenger experience, reducing congestion, and ensuring timely travel connections. Description: The problem involves developing a comprehensive navigation solution for railway stations that assists passengers in locating various facilities and destinations within the station premises. This includes creating detailed maps, providing real-time directions, and integrating features such as accessibility options for individuals with disabilities. The solution should be intuitive, easy to use, and accessible via multiple platforms, including mobile devices and digital kiosks. Key challenges include updating navigation information in real-time, ensuring accuracy, and accommodating the diverse needs of all passengers. Expected Solution: The expected solution is a multi-platform navigation system that provides detailed, real-time directions to all facilities and locations within a railway station. This system should include: A mobile application with 3D interactive maps and step-by-step navigation. Digital kiosks located throughout the station with touch-screen interfaces. Voice-guided navigation for visually impaired passengers. Regular updates to reflect changes in station layout and facility locations. Integration with existing railway apps and services for seamless user experience. The solution should enhance the overall passenger experience by reducing confusion, saving time, and improving accessibility within the station.

## Problem Creater's Organization
Ministry of Railway

#Idea
A highly effective, low-cost alternative to custom 3D apps and specialized hardware is a "Scan & Go" Progressive Web App (PWA) paired with smart physical wayfinding. By placing high-visibility QR codes on pillars throughout the station, passengers can instantly open a lightweight web map via their smartphone camera without downloading any applications, instantly anchoring their starting location without complex indoor GPS. This digital layer is seamlessly reinforced by physical color-coded floor decals—such as a blue line for platforms and a red line for exits—allowing users to follow simple directions even if their phone battery dies. For accessibility, low-cost Bluetooth Low Energy (BLE) beacons broadcast location tags that trigger audio navigation cues through the native screen readers already built into visually impaired passengers' smartphones. Finally, instead of expensive custom hardware, heavy-duty commercial tablets locked in "Kiosk Mode" run the exact same web app across the station, ensuring real-time synchronization across all devices whenever a facility's location is updated.


## Proposed Solution / Architecture Diagram
                        [ STATION ADMIN PORTAL ]
                                  |
                                  v (Updates POIs & Layout)
                        +----------------------+
                        |   CENTRAL DATABASE   |
                        | - Station Map Data   |
                        | - QR Anchor IDs      |
                        | - Facility Locations |
                        +----------------------+
                                  |
                                  v
                        +----------------------+
                        |    CLOUD BACKEND     |
                        | - API Gateway        |
                        | - Routing Engine     |
                        +----------------------+
                                  |
               +------------------+------------------+
               |                  |                  |
               v                  v                  v
    +--------------------+ +-------------+ +--------------------+
    | PWA FRONTEND (Web) | | BLE NETWORK | | PWA FRONTEND (Web) |
    +--------------------+ +-------------+ +--------------------+
               ^                  |                  ^
               |                  v                  |
               |         (Bluetooth Signal)          |
               |                  |                  |
        (HTTP Request)            |             (HTTP Request)
               |                  v                  |
    +--------------------+ +-------------+ +--------------------+
    | PASSENGER'S PHONE  | | ACCESSIBILITY| | STATION KIOSK      |
    | (Mobile Browser)   | | SCREEN READER| | (Commercial Tablet)|
    +--------------------+ +-------------+ +--------------------+
               ^                  ^                  ^
               |                  |                  |
           (Scans)           (Triggers)           (Touches)
               |                  |                  |
    +--------------------+ +-------------+ +--------------------+
    | PHYSICAL QR CODES  | | BLE BEACONS | | KIOSK ENCLOSURE    |
    | (Pillars & Walls)  | | (Corridors) | | (Station Entrance) |
    +--------------------+ +-------------+ +--------------------+


## Use Cases
Imagine a stressed, first-time passenger arriving at a sprawling, crowded railway station with only ten minutes to find a connecting train at a distant platform. Instead of wasting precious minutes searching for an information desk or waiting to download a heavy navigation app, they simply scan a highly visible "Scan for Directions" QR code on a nearby pillar. Their smartphone instantly opens a fast-loading web map that already knows their exact starting point and calculates the fastest route to Platform 9. The screen instructs them to simply "Follow the Green Line," allowing the passenger to put their phone away and quickly follow the physical green decals painted on the floor through the crowd, seamlessly guiding them to their train with time to spare.


## Technology Stack
The Progressive Web App (PWA) backend leverages Node.js with Express.js (or Python's FastAPI) connected to a PostgreSQL database running the PostGIS extension to handle spatial data, station layouts, and real-time Dijkstra or A* shortest-path routing algorithms. On the frontend, lightweight frameworks like React.js or Vue.js paired with Mapbox GL JS or Leaflet.js render fast, interactive 2D isometric maps directly in the passenger's mobile browser, with Workbox enabling offline caching. The physical-to-digital layer uses standard URL-encoded QR codes for static positioning, Bluetooth Low Energy (BLE) beacons utilizing the Web Bluetooth API to trigger native smartphone screen readers (VoiceOver/TalkBack) for audio navigation, and Google Firebase (or WebSocket connections) to push real-time station updates instantly to mobile web apps and kiosk-mode tablets.


## Dependencies
The solution's dependency ecosystem spans the frontend, backend, routing, and hardware integration layers. On the frontend, core rendering relies on React or Vue, while spatial map visualization and offline Progressive Web App caching are driven by Mapbox GL JS (or Leaflet) and Workbox. The backend server is built using Express.js (or FastAPI), utilizing drivers like pg or Sequelize for database connectivity, alongside cors for cross-origin security and dotenv for environment management. Spatial route calculations rely on the pgRouting extension for PostgreSQL alongside client-side geospatial analysis tools like @turf/turf. Real-time layout updates across kiosks and user devices are handled via Firebase Admin or Socket.io, while hardware interactions leverage native browser APIs—such as the Web Bluetooth API for BLE beacon detection—without requiring external third-party physical libraries.
