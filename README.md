# README.md
# Flask Code Challenge - Superheroes
Superheroes is an API for tracking heroes and their
superpowers.


## Setup

To download the dependencies for the Superheroes, run:

```sh
pipenv install
```

You can run your Flask API on [`localhost:5555`](http://localhost:5555) by running:

```sh
python app.py
```

You can check your Superheroes progress by:

- Running the Flask server and using Postman to make requests

## Models

Superheroes has this relationships:

- A `Hero` has many `Power`s through `HeroPower`
- A `Power` has many `Hero`s through `HeroPower`
- A `HeroPower` belongs to a `Hero` and belongs to a `Power`


![domain diagram](domain.png)



## Routes

Superheroes returns JSON data in the format
along with the appropriate HTTP verb.

### GET /heroes

Return JSON data in the format below:

```json
[
  { "id": 1, "name": "Kamala Khan", "super_name": "Ms. Marvel" },
  { "id": 2, "name": "Doreen Green", "super_name": "Squirrel Girl" },
  { "id": 3, "name": "Gwen Stacy", "super_name": "Spider-Gwen" }
]
```

### GET /heroes/:id

If the `Hero` exists, return JSON data in the format below:

```json
{
  "id": 1,
  "name": "Kamala Khan",
  "super_name": "Ms. Marvel",
  "powers": [
    {
      "id": 1,
      "name": "super strength",
      "description": "gives the wielder super-human strengths"
    },
    {
      "id": 2,
      "name": "flight",
      "description": "gives the wielder the ability to fly through the skies at supersonic speed"
    }
  ]
}
```

If the `Hero` does not exist, return the following JSON data, along with
the appropriate HTTP status code:

```json
{
  "error": "Hero not found"
}
```

### GET /powers

Return JSON data in the format below:

```json
[
  {
    "id": 1,
    "name": "super strength",
    "description": "gives the wielder super-human strengths"
  },
  {
    "id": 1,
    "name": "flight",
    "description": "gives the wielder the ability to fly through the skies at supersonic speed"
  }
]
```

### GET /powers/:id

If the `Power` exists, return JSON data in the format below:

```json
{
  "id": 1,
  "name": "super strength",
  "description": "gives the wielder super-human strengths"
}
```

If the `Power` does not exist, return the following JSON data, along with
the appropriate HTTP status code:

```json
{
  "error": "Power not found"
}
```

### PATCH /powers/:id

This route updates an existing `Power`. It accepts an object with
the following properties in the body of the request:

```json
{
  "description": "Updated description"
}
```

If the `Power` exists and is updated successfully (passes validations), it updates
its description and return JSON data in the format below:

```json
{
  "id": 1,
  "name": "super strength",
  "description": "Updated description"
}
```

If the `Power` does not exist, it returns the following JSON data, along with
the appropriate HTTP status code:

```json
{
  "error": "Power not found"
}
```

If the `Power` is **not** updated successfully (does not pass validations),
it returns the following JSON data, along with the appropriate HTTP status code:

```json
{
  "errors": ["validation errors"]
}
```

### POST /hero_powers

This route should create a new `HeroPower` that is associated with an
existing `Power` and `Hero`. It should accept an object with the following
properties in the body of the request:

```json
{
  "strength": "Average",
  "power_id": 1,
  "hero_id": 3
}
```

If the `HeroPower` is created successfully, sends back a response with the data
related to the `Hero`:

```json
{
  "id": 1,
  "name": "Kamala Khan",
  "super_name": "Ms. Marvel",
  "powers": [
    {
      "id": 1,
      "name": "super strength",
      "description": "gives the wielder super-human strengths"
    },
    {
      "id": 2,
      "name": "flight",
      "description": "gives the wielder the ability to fly through the skies at supersonic speed"
    }
  ]
}
```

If the `HeroPower` is **not** created successfully, it returns the following
JSON data, along with the appropriate HTTP status code:

```json
{
  "errors": ["validation errors"]
}
```
