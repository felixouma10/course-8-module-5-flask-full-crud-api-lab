# Flask Events API

A small Flask REST API for creating, updating, and deleting events. Event data is
stored in an in-memory Python list, so changes are reset when the server restarts.

## Requirements

- Python 3
- Flask

## Setup

Create and activate a virtual environment, then install Flask:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install flask
```

On Windows, activate the environment with:

```powershell
.venv\Scripts\Activate.ps1
```

## Run the API

From the project directory, start the Flask server:

```bash
python app.py
```

The server runs at `http://localhost:5000`.

## Endpoints

### Create an event

`POST /events`

Send a JSON body containing a title:

```bash
curl -X POST http://localhost:5000/events \
  -H "Content-Type: application/json" \
  -d '{"title":"Hackathon"}'
```

The response has status `201 Created` and includes the assigned ID:

```json
{
  "id": 3,
  "title": "Hackathon"
}
```

### Update an event title

`PATCH /events/<event_id>`

The route requires a slash before the ID (for example, `/events/1`):

```bash
curl -X PATCH http://localhost:5000/events/1 \
  -H "Content-Type: application/json" \
  -d '{"title":"Hackathon 2025"}'
```

The response has status `200 OK`:

```json
{
  "id": 1,
  "title": "Hackathon 2025"
}
```

### Delete an event

`DELETE /events/<event_id>`

```bash
curl -X DELETE http://localhost:5000/events/2
```

A successful deletion returns `204 No Content` with an empty response body.
If the requested ID does not exist, PATCH and DELETE return `404 Not Found`.

## Run the tests

Install pytest if needed, then run the test suite:

```bash
python -m pip install pytest
python -m pytest
```
