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


#
