Trader User Interface
---------------------

Description
===========

The job consists in building a user interface (a single HTML page, not an SPA) which will be used for crypto trading. The interface will be displaying few key elements including messages coming from a few backend services (all websocket based), the balances of the exchange accounts as tables and a "set up" area from which the trader can trigger changes in the trade backend services.

The work is 100% frontend and the API interactions will be provided with documentation.

A note on compatibility: The page will be accessed by restricted people who only use Chrome and Edge, latest versions. Compatibility with old browsers is therefore not an issue.

Deliverables
============

1. all source code which can be built/bundled using a single command: `yarn run build`. The 🚨built code by itself🚨 would **not be accepted as delivery**.
2. a lean dockerfile which installs all necessary dependencies and builds the project, and in a second stage sets up the project to be served as a static site on port 80. This must be achievable with the single command `docker run -p 8888:80 trader-user-interface:latest`.

Technologies
============

- Source control: Git(hub/lab)
- Package manager: 🟢yarn (non PnP) preferred; alternatively 🟠npm
- Frontend framework: 🟢VueJS 3
    * All code is to be written in 🟢TypeScript
    * Use of single file components is preferred
    * Use of composition API is preferred
    * State management is left to the freelancer's discretion (can be without state management)
    * Certain settings will need to be saved to/loaded from localStorage.
- Websockets:
    * The interface will connect to 3 websockets. The choice of JS client is up to you, but the connections need to be reconnectable with exponential backoff
    * The use of ReactiveJS is an option to handle the messages coming from the sockets
    * Description of the sockets is found in ------- separate file
- Styling/CSS: 
    * 🟢Tailwind CSS is preferred. 
    * Alternatives can be considered if this is a blocker. 
    * Alternatives must be CSS frameworks based on SASS or Stylus. 
    * Alternatives can be part of a UI framework such as Vuetify.
- Build: suggestions are welcome but preference would be 🟢Parcel followed by 🟠Webpack. 🟢Vue-CLI (which uses webpack) is an acceptable solution for setting up the project and build.

Requirements
============

### Page design

We would apprecate if you can suggest a design for the page that will ensure clarity of information. The 3 main components are:

- the list of messages coming from the backends. More information about them below.
- the settings where some values can be adjusted and sent to the backends (e.g. amount to trade at once, etc)
- the balances for the two accounts the trader is currently using. These consist of 1 FIAT and 5 coins

### Messages

Messages are sent to the 3 websockets that control the 