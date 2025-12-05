sequenceDiagram
    participant browser
    participant server

    Note right of browser: User writes a note and clicks Save
    browser->>server: POST /new_note with note content
    activate server
    Note right of server: Server adds the new note to the notes array
    server-->>browser: 302 Redirect to /notes
    deactivate server

    Note right of browser: Browser follows redirect and reloads Notes page
    browser->>server: GET /notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET /main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET /main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    Note right of browser: Browser executes JavaScript code (AJAX) to fetch notes
    browser->>server: GET /data.json
    activate server
    server-->>browser: JSON array with all notes including the new one
    deactivate server

    Note right of browser: Browser renders all notes on the page
