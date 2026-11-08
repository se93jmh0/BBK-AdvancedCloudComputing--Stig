# User Journey: Logging In and Retrieving Posts

Note that all implementation details (i.e., non-API bits) of this journey are
currently subject to change.

Before a user can log into the the Piazza Application, first they must register.
To do this, they send a Register Request (a `POST` to `/auth/register`) with
a JSON body containing their email address and a password of their choosing. The
Piazza Application checks that the user is not already registered, then hashes
the password (so that if the worst happens and the credentials database is
leaked, then the password is still not compromised) and stores the combination
in the database.

The user is now able to log in, which they do by sending a Login Request (a
`POST` to `/auth/login`) with a JSON body containing their email address and
previously-registered password.  The Piazza Application checks that the user
exists and that the hashed password matches, and then responds with a JWT
with a preconfigured expiry.

The user is now able to query Posts.  They do this by sending the JWT they
received to the Login Request to the `/posts` endpoint, possibly with `topic`
and/or `status` filters (which are pre-validated using Pydantic).  The Piazza
Application verifies the token by means of its secret key and the PyJWT library,
and assuming that everything is ok, returns the filtered Posts, using
SQLAlchemy's ORM technology and by dynamically calculating whether each stored
Post is expired or not.  Should the supplied JWT be invalid or have expired,
rather than receiving a (possibly empty) JSON-based list of Posts in a 200
response, they will instead receive a 401.

# First Outstanding Design Question

Can we use SQLAlchemy to calculate Post expiry?
