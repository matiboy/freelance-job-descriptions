Trader User Interface
---------------------

Description
===========

The job consists in building a user interface (a single HTML page) which will be used for crypto trading. The interface will be displaying few elements including messages coming from a few backend services (all websocket based), the balances of the exchange accounts as tables and a "set up" area from which the trader can trigger changes in the trade backend services.

The work is 100% frontend and the API interactions will be provided with documentation.

Deliverables
============

1. all source code which can be built/bundled using a single command: `yarn run build`. The built code by itself would not be accepted as delivery.
2. a lean dockerfile which installs all necessary dependencies and builds the project, and in a second stage sets up the project to be served as a static site on port 80. This must be achievable with the single command `docker run -p 8888:80 trader-user-interface:latest`.

Technologies
============

- Source control: Git(hub/lab)
- Package manager: yarn (non PnP) preferred; alternatively npm
- Frontend framework: VueJS 3
    * All code is to be written in TypeScript
    * Use of single file components is preferred
    * Use of composition API is preferred
    * State management is left to the freelancer's discretion (can be no state management)
    * Certain settings will need to be saved to/loaded from localStorage.
- Websockets:
    * The interface will connect to 3 websockets. The choice of JS client is up to you, but the connections need to be reconnectable with exponential backoff
    * The use of ReactiveJS is an option to handle the messages coming from the sockets
    * Description of the sockets is found in ------- separate file
- Styling/CSS: Tailwind CSS is preferred. Alternatives can be considered if this is a blocker. Alternatives must be CSS frameworks based on SASS or Stylus
- Build: suggestions are welcome but preference would be Parcel followed by Webpack. Vue-CLI (which uses webpack) is an acceptable solution for 

Requirements
============

### Page design

You are expected to suggest a design for the page that will ensure clarity of information. The 3 main components are:

- the list of messages coming from the backends. More information about the 