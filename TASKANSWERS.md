# Full-Stack-part0
# part 0 work about sequence diagrams

# 0.4 Creating a similar diagram depicting the situation where the user creates a new note on the page:

    
    sequenceDiagram
    
    participant user #lightblue
    participant browser #lightpink
    participant server #lightgreen

    Note over user,browser: User writes a note and clicks Save

    user-[#red]>>browser: Enter note text 
    user-[#red]>>browser: Click Save

    browser-[#red]>>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    Note right of browser: Form data is sent in the request body

    activate server
    Note right of server: Server adds the note to the notes array
    server-[#darkblue]->>browser: HTTP 302 Redirect, Location: https://studies.cs.helsinki.fi/exampleapp/notes
    deactivate server

    browser-[#red]>>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-[#darkblue]->>browser: HTML document
    deactivate server

    browser-[#red]>>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-[#darkblue]->>browser: CSS file
    deactivate server

    browser-[#red]>>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-[#darkblue]->>browser: JavaScript file
    deactivate server

    Note right of browser: Browser executes main.js, which fetches the notes as JSON

    browser-[#red]>>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-[#darkblue]->>browser: JSON data containing the notes
    deactivate server

    Note right of browser: Browser renders the notes using the DOM API

In simple, flow is like this::

User enters note → Clicks Save → POST note → Server saves note → 302 Redirect → GET page → Load CSS → Load JavaScript → GET notes JSON → Render notes

0.4: Save note → reload


# 0.5 Creating a diagram depicting the situation where the user goes to the single-page app version of the notes app


     sequenceDiagram
     
     participant user #lightblue
     participant browser #lightpink
     participant server #lightgreen
     
    user-[#red]>>browser: Naviagtes & Open https://studies.cs.helsinki.fi/exampleapp/spa
    
    browser-[#red]>>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-[#darkblue]->>browser: HTML document
    deactivate server
    
    browser-[#red]>>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-[#darkblue]->>browser: CSS file
    deactivate server
    
    browser-[#red]>>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-[#darkblue]->>browser: JavaScript file
    deactivate server
    
    Note right of browser: Browser executes spa.js
    
    browser-[#red]>>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-[#darkblue]->>browser: JSON data containing the notes
    deactivate server
    
    Note right of browser: JavaScript renders the notes using the DOM API
    
In simple, flow is like this::

User opens SPA → GET SPA page → Load CSS → Load SPA JavaScript → JavaScript requests notes → Render notes


0.5: Open SPA → load everything


# 0.6 Creating a diagram depicting the situation where the user goes to the single-page app version of the notes app

    sequenceDiagram
 
    participant user #lightblue
    participant browser #lightpink
    participant server #lightgreen

    Note over user,browser: The SPA page is already open

     user-[#red]>>browser: Enter note text
     user-[#red]>>browser: Click Save

    Note right of browser: JavaScript prevents the default form submission<br/>using e.preventDefault()

    Note right of browser: JavaScript creates a note with content and date
    Note right of browser: JavaScript adds the note to the local notes array
    Note right of browser: JavaScript clears the text field
    Note right of browser: JavaScript redraws the notes on the page

    browser-[#red]>>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    Note right of browser: JSON body: { content, date }<br/>Content-Type: application/json

    activate server
    Note right of server: Server stores the new note
    server-[#darkblue]->>browser: HTTP 201 Created
    deactivate server

    Note right of browser: Browser remains on the same page<br/>No redirect or page reload occurs

 In simple, flow is like this::
 
 User action → JavaScript handles it → local UI update → POST JSON → server stores note → 201 Created → same page


0.6: Save note in SPA → no reload
