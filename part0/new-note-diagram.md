```mermaid
sequenceDiagram
    participant browser
    participant server

    Note right of browser: User types a new note into the text field
    Note right of browser: User clicks the "Save" button (submits the form)

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note\n(Form data: note=<user text>)
    activate server
    Note right of server: Server stores the new note (e.g., in memory / database)
    server-->>browser: 302 Redirect (Location: /exampleapp/notes)
    deactivate server

    Note right of browser: Browser follows the redirect and reloads the Notes page

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    Note right of browser: Browser executes JS, which fetches updated notes as JSON

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: Updated notes list (includes the new note)
    deactivate server

    Note right of browser: Browser renders the notes list, now showing the new note
