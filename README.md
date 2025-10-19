# MobileApp-Referee-Manager
Referee Manager is a simple mobile app for managing referees and their match assignments. The app lets referees and coordinators view profiles, add and update personal information, record past matches, and see upcoming assignments. It works offline so referees can update availability or match notes on their phones without an internet connection; changes are synced automatically when online.

Entity: Referee
id — Unique identifier (assigned by server).'\n'
fullName — Full name shown in the list and profile.
birthDate — Date of birth (used to compute age).
contactPhone — Phone number for scheduling/notifications.
leagues — List of competitions the referee can officiate (e.g., “Local League A”, “Youth Cup”).
profilePhotoUrl — URL or local path to a profile photo.
averageRating — Numeric average of user ratings (0–5).
notes — Short free text for availability, certifications, etc.
