Build "Stable Match" — a full-stack horse-dating app — as a working, well-tested project.
This is a real app that will later be code-reviewed, so correctness, clarity, and idiomatic
style matter as much as features. Build it clean: NO deliberate bugs, NO shortcuts.

## Stack (hard requirements)
- Backend: Python 3.11+, FastAPI, SQLAlchemy 2.x, SQLite. Pydantic v2 schemas. Passwords hashed
  with passlib[bcrypt]. Auth via bearer tokens stored in a Session table.
- Tests: pytest, using an in-memory or temp SQLite DB. All tests must pass.
- Frontend: a thin vanilla HTML/CSS/JS client (no framework, no build step).
- Pinned requirements.txt. Runs fully offline, no external services, no network calls.
- One documented way to run it: `pip install -r requirements.txt`, `python -m app.seed`,
  then `uvicorn app.main:app --reload`.

## Split the work across your team, one agent per stream, in PARALLEL.
FIRST agree the shared foundation (models + database + Pydantic schemas) since everything
depends on it, THEN fan out routes / matching / auth / frontend / tests against that contract.

- DATA & DB: SQLAlchemy models + engine/session setup + a seed script with ~10 funny horse
  profiles (Sir Gallops-a-Lot, Neighoncé, etc.).
- AUTH: signup, login, bearer-token sessions, and a get_current_horse dependency.
- API ROUTES: profiles, likes, matches endpoints (contract below).
- MATCHING SERVICE: the reciprocity logic (spec below), isolated in services/matching.py.
- FRONTEND: a swipe view (fetch the deck, like/pass) and a "My Stable" matches view.
- TESTS: pytest suite covering auth, likes, matching, and access control.

## Data model
- Horse: id, username (unique), password_hash, name, breed, age, bio, avatar_emoji, created_at.
  PUBLIC fields = name, breed, age, bio, avatar_emoji, interests. PRIVATE = its likes, matches.
- Interest: id, horse_id (FK), tag  (a horse has several; store as its own table/rows — NOT a
  comma-joined string).
- Like: id, liker_id (FK Horse), likee_id (FK Horse), created_at. Unique(liker_id, likee_id).
- Match: id, horse_a_id (FK), horse_b_id (FK), created_at. One row per unordered pair.
- Session: id, token (unique), horse_id (FK), created_at.

## Matching rule (implement exactly)
A Match between A and B exists IF AND ONLY IF A has liked B AND B has liked A (mutual).
When a like is created, check whether the reverse like already exists; if so, create exactly
one Match for the unordered pair {A, B} (never duplicate, never self-match).

## API contract
- POST /auth/signup      -> create a horse account, return the horse's public profile
- POST /auth/login       -> {username, password} -> {token}
- GET  /profiles         -> list PUBLIC profiles for the swipe deck (exclude the current horse)
- GET  /profiles/{id}    -> one horse's PUBLIC profile
- PUT  /profiles/me      -> update the current horse's own profile (auth required)
- POST /likes            -> {likee_id}; records a like, creates a Match if reciprocal (auth required)
- GET  /matches          -> the current horse's matches (auth required; PRIVATE — a horse may only
                            see its own matches)

## Project layout
stable-match/
  backend/
    app/
      main.py            # FastAPI app + router registration
      database.py        # engine, SessionLocal, Base, get_db
      models.py          # SQLAlchemy models
      schemas.py         # Pydantic v2 schemas
      auth.py            # signup/login, token issue, get_current_horse dependency
      routers/{profiles.py, likes.py, matches.py}
      services/matching.py
      seed.py            # seed the ~10 horses
    tests/{conftest.py, test_auth.py, test_likes.py, test_matching.py, test_profiles.py}
    requirements.txt
    README.md            # how to install, seed, run, and test
  frontend/{index.html, app.js, styles.css}

## Tests must cover (at minimum)
- signup then login returns a working token
- liking back creates exactly one match; a one-directional like creates NO match
- /matches requires auth and returns only the current horse's matches
- a horse cannot see another horse's matches

## Conventions
- Type hints everywhere, short focused functions, docstrings on services and non-obvious routes.
- Idiomatic FastAPI (dependencies for DB session + current horse). Parameterized queries only.
- Clean, readable, review-ready code. No dead code, no TODOs left in.

## Done means
- `pytest` is green, the server runs via the documented command, the seed loads ~10 horses,
  and the frontend can page through the deck and show matches.
- Reply with a one-line summary of what each agent built.
