# Copilot Instructions

## Architecture

- `src/app.py` is the FastAPI application and source of truth for activities. Activity data is an in-memory dictionary keyed by activity name; the API exposes it at `/activities` and handles sign-ups at `/activities/{activity_name}/signup`.
- The root route redirects to the static site. `src/static/index.html`, `app.js`, and `styles.css` make up the browser UI; `app.js` fetches the activities API to populate both activity cards and the sign-up selector.
- Data is not persisted: activity and participant changes are lost when the server restarts. Keep the API response fields and frontend rendering in sync when changing the activity model.

## Run and test

- Install dependencies with `pip install -r requirements.txt` (also run automatically when the dev container is created).
- Start the app from the repository root with `uvicorn src.app:app --reload`. The VS Code launch configuration uses this application target.
- The project has a `pytest.ini`, but no tests directory yet and `pytest` is not currently in `requirements.txt`. The testing exercise asks to add pytest and backend tests under `tests/`.
- Once pytest and tests are present, run the suite with `python -m pytest`; run one test with `python -m pytest tests/test_app.py::test_name` (replace with the actual file and test node).

## Repository conventions

- Keep activity records keyed by their displayed names and preserve the fields consumed by the UI: `description`, `schedule`, `max_participants`, and `participants`.
- The app uses FastAPI routes for backend behavior and browser-native JavaScript with `fetch` for API calls; static assets are served under `/static`.
- This repository is a staged GitHub Skills exercise. Numbered workflows correspond to `.github/steps/` and check specific branches, paths, or deliverables; inspect the matching workflow before changing files that are part of an exercise step.
