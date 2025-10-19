# MobileApp-Referee-Manager
Referee Manager is a simple mobile app that helps sports coordinators organize referees and their match assignments easily. It allows users to view and edit referee details, record past games, and check upcoming matches in one place. The app also works offline, so information can still be viewed or updated anywhere. Once internet access is available, all updates are synchronized automatically. This saves time, reduces paperwork, and keeps referee data always up to date.  
# Referee will have the following information stored:  
-> id — Unique identifier (assigned by server).  
-> fullName — Full name shown in the list and profile.  
-> birthDate — Date of birth (used to compute age).  
-> contactPhone — Phone number for scheduling/notifications.  
-> leagues — List of competitions the referee can officiate (e.g., “Local League A”, “Youth Cup”).  
-> profilePhotoUrl — URL to a profile photo.  
-> averageRating — Numeric average of user ratings (0–5).  
-> notes — Short free text for availability, certifications, etc.

# Match will have the following information stored:  
-> id — Unique identifier.  
-> refereeId — ID of the referee assigned to this match.  
-> date — Match date and time.  
-> teams — Short description of the teams/fixture (e.g., "Team A vs Team B").  
-> competition — Name of competition (e.g., "County Cup").  
-> role — Role for that match (main referee, assistant).  
-> notes — Post-match notes (e.g., performance, incidents)  

# CRUD — details of each operation (for each entity)  
  
**Referee:**  
Create (Add a referee)    
User fills Add Referee form (name, phone, leagues, photo). App saves locally and queues the new referee to be uploaded to the server when online.

Read (View list/profile)  
The list screen reads referees from the local database (fast). When online, the app fetches updates from server and refreshes local cache.

Update (Edit referee)  
Edit screen allows changing contact, leagues or notes. Changes are applied locally immediately and synced to server in background.

Delete (Remove referee)  
Confirm delete in UI. Deletion is applied locally (so list updates immediately) and a delete request is sent to server when online.

**Match:**  
Create (Add past or future match) — stored locally and queued to server.

Read (List match history / upcoming) — read from local cache; server update on sync.

Update (Edit match notes or role) — local immediate, sync later.

Delete (Remove match record) — local remove + server delete queued.

# Persistence details (what is stored where)

-Local database (mobile device) — All referees and match records are persisted locally (SQLite or similar). This ensures the app is fully functional offline (reads/writes).  
-Server (remote central API) — The definitive copy lives on the server. The app synchronizes changes (create / update / delete) to the server when online.  
-Minimum operations persisted on both (for excellent rubric coverage): Create, Update, Delete for both Referee and Match are persisted locally immediately and sent to the server when online. Read uses local cache for speed and offline availability; server read updates local cache on sync.

# Offline scenarios (one separate scenario for each CRUD operation as required)

-Create (offline) — A coordinator in a stadium has no signal but needs to add a new assistant referee. They fill the Add screen and tap Save. The referee appears immediately in the list (local DB). The app notes “Pending sync” and automatically uploads when online later.  
-Read (offline) — A referee traveling to a match opens the app at the stadium where there’s no internet. They can open their profile and see their previous matches and contact phone because the data is available from the local cache.  
-Update (offline) — After a match, a referee adds post-match notes while offline. The note is saved locally and shown in the local profile. When the device reconnects, the note is pushed to the server. If the same match was edited on another device earlier, a simple “last-writer-wins” policy is used and the user is notified about the conflict.  
-Delete (offline) — The coordinator deletes an outdated match record while offline. The record disappears locally and a delete operation is queued to the server. When online, the server processes the delete.

# App mockups  
<img width="1024" height="1024" alt="ChatGPT Image 19 oct  2025, 18_33_25" src="https://github.com/user-attachments/assets/bcd9082c-a4e5-4ad9-aeee-d9ebe1254b66" />

