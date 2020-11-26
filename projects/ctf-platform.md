---
tags: project
---

# CTF Platform

This project has the (temporary) name of `flags-rs`, which reads "Flags'r'us".

- [CTF Platform](#ctf-platform)
  - [Objective](#objective)
  - [Meta Objectives](#meta-objectives)
  - [Architecture](#architecture)
    - [Frontend](#frontend)
    - [Backend](#backend)
    - [Data](#data)
  - [API](#api)
    - [Register - `/register`](#register---register)
      - [Supported Methods](#supported-methods)
    - [Login - `/login`](#login---login)
      - [Supported Methods](#supported-methods-1)
    - [Challenges - `/challenges`](#challenges---challenges)
      - [Supported Methods](#supported-methods-2)
    - [Scoreboard - `/score`](#scoreboard---score)
      - [Supported Methods](#supported-methods-3)
    - [Profile - `/profile`](#profile---profile)
      - [Supported Methods](#supported-methods-4)

## Objective

The objective of this project is to build a new CTF challenge platform.
While the scope can increase (as in every project),
the platform aims to be opinionated and simple for both organizers and end-users (with a focus on the end user).

The platform UI should be fast and not lag when selecting a challenge (looking at you CTFd).
Page loads should also be fast, no one likes to wait for the challenges nor occupy bandwidth with unnecessary information.

Also, it is 2020, we are dealing with accounts, lets keep things safe by using:
- HTTPS
- Decent Session Tokens
- Encrypted Password Storage
- Decent Password Recovery (?)
- Store user details encrypted (?)

## Meta Objectives

This project has the following meta objectives:
- Learn more about WebAssembly.
- Learn about web development, both front and back end.

## Architecture

The platform should be a 3-tier solution, that is, frontend, backend and a data tier.

### Frontend

The frontend is supposed to be supported by [Seed](https://seed-rs.org/),
as previously discussed, it is supposed to be fast and lightweight.

The current idea is for the front end to be served by the `GET` requests from the server API,
however, ideally the frontend should be possible to be cached and served from outside the API.

While caching should be possible, one needs to be careful as challenges could be hidden by old cache instances.

### Backend

The backend aims to be scalable, ideally it could be distributed as to take care of the beating a CTF takes on the server,
but hiding several instances behind a Nginx instance seems like a sensible solution as well.

The candidates for the backend framework are [Actix Web](https://actix.rs/), known for its speed, and [Tokio Hyper](https://tokio.rs).
I have no experience with either and need to find out more.

### Data

The data tier could be agnostic to the backend, but locking it to SQL seems to be a more scalable in the long way.
To start we could just support SQLite and eventually add support for PostgreSQL.
Being agnostic to the backend is the ideal solution, however I think we'd still need to lock in with a set of interfaces,
this requires more research.

Challenges requiring blobs will need to be stored somewhere,
we could either serve them or store in a CDN/Blob storage solution.
Either solution is required to be independent of the API,
so when the API is queried for challenges, their JSON only returns a download link.

## API

The API aims to be feature-complete from the client-side first, that is, a backoffice application is not a priority.
It should be public and easy to use, there is no need for people to write web-scrappers to download the challenges,
simply authenticate and download the JSON.

In the case that requests have unexpected headers maybe the server can return a `400`, signaling the client to not send such headers.

### Register - `/register`

The register endpoint allows clients to register a user.
In the case that teams are to register,
they should use one account and share the password,
competition among teammates is counter-productive and should not take place within another competition
(or just keep an internal scoreboard).

#### Supported Methods

- `GET` - Returns the HTML page
  - Always return `200`
- `POST` - Registers a new user in the platform
  - Return `200` if the user is successfully registered
  - Return `409` if the user already exists

### Login - `/login`

Login the user into the platform.
A successful login should be accompanied by a session token,
the token implementation is pending but candidates are:

- JWT
- PASETO

Since JWT is standardized, it is probably a better solution.

#### Supported Methods

- `GET` - Returns the HTML page
  - Always return `200`
- `POST` - Login the client into the platform
  - Return `200` if the login is successful, include a session cookie (pending research)
  - Return `401` on a failed login attempt

### Challenges - `/challenges`

Return the list of available challenges.
The challenge is required to have a flag, but obviously, the flag should not be returned by the public API.

A challenge should have at least 2 attributes:

- Name
- Description

Optionally, the challenge can contain a single challenge file,
if several files are required, make use of `.zip` or other compression formats.
There is no excuse to make people download several files.

In the API, the file field should return a direct link to the file download.
The file can be hosted directly on the server or in a separate storage solution (e.g. Azure Blob Storage)

#### Supported Methods

- `GET` - This imposes a problem, either the request returns the API or the page.
  The server may also separate the API in two endpoints. If this is done, then all other endpoints must be converted.
  - Returns `403` if the user is not authenticated
  - `200` if the challenges are up
  - `204` if there are no challenges

### Scoreboard - `/score`

Should return the scoreboard, this can be presented in a ranked list.
The page can also have some visualization of the current score for the top teams,
however it is important to keep in mind that speed is a priority and loading an external JS source to show a graph is expensive.
Finally, the scoreboard should be able to handle pagination, this is not hard, rather a matter of handling query parameters and some `LIMIT` queries on the database.

#### Supported Methods

- `GET` - Just like the challenges, this requires the API endpoints to be distinct from the presentation ones.
  - If there are no teams on the scoreboard the endpoint returns `204`
  - Otherwise returns `200`

### Profile - `/profile`

Show a user profile, maybe allow a user to make changes to its information,
however, available information should already be minimal.

Required information for an account should be a username and password.

#### Supported Methods

- `GET` - Another dissociation between API and presentation, should return the user information
  - `404` if the user does not exist
  - `200` if it exists
- `PUT` - should allow a user to add information, such as country and team kind (Highschool, University, Professional), existing information is replaced.
  Requires authentication.
  - `200` if the request is successful
  - `403` if not authenticated
  - `400` if the request is missing information or something else