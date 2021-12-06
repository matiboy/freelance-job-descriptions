Trader User Interface
=====================

Description
-----------

The job consists in building a user interface (a single HTML page, not an SPA) which will be used for crypto trading. The interface will be displaying few key elements including messages coming from a few backend services (all websocket based), the balances of the exchange accounts as tables and a "set up" area from which the trader can trigger changes in the trade backend services.

The work is 100% frontend and the API interactions will be provided with documentation.

A note on compatibility: The page will be accessed by restricted people who only use Chrome and Edge, latest versions. Compatibility with old browsers is therefore not an issue.

Deliverables
------------

1. all source code which can be built/bundled using a single command: `yarn run build`. The 🚨built code by itself🚨 would **not be accepted as delivery**.
2. a lean dockerfile which installs all necessary dependencies and builds the project, and in a second stage sets up the project to be served as a static site on port 80. This must be achievable with the single command `docker run -p 8888:80 trader-user-interface:latest`.

Technologies
------------

- Source control: Git(hub/lab)
- Package manager: 🟢yarn (non PnP) preferred; alternatively 🟠npm
- Frontend framework: 🟢VueJS 3
    * All code is to be written in 🟢TypeScript
    * Use of single file components is preferred
    * Use of composition API is preferred
    * State management is left your discretion (can be without state management)
    * Certain settings will need to be saved to/loaded from localStorage/browser db.
- Websockets:
    * The interface will connect to 3 websockets. The choice of JS client is up to you, but the connections need to auto reconnect with exponential backoff and upon renewed internet connection
    * The use of ReactiveJS is an option to handle the messages coming from the sockets
    * Description of the sockets is found in ------- separate file
- Styling/CSS: 
    * 🟢Tailwind CSS is preferred. 
    * Alternatives can be considered if this is a blocker. 
    * Alternatives must be CSS frameworks based on SASS or Stylus. 
    * Alternatives can be part of a UI framework such as Vuetify.
- Build: suggestions are welcome but preference would be 🟢Parcel followed by 🟠Webpack. 🟢Vue-CLI (which uses webpack) is an acceptable solution for setting up the project and build.

Requirements
------------

### Page design

We would apprecate if you can suggest a design for the page that will ensure clarity of information. The main components are:

- the list of messages coming from the backends. More information about them below. This is a very important display and needs to be prominent.
- the settings where some values can be adjusted and sent to the backends (e.g. amount to trade at once, etc). Second most important, needs to be easily accessible for editing.
- the balances for the two accounts the trader is currently using. These consist of 7 rows and 3 columns
- statuses box: indicators of the 3 websockets current connection (dis/connected), up to date balances, up to date prices

### Websockets

- All 3 websockets can be connected to immediately. Upon connection or reconnection, an `id` read from the page querystring `trader.html?id=abc` needs to be sent as first message to the websocket: `{"session": "abc"}`. The websocket will respond with the same message. From then, messages will start arriving.
- The connections need to auto reconnect upon disconnection
- The connections need to reconnect when page is back online
- All reconnects should use exponential backoff

#### Trades websocket

This websocket sends messages only (see Messages below).

#### Balances websocket

Balances websocket sends messages (see Messages below).

It also sends balance updates ("type": "balances") in the format:

```json
{
    "accountId": "account identifier",
    "accountName": "human readable name",
    "timestamp": 12333333333,
    "balances": [
        {   
            "currency": "USD", // can also be cryptos e.g. "ETH"
            "amount": "220.45"
        },
        ...
    ]
}
```

*Note that amounts always come as strings.*

#### Trade session websocket

Trade session websocket sends messages (see Messages below).

It also sends status updates ("type": "trading_status" or "book_lastupdate") in the format:

```json
TO BE CONFIRMED
```

It is also necessary to be able to *send updates to* the Trade session WS using a button labeled "Update" (see Trade session form below).
There are two types of updates:

1. `{"type": "tradeOn", "direction": "on or off"}`
2. `{"type": "settings", "settings": {} // and object containing the whole form}`

### User interface

#### Messages

Messages are sent via the 3 websockets that control the backend. The messages are identified by "type": "message" and they come in the format:

```json
{
    "type": "message",
    "category": MESSAGE_CATEGORY,
    "level": MESSAGE_LEVEL,
    "message": "string", // Note this might be HTML
    "details": {"some keys": "value"},
}
```

They will need to be displayed from most recent (top) to less recent. Different levels (SUCCESS, WARNING, INFO, ERROR) need to be identifiable (likely using color and other styles). Different categories should be identifiable via icons. 
They all need to be timestamped using a suitable format (suggestion: HH:mm if same day as now, DD,MMM HH:mm otherwise).

Additionally they need to be kept in localStorage or db within space limitations so that if page is reloaded, messages still appear.

A button allows to "clear" them. If cleared, they should be deleted from localStorage

#### Balances

Balances need to consist of one table per different "accountId" value (see Balances websocket format). The tables are sorted left to right by the human readable name.

The tables need to display a header (Currency | Amount | Last update). The values are updated by the Balances socket messages.

"Last update" needs to be computed by the frontend for each row depending on the last time the "amount" changed for the given currency.

