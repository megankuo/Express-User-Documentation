Possible project structure. This is not written in stone, MVC and other architecture are often highly opinionated.
```bash
|-- project-name              # Root Directory
    |-- docs/                 # Documentation
    |-- public/               # Publicly Accessible Assets
    |   |-- images/
    |   |-- js/               # Client-side JavaScript
    |   |-- styles/           # CSS Stylesheets   
    |-- src/
    |   |-- app.js            # Application Entry Point
    |   |-- api/
    |   |   |-- controllers/  # Request Managers
    |   |   |-- middleware/   # Intermediary b/w Client Request & Server Response
    |   |   |-- routes/       # API Endpoints (URIs)
    |   |-- config/           # Configuration/Settings Files
    |   |-- db/               # Mock Database or Connection to Database
    |   |-- models/           # Database Models
    |   |-- services/         # Services Layer for Business Logic (Talks to Database)
    |   |-- utils/            # Miscellaneous Helper Functions
    |   |-- views/            # Static Template Files (EJS, Pug, or Mustache)
    |-- test/                 # Test Suite   
    |-- .env                  # Environment Variables
    |-- .eslintignore
    |-- .eslintrc.js          # Linting Rules
    |-- .gitignore            # Files/Directory Git Should Ignore 
    |-- .prettierignore   
    |-- .prettierrc.js        # Code Formatting Rules
    |-- package.json          # Metadata and Package List
    |-- README.md
    |-- server.js             # Application Server 
```