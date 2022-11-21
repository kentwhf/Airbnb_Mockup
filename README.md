
# Project 1, Part 3 Submission from Brian Lee, Huifeng Wu

This repository holds the Flask / Jinja stack with server.py serving SQL table queries from 
REST API Endpoints. And the HTML with Jinja Templates and CSS files are in the templates folder.


## Installation

To get this project up and running on your local environment:

First, if you don't have postgresql installed on your OS, install brew (if you haven't already), then run:
```bash
  brew install postgresql
```

Then run:

```bash
  python3 -m venv venv
  . venv/bin/activate
  pip install flask
```

Then try running using

```bash
python3 server.py
```

if you are getting an error after this step, execute code below on terminal then try again:

```bash
pip install psycopg2
```

After this point, the server should get running, and you will be able to see the 
HTML pages in the templates folder.
## API Reference

#### Pages

```http
  GET /
```

Returns index page with 4 rentals to show.

&nbsp;

```http
  GET /rentals
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `from` | `string` | **Required**. Start Date Filter |
| `to` | `string` | **Required**. End Date Filter |
| `order_by` | `string` | **Required**. Order Category |
| `sort_by` | `string` | **Required**. ASC or DESC |
| `amenity1` | `boolean` | Swimming Pool inclusion |
| `amenity2` | `boolean` | Gym inclusion |

Returns the rental page with filters enabled

&nbsp;

```http
  GET /login
```

Returns the login form page

&nbsp;

```http
  GET /create
```

Returns the create user form page

&nbsp;

```http
  GET /user
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `uid` | `string` | **Required**. User ID |

Returns the user page with uid specified in parameter

&nbsp;

#### API References

```http
  GET /available_times
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `pid`      | `string` | **Required**. Property ID |

Get's all available times for a particular property

&nbsp;

```http
  POST /create_profile
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `first_name`      | `string` | **Required**.First Name |
| `last_name`      | `string` | **Required**. Last Name |
| `phone_number`      | `string` | **Required**. Phone Number |
| `password`      | `string` | **Required**. Password |

Create's a user profile with parameters above

&nbsp;

```http
  POST /login_user
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `phone_number`      | `string` | **Required**. Phone Number |
| `password`      | `string` | **Required**. Password |

Log's in user if parameters are correct

&nbsp;

```http
  POST /create_prop
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `uid`      | `string` | **Required**. User ID |
| `addr`      | `string` | **Required**. Address |
| `city`      | `string` | **Required**. City |
| `state`      | `string` | **Required**. State |
| `size`      | `string` | **Required**. Property Size |
| `amenity1`      | `boolean` | Swimming Pool |
| `amenity2`      | `boolean` | Gym |

Creates a property under a certain user's id

&nbsp;

```http
  POST /delete_prop
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `pid`      | `string` | **Required**. Property ID |

Deletes a property

&nbsp;


```http
  POST /add_availability
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `pid`      | `string` | **Required**. Property ID |
| `start_from`      | `string` | **Required**. Start Date |
| `end_at`      | `string` | **Required**. End Date |

Creates an availability row for a particular property

&nbsp;

```http
  POST /remove_availability
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `pid`      | `string` | **Required**. Property ID |
| `start_from`      | `string` | **Required**. Start Date |
| `end_at`      | `string` | **Required**. End Date |

Removes an availability row for a particular property

&nbsp;

```http
  POST /book
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `pid`      | `string` | **Required**. Property ID |
| `uid_host`      | `string` | **Required**. Host's User ID |
| `uid_renter`      | `string` | **Required**. Renter's User ID |
| `start_from`      | `string` | **Required**. Start Date |
| `end_at`      | `string` | **Required**. End Date |

Book's a rental slot for someone else's property under their available times
## AJAX Calls from Front End

    1. index.html / line 176:
    - /available_times GET AJAX call. Get's all available times for a property.
      on success, appends html to the page showing available times.

    2. index.html / line 244:
    - /book POST AJAX call, for when a user books a rental. 
      Reloads on successful book.

    3. login.html / line 50:
    - /login_user POST AJAX call, for logging in a user.
      Redirects to the user page after successful 200 status.

    4. rentals.html / line 215:
    - /available_times GET AJAX call. Get's all available times for a property.
      on success, appends html to the page showing available times.

    5. rentals.html / line 283:
    - /book POST AJAX call, for when a user books a rental. 
      Reloads on successful book.

    6. user.html / line 204:
    - /book POST AJAX call, for when a user books a rental. 
      Reloads on successful book.

    7. user.html / line 220:
    - /delete_prop POST AJAX call, remove's a user's property
      Reloads page on success.

    8. user.html / line 348:
    - /available_times GET AJAX call. Get's all available times for a property.
      on success, appends html to the page showing available times.

    9. user.html / line 399:
    - /remove_availability POST AJAX call. Removes a particular availability from a property.
      Removes the HTML for the removed available time on success.