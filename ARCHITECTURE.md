<h1>Movie Watchlist</h1>


<h2>C4 Context Diagram:</h2>

<p>C4Context
    title Movie Watchlist App - System Context
    Person(user, "User", "A person who uses the app to manage their movie watchlist.")
    System(movieWatchlistApp, "Movie Watchlist App", "A platform to track, organize, and discover movies and TV shows.")
    System_Ext(tmdbAPI, "TMDb API", "Provides movie data like ratings, trailers, and cast information.")
    System_Ext(firebase, "Firebase", "A backend service for authentication and database management.")
    
    Rel(user, movieWatchlistApp, "Uses")
    Rel(movieWatchlistApp, tmdbAPI, "Fetches movie details")
    Rel(movieWatchlistApp, firebase, "Stores user data and handles authentication")
</p>

[C4 Context Diagram](https://www.mermaidchart.com/raw/0d2b5e87-5197-4b14-8015-a503afbbdaf2?theme=light&version=v0.1&format=svg)
    
<h2>C4 Container Diagram:</h2> 

C4Container
    title Movie Watchlist App - Container Diagram
    System_Boundary(app, "Movie Watchlist App") {
        Container(webApp, "Web Application", "React", "Frontend interface where users interact with the app.")
        Container(api, "API Server", "Node.js", "Handles backend logic, user authentication, and communication with external services.")
        ContainerDb(database, "Firebase Database", "Firebase", "Stores user data, watchlists, and authentication info.")
    }
    System_Ext(tmdbAPI, "TMDb API", "Provides movie data.")
    
    Rel(webApp, api, "Uses API for movie details and watchlist management")
    Rel(api, database, "Reads/Writes user data")
    Rel(api, tmdbAPI, "Fetches movie data")

<h2>C4 Component Diagram: </h2>

C4Component
    title Movie Watchlist App - Component Diagram
    
    Container(webApp, "Web Application", "React", "Frontend interface where users interact with the app.") 
    Container(api, "API Server", "Node.js", "Handles backend logic.") 

    Component(authComponent, "Authentication Component", "React", "Handles user login and registration.")
    Component(watchlistComponent, "Watchlist Component", "React", "Allows users to manage their movie watchlist.")
    Component(movieInfoComponent, "Movie Info Component", "React", "Displays movie details fetched from the backend.")
    
    Rel(authComponent, api, "Sends authentication requests")
    Rel(watchlistComponent, api, "Manages watchlist items")
    Rel(movieInfoComponent, api, "Fetches movie data")

<h2>C4 Deployment Diagram:</h2>

C4Deployment
    title Movie Watchlist App - Deployment Diagram
    
    Node(webServer, "Web Server", "Hosts the React application") {
        Container(webApp, "Web Application", "React", "Frontend interface where users interact with the app.")
    }
    
    Node(appServer, "App Server", "Node.js Backend Server") {
        Container(api, "API Server", "Node.js", "Handles backend logic and communicates with Firebase and TMDb API.")
    }

    Node(firebaseCloud, "Firebase Cloud", "Firebase") {
        Container(database, "Firebase Database", "Firebase", "Stores user data and watchlists.")
    }

    Node(tmdbCloud, "TMDb Cloud", "TMDb API") {
        Container(tmdbAPI, "TMDb API", "TMDb", "Provides movie data including ratings, cast, and trailers.")
    }

    Rel(webApp, api, "Uses API for movie data and watchlist management")
    Rel(api, database, "Reads/Writes data to Firebase")
    Rel(api, tmdbAPI, "Fetches movie data from TMDb")
