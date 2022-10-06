# Chapter 2

## Day 4

#### 1.Deploy a new contract that has a Struct of your choosing inside of it (must be different than Profile).

#### 2.Create a dictionary or array that contains the Struct you defined.

#### 3.Create a function to add to that array/dictionary.

```
pub contract MovieRating {

    pub var filmData: {String: MovieData}

    pub struct MovieData {
        pub let movieName : String
        pub let genre  : String
        pub let rating  : UFix64

        init(_movieName: String, _genre: String, _rating: UFix64) {
            self.movieName = _movieName
            self.genre = _genre
            self.rating = _rating
        }
    }

    pub fun addMovieData(movieName: String, genre: String, rating: UFix64) {
        let newMovieData = MovieData(_movieName : movieName, _genre : genre, _rating : rating)
        self.filmData[movieName] = newMovieData
    }


    init() {
        self.filmData = {}
    }
}


```

#### 4.Add a transaction to call that function in step 3.

```

import MovieRating from 0x01

transaction(movieName: String, genre: String, rating: UFix64) {

    prepare(signer: AuthAccount) {}

    execute {
        MovieRating.addMovieData(movieName: movieName, genre: genre, rating: rating)
        log("We're done.")
    }
}
```

#### 5.Add a script to read the Struct you defined.

```
import MovieRating from 0x01

pub fun main(movieData: String): MovieRating.MovieData {
    return MovieRating.filmData[movieData]!

}

```
