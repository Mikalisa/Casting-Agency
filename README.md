# Casting Agency Capstone

The Casting Agency API models a company that is responsible for creating movies and managing/assigning actors to those movies.
This api is responsible for checking permissions and handling CRUD for an Actor and Movie model/
## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the root directory of this project and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

After installing the dependencies, In the Token_test file there all variables needed like Tokens AUTH0_DOMAIN and API_AUDIENCE.

I have also created three accounts for testing with auth0:

casting-assistant@casting-agency.com
password: 123456789Assistant

casting-director@casting-agency.com
password: 123456789Director

executive-produce@cating-agency.com
password: 123456789Producer


The app can be found live on https://casting-agenccy.herokuapp.com/actors


Execute the bash file `setup.sh` to set the user jwts, auth0 credentials and the remote database url by naviging to the root directory of this project and running:

```bash
source setup.sh
```

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server.

- [jose](https://python-jose.readthedocs.io/en/latest/) JavaScript Object Signing and Encryption for JWTs. Useful for encoding, decoding, and verifying JWTS.

## Running the server

From within the root directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=app.py
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 



## API Reference

### Error Handling
Errors are returned as JSON objects in the following format:
```
{
    "success": False, 
    "error": 404,
    "message": "Resource not found."
}
```

The API will return three error types with multiple different error messages when requests fail:
- 400: Bad Request
- 400: Permissions were not included in the JWT.
- 400: Unable to parse authentication token.
- 400: Unable to parse authentication token.
- 400: Unable to find the appropriate key.

- 401: Authorization header is expected.
- 401: Authorization header must start with "Bearer".
- 401: Token not found.
- 401: Authorization header must be bearer token.
- 401: Authorization malformed.
- 401: Token expired.
- 401: Incorrect claims. Please, check the audience and issuer.

- 403: Permission denied.

- 404: Resource Not Found.

### Endpoints

#### GET '/actors'
- Fetches a paginated list of actors.
- Request Arguments: offset: 1(default), limit: 30(default).
- Returns: list of actors ordered by id.
```

{
  'success': True,
  'actors': [
    {
      id: 1,
      name: 'Actor 1',
      age: 30,
      gender: 'male'
    }
  ]
}
```

#### GET '/movies'
- Fetches a paginated list of movies.
- Request Arguments: offset: 1(default), limit: 30(default).
- Returns: list of movies ordered by id.
```
{
  'success': True,
  'movies': [
    {
      id: 1,
      title: 'New Movie 1',
      release_date: '2021-10-1 04:22'
    }
  ]
}
```

#### POST '/actors'
- Create a new actor.
- Request Arguments: { name: String, age: Integer, gender: String }.
- Returns: An object with `success: True` and the new actor inside an array.
```
{
  'success': True,
  'actors': [
    {
      id: 2,
      name: 'Actor 2',
      age: 28,
      gender: 'Female'
    }
  ]
}
```

#### POST '/movies'
- Create a new movie.
- Request Arguments: { title: String, release_date: DateTime }.
- Returns: An object with `success: True` and the new movie inside an array.
```
{
  'success': True,
  'movies': [
    {
      id: 2,
      title: 'New Movie 2',
      release_date: '2022-10-1 04:22'
    }
  ]
}
```

#### Patch '/actors/<actor_id>'
- Update an actor.
- Request Arguments: { name: String, age: Integer, gender: String }.
- Returns: An object with `success: True` and the updated actor inside an array.
```
{
  'success': True,
  'actors': [
    {
      id: 1,
      name: 'Updated Actor',
      age: 50,
      gender: 'Male'
    }
  ]
}
```

#### Patch '/movies/<movie_id>'
- Update a movie.
- Request Arguments: { title: String, release_date: DateTime }.
- Returns: An object with `success: True` and the updated movie inside an array.
```
{
  'success': True,
  'movies': [
    {
      id: 1,
      title: 'Updated Movie 1',
      release_date: '2030-10-1 04:22'
    }
  ]
}
```

#### DELETE '/actors/<actor_id>'
- Removes an actor from the database.
- Request Parameters: question id slug.
- Returns: An object with `success: True` and the id of the deleted actor
```
{
  'success': True,
  'id': 1
}
```

#### DELETE '/movies/<movie_id>'
- Removes a movie from the database.
- Request Parameters: question id slug.
- Returns: An object with `success: True` and the id of the deleted movie
```
{
  'success': True,
  'id': 1
}
```


#### Running tests locally
To run the tests from ./test_app.py, first make sure you have ran and executed the setup.sh file to set the enviorment.

After setting the enviorment start your local postgress server:
```bash
pg_ctl -D /usr/local/var/postgres start
```

Then run the follwing commands to run the tests:
```
dropdb casting_test
createdb casting_test
psql casting_test < casting_test.psql
python test_app.py
```