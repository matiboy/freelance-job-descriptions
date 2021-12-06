Frontend Developer (VueJS 3)
============================

Description
-----------

We are looking for a frontend developer (VueJS 3) with the skills to use an existing CSS framework (Vuetify, Tailwind etc) to design efficient management pages. Focus is on usability and efficient presentation rather than UI design. The Javascript interactions will require slightly advanced skills. No backend work is required.

The freelancer should be familiar with the technologies below. Most of the work is about designing the page to fit the information and present it in a dynamic and easy to read manner. Basic skills with bundlers (Parcel/webpack) will be needed.

The frontend will interact with a few backend services via websockets. The main components on the page are:

- the list of messages coming from the backends. This is a very important display and needs to be prominent.
- the settings where some values can be adjusted and sent to the backends (e.g. amount to trade at once, etc). Second most important, needs to be easily accessible for editing.
- the balances for the two accounts the trader is currently using. These consist of 7 rows and 3 columns
- statuses box: indicators of the 3 websockets current connection (dis/connected), up to date balances, up to date prices

More work will follow and the developer of this project will be given priority for additional requirements.

Deliverables
------------

For all jobs, deliverables will come in the form of source code (Typescript, .vue, SASS), which need to be easily built/bundled.The 🚨built code by itself🚨 would **not be accepted as delivery**.

Technologies
------------

- Source control: Git(hub/lab)
- Package manager: yarn (non PnP) preferred; alternatively 🟠npm
- Frontend framework: VueJS 3 written in TypeScript
- Websockets. The choice of JS client is up to you, but the connections need to auto reconnect. The use of ReactiveJS is an option to handle the messages coming from the sockets
- Styling/CSS: Tailwind CSS is preferred or CSS frameworks based on SASS or Stylus (e.g. Vuetify)
- Build: suggestions are welcome but preference would be Parcel followed by 🟠Webpack. 🟢Vue-CLI (which uses webpack) is an acceptable solution for setting up the project and build.
- Ability to bundle everything into a lean Docker container would be a plus
