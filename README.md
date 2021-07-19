# Coffee Shop Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) and [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/) are libraries to handle the lightweight sqlite database. Since we want you to focus on auth, we handle the heavy lift for you in `./src/database/models.py`. We recommend skimming this code first so you know how to interface with the Drink model.

- [jose](https://python-jose.readthedocs.io/en/latest/) JavaScript Object Signing and Encryption for JWTs. Useful for encoding, decoding, and verifying JWTS.

## Running the server

From within the `./src` directory first ensure you are working using your created virtual environment.

Each time you open a new terminal session, run:

```bash
export FLASK_APP=api.py;
```

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

## Tasks

### Setup Auth0

1. Create a new Auth0 Account
2. Select a unique tenant domain
3. Create a new, single page web application
4. Create a new API
    - in API Settings:
        - Enable RBAC
        - Enable Add Permissions in the Access Token
5. Create new API permissions:
    - `get:drinks-detail`
    - `post:drinks`
    - `patch:drinks`
    - `delete:drinks`
6. Create new roles for:
    - Barista
        - can `get:drinks-detail`
    - Manager
        - can perform all actions
7. Test your endpoints with [Postman](https://getpostman.com). 
    - Register 2 users - assign the Barista role to one and Manager role to the other.
    - Sign into each account and make note of the JWT.
    - Import the postman collection `./starter_code/backend/udacity-fsnd-udaspicelatte.postman_collection.json`
    - Right-clicking the collection folder for barista and manager, navigate to the authorization tab, and including the JWT in the token field (you should have noted these JWTs).
    - Run the collection and correct any errors.
    - Export the collection overwriting the one we've included so that we have your proper JWTs during review!

### Implement The Server

There are `@TODO` comments throughout the `./backend/src`. We recommend tackling the files in order and from top to bottom:

1. `./src/auth/auth.py`
2. `./src/api.py`
# link to get token
https://mostafaelhabrok.us.auth0.com/authorize?
  audience=coffee-shop&
  response_type=token&
  client_id=8WqL4GWUB0mENmoqR3tYqGANArfmt3Z2&
  redirect_uri=http://localhost:8100/tabs/user-page

# Tokens
  barista:
  eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IjI1ay1GMjhKX25OT0tyX09CbTY5QiJ9.eyJpc3MiOiJodHRwczovL21vc3RhZmFlbGhhYnJvay51cy5hdXRoMC5jb20vIiwic3ViIjoiYXV0aDB8NWZmNDgwOGZlYTNmYzcwMDc4NzdhYTQ2IiwiYXVkIjoiY29mZmVlLXNob3AiLCJpYXQiOjE2MTAwMDcwNjksImV4cCI6MTYxMDA5MzQ2OSwiYXpwIjoiOFdxTDRHV1VCMG1FTm1vcVIzdFlxR0FOQXJmbXQzWjIiLCJzY29wZSI6IiIsInBlcm1pc3Npb25zIjpbImdldDpkcmlua3MtZGV0YWlsIl19.Bdh0mJsIVehqET8ZpBRaKpYFlSjCmgEfvdJGLn65NeNSIMM96h6ukikvAVJF_Iw6eAarq7RpboQL6_iXXq1VYaGo9aTF0uGpN5jWKv3D1Btw285SmFgUN91haVXqHmXij2RtrZWiGQtzl3Jprusm9DtuqtkcPzECe24P8jBzZAWOz8DmGk0esCiJamHe9Ktp8n5KMJTlp9h20ZX9ONB2by68_r-32lwtwRphot37Sj_XJRHb_JdIvNfBMMuEMah2pI7kfaon3KS-hD9XqPPC-awgK2h_hi2yHMdkLoLLaNM5xtpCpUO2NAFx_u6o3NM9LYKqv6zbx_6tFQZEtmTRDQ

  manager:
  eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IjI1ay1GMjhKX25OT0tyX09CbTY5QiJ9.eyJpc3MiOiJodHRwczovL21vc3RhZmFlbGhhYnJvay51cy5hdXRoMC5jb20vIiwic3ViIjoiYXV0aDB8NWZmNDgwZDE4MTYzN2IwMDY4NWQ1YTUxIiwiYXVkIjoiY29mZmVlLXNob3AiLCJpYXQiOjE2MTAwMDcxMjYsImV4cCI6MTYxMDA5MzUyNiwiYXpwIjoiOFdxTDRHV1VCMG1FTm1vcVIzdFlxR0FOQXJmbXQzWjIiLCJzY29wZSI6IiIsInBlcm1pc3Npb25zIjpbImRlbGV0ZTpkcmlua3MiLCJnZXQ6ZHJpbmtzLWRldGFpbCIsInBhdGNoOmRyaW5rcyIsInBvc3Q6ZHJpbmtzIl19.Tnh8IAYtQYUWiUoz_gXUoESecZh4AggXerJmFsreXg3--0DjSu8sc6cdY0H2snww4zP7wr0ViHyWI-RpW531z629mWZ4KFPbrcLDaOv-6Xyq_fDjiFgp4Ulvz7h3NOAsCS_Ljfdc_vqpvgOR0lKnWEImGLLRV-HCPrP73yiSWDokD0Y2zLkNWCGYzusih7cW4WWEYW8KYjwxkltJHWO-vHAcErA5gLaXqkda6Ntb6NMgsVXKl5oY7nbZCZARqpijZ-c7z7sa1R2NSlBfmdD7rvY0C4c9GBdNlSPy9kkzRFUcWqfPrSK45c_fvgy43Iq1vkC6lGoRZN2EjuMHbqfpZw