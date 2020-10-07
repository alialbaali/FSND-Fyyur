Fyyur
-----

### Introduction

Fyyur is a musical venue and artist booking site that facilitates the discovery and bookings of shows between local performing artists and venues. This site lets you list new artists and venues, discover them, and list shows with artists as a venue owner.

### Dependencies

Dependencies are listed in the `requirements.txt` file. 
Run `pip3 install -r requirements.txt` to install them.


### Features

* Creating new venues, artists, and creating new shows.
* Searching for venues and artists.
* Learning more about a specific artist or venue.


### Tech Stack

* SQLAlchemy ORM
* PostgreSQL
* Python3 and Flask
* Flask-Migrate
* HTML, CSS, and Javascript with [Bootstrap 3](https://getbootstrap.com/docs/3.4/customize/) for the website's frontend

### Main Files: Project Structure

  ```sh
  ├── README.md
  ├── app.py *** the main driver of the app. Includes SQLAlchemy models.
                    "python app.py" to run after installing dependences
  ├── config.py *** Database URLs, CSRF generation, etc
  ├── error.log
  ├── forms.py *** forms used to create new artists, shows, and venues.
  ├── requirements.txt *** The dependencies which can be installed like this "pip3 install -r requirements.txt"
  ├── static
  │   ├── css 
  │   ├── font
  │   ├── ico
  │   ├── img
  │   └── js
  └── templates
      ├── errors
      ├── forms
      ├── layouts
      └── pages
  ```

Overall:
* Models are located in the `MODELS` section of `app.py`.
* Controllers are also located in `app.py`.
* The web frontend is located in `templates/`, which builds static assets deployed to the web server at `static/`.
* Web forms for creating data are located in `form.py`


Highlight folders:
* `templates/pages` -- Defines the pages that are rendered to the site. These templates render views based on data passed into the template’s view, in the controllers defined in `app.py`. These pages successfully represent the data to the user.
* `templates/layouts` -- Defines the layout that a page can be contained in to define footer and header code for a given page.
* `templates/forms` -- Defines the forms used to create new artists, shows, and venues.
* `app.py` -- Defines routes that match the user’s URL, and controllers which handle data and renders views to the user. This is the main file which connects to and manipulates the database and render views with data to the user, based on the URL.
* Models in `app.py` -- Defines the data models that set up the database tables.
* `config.py` -- Stores configuration variables and instructions, separate from the main application code. This is where the app connects to the database.

## Endpoints

## Venues

### `GET /venues`

- Fetches all the venues from the database
- Request arguments: None
- Returns: A list of venues filtered by cities and states

#### `Response`

```json5
{
  "city" : "New York",
  "state" : "State",
  "venues": [
    {
      "id": 1,
      "name": "Venue",
      "num_upcoming_shows": 3
    },
    {
      "id": 2,
      "name": "Venue 2",
      "num_upcoming_shows": 6
    }
  ]
}
```


### `GET /venues/<int:venue_id>`

- Fetches a venue matching the venue id
- Request arguments: Venue id
- Returns: a fully detailed venue or `404 Not Found` if there's no venue matching that id 

#### `Response`

```json5
{
    "id": 31,
    "name": "Venue",
    "genres": [],
    "address": "Address",
    "city": "New York",
    "state": "State",
    "phone": "134453635",
    "website": "https://Venue.com",
    "facebook_link": "https://facebook.com/Venue",
    "seeking_talent": true,
    "seeking_description": false,
    "image_link": "https://venue.png",
    "past_shows": [
       {
              "artist_id": 1,
              "artist_name": "Artist",
              "image_link": "https://artist.png",
              "start_time": "6:30PM"
        },
        {
              "artist_id": 2,
              "artist_name": "Artist 2",
              "image_link": "https://artist.png",
              "start_time": "6:30PM"
        }
     ],
    "upcoming_shows": [
       {
              "artist_id": 3,
              "artist_name": "Artist 3",
              "image_link": "https://artist.png",
              "start_time": "6:30PM"
        },
        {
              "artist_id": 4,
              "artist_name": "Artist 4",
              "image_link": "https://artist.png",
              "start_time": "6:30PM"
        }
     ],
    "past_shows_count": 2,
    "upcoming_shows_count": 2
}
```

### `POST /venues/search`

- Fetches venues matching the search term
- Request arguments: Search term
- Returns: A list of venues matches the search term

#### `Response`

```json5
{
  "count" : 2,
  "data": [
    {
      "id": 1,
      "name": "Venue",
      "num_upcoming_shows": 3
    },
    {
      "id": 2,
      "name": "Venue 2",
      "num_upcoming_shows": 6
    }
  ]
}
```

### `POST /venues/create`

- Creates a venue using the form values
- Request arguments: Venue Form data
- Returns: back to home

#### `Request`

```json5
{
    "id": 31,
    "name": "Venue",
    "city": "New York",
    "state": "State",
    "address": "Address",
    "phone": "134453635",
    "genres": [],
    "image_link": "https://venue.png",
    "facebook_link": "https://facebook.com/Venue",
    "website": "https://Venue.com",
    "seeking_talent": true,
    "seeking_description": false,
}
```

### `DELETE /venues/<int:venue_id>`

- Deletes a venue matching the venue id
- Request arguments: Venue id
- Returns: back to home

## Artists

### `GET /artists`

- Fetches all the artists from the database
- Request arguments: None
- Returns: A list of artists

#### `Response`

```json5
{
    "id": 31,
    "name": "Artist",
    "city": "New York",
    "state": "State",
    "address": "Address",
    "phone": "134453635",
    "genres": [],
    "image_link": "https://Artist.png",
    "facebook_link": "https://facebook.com/Artist",
    "website": "https://Artist.com",
    "seeking_talent": true,
    "seeking_description": false,
}
```

### `GET /artists/<int:artist_id>`

- Fetches an artist matching the artist id
- Request arguments: None
- Returns: an artist matching the artist id or `404 Not Found` if there's no artist matching that id 

#### `Response`

```json5
{
    "id": 31,
    "name": "Artist",
    "city": "New York",
    "state": "State",
    "address": "Address",
    "phone": "134453635",
    "genres": [],
    "image_link": "https://Artist.png",
    "facebook_link": "https://facebook.com/Artist",
    "website": "https://Artist.com",
    "seeking_talent": true,
    "seeking_description": false,
    "past_shows": [
           {
              "venue_id": 1,
              "venue_name": "Venue",
              "image_link": "https://venue.png",
              "start_time": "6:30PM"
            },
            {
              "venue_id": 2,
              "venue_name": "Venue 2",
              "image_link": "https://venue.png",
              "start_time": "10:45AM"
            }
         ],
     "upcoming_shows": [
           {
              "venue_id": 3,
              "venue_name": "Venue",
              "image_link": "https://venue.png",
              "start_time": "6:30PM"
            },
            {
              "venue_id": 5,
              "venue_name": "Venue",
              "image_link": "https://venue.png",
              "start_time": "6:30PM"
            }
         ],
     "past_shows_count": 2,
     "upcoming_shows_count": 2
}
```

### `POST /artists/search`

- Fetches artists matching the search term
- Request arguments: Search term
- Returns: A list of artists matches the search term

#### `Response`

```json5
{
  "count" : 2,
  "data": [
    {
          "id": 31,
          "name": "Artist",
          "city": "New York",
          "state": "State",
          "address": "Address",
          "phone": "134453635",
          "genres": [],
          "image_link": "https://Artist.png",
          "facebook_link": "https://facebook.com/Artist",
          "website": "https://Artist.com",
          "seeking_talent": true,
          "seeking_description": false,
    },
    {
         "id": 42,
         "name": "Artist",
         "city": "New York",
         "state": "State",
         "address": "Address",
         "phone": "134453635",
         "genres": [],
         "image_link": "https://Artist.png",
         "facebook_link": "https://facebook.com/Artist",
         "website": "https://Artist.com",
         "seeking_talent": true,
         "seeking_description": false,
    }
  ]
}
```

### `POST /artists/create`

- Creates an artist using the form values
- Request arguments: Artist Form data
- Returns: back to home

#### `Request`

```json5
{
    "id": 31,
    "name": "Artist",
    "city": "New York",
    "state": "State",
    "address": "Address",
    "phone": "134453635",
    "genres": [],
    "image_link": "https://Artist.png",
    "facebook_link": "https://facebook.com/Artist",
    "website": "https://Artist.com",
    "seeking_talent": true,
    "seeking_description": false,
}
```

### Shows 

### `GET /shows`

- Fetches all shows from the database
- Request arguments: None
- Returns: a list of shows

#### `Response`

```json5
{
    "venue_id": 31,
    "venue_name": "Venue",
    "artist_id": 23,
    "artist_name": "Artist",
    "artist_image_link": "https://artist.png",
    "start_time": "4:30PM",
}
```

### `POST /shows/create`

- Creates a show using the form data
- Request arguments: Show Form data
- Returns: back to home

#### `Request`

```json5
{
    "venue_id": 31,
    "artist_id": 23,
    "start_time": "2:30AM",
}
```


## Status Codes

- `200` : Request has been fulfilled
- `201` : Entity has been created
- `400` : Missing parameters or body
- `404` : Resource not found
- `500` : Internal server error

### Development Setup

First, [install Flask](http://flask.pocoo.org/docs/1.0/installation/#install-flask)

  ```
  $ cd ~
  $ sudo pip3 install Flask
  ```

To start and run the local development server,

1. Initialize and activate a virtualenv:
  ```
  $ cd YOUR_PROJECT_DIRECTORY_PATH/
  $ virtualenv --no-site-packages env
  $ source env/bin/activate
  ```

2. Install the dependencies:
  ```
  $ pip install -r requirements.txt
  ```

3. Run the development server:
  ```
  $ export FLASK_APP=myapp
  $ export FLASK_ENV=development # enables debug mode
  $ python3 app.py
  ```

4. Navigate to Home page [http://localhost:5000](http://localhost:5000)
