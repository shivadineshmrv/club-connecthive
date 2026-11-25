# ClubConnect Hive – CollabCampus Cup

A responsive Flask + SQLite prototype for campus club discovery, membership, shared-resource booking and cross-club event planning.

## Features
- Dashboard with live counts and upcoming activity
- Searchable, category-filtered directory of 8 sample clubs
- Club detail pages, faculty advisors, executive leads, achievements and member rosters
- Join-club workflow with duplicate-email protection
- Shared resources: Main Audi, Seminar Hall A, Project Lab 3, projector and PA system
- Booking overlap detection using `existing_start < requested_end AND existing_end > requested_start`
- Joint event creation requiring at least two co-host clubs
- Campus events feed, community discussion board and club scorecard
- SQLite persistence; sample seed data (30 members and 12 events)

## Requirements
- Python 3.9+
- pip

## Run (macOS / Linux)
```bash
cd ClubConnect_Hive_Prototype
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python app.py
```
Open http://127.0.0.1:5000

## Run (Windows)
```bat
cd ClubConnect_Hive_Prototype
py -m venv .venv
.venv\\Scripts\\activate
pip install -r requirements.txt
py app.py
```
Open http://127.0.0.1:5000

## Suggested judge demo
1. Open Clubs and select Robotics Club.
2. Browse Coding Society and return to Joint Events.
3. Propose `AI Robo-Hack 2026`, select Robotics Club and Coding Society as co-hosts.
4. Open Resource Booking. Select Main Audi, Robotics Club, a date, 14:00–15:00 and submit.
5. Submit a second booking for Main Audi, Dramatics Society, same date and 14:00–15:00. The app rejects it with `Facility Already Reserved`.
6. Try an adjacent slot (15:00–16:00); it is accepted because touching endpoints are not overlapping.

## Booking logic
For a requested interval `[start, end)` and an existing interval `[old_start, old_end)`, a collision exists when:
`old_start < end AND old_end > start`.
This correctly rejects full containment and partial overlaps while allowing back-to-back bookings.

## Project structure
```text
ClubConnect_Hive_Prototype/
├── app.py
├── requirements.txt
├── README.md
├── templates/
└── static/
```

## Important prototype notes
- The demo uses a simple open campus portal rather than real authentication. Do not use real student data or expose it publicly as-is.
- Booking requests are automatically approved in this prototype. A production version should add user accounts, role-based permissions, faculty approval, CSRF protection, validation, audit logs and database-level transaction locking for concurrent requests.
- QR attendance is represented as a future extension; the current attendance table is ready for expansion.
