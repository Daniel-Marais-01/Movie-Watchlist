<h1>Movie Watchlist</h1>



C4Context
  title System Context diagram for Movie Watchlist App
  Enterprise_Boundary(b0, "Movie Watchlist App Boundary") {
    Person(user, "User", "A user who wants to organize, track, and discover movies and TV shows.")
    
    System(movieApp, "Movie Watchlist App", "A platform where users can organize, track, and discover movies and TV shows across different streaming services.")
    
    Enterprise_Boundary(b1, "Backend Services") {
      SystemDb_Ext(firestore, "Firebase", "Handles user authentication and stores user data (e.g., watchlist).")
      System(tmdbAPI, "TMDb API", "Provides movie data like ratings, trailers, and cast.")
      System(imdbAPI, "IMDb API", "Provides additional movie details.")
    }
  }

  BiRel(user, movieApp, "Uses")
  BiRel(movieApp, firestore, "Uses for storing user data")
  Rel(movieApp, tmdbAPI, "Fetches movie data", "REST API")
  Rel(movieApp, imdbAPI, "Fetches additional movie data", "REST API")

  UpdateElementStyle(user, $fontColor="blue", $bgColor="yellow", $borderColor="green")
  UpdateRelStyle(user, movieApp, $textColor="blue", $lineColor="blue", $offsetX="10")
  UpdateRelStyle(movieApp, firestore, $textColor="green", $lineColor="green", $offsetY="-10")
  UpdateRelStyle(movieApp, tmdbAPI, $textColor="red", $lineColor="red", $offsetY="-20")
  UpdateRelStyle(movieApp, imdbAPI, $textColor="purple", $lineColor="purple", $offsetY="-30")

  UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")****
