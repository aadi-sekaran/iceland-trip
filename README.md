# Iceland Trip 2026 — Planner

Shared trip planner for Aadi & Krithika, Nithish & Niranjana. 15–20 Sept 2026, Dublin → Reykjavík.

Single static `index.html` — no build step. Data (itinerary, costs, packing, checklist) is
hardcoded in the `<script>` block; checkbox state (packed / done) syncs live across everyone's
phones via Supabase.

## Stack
- Plain HTML/CSS/JS, no framework, no bundler
- Supabase (project `tlea`, table `iceland_trip_data`) for shared checkbox sync
- Deploys on Vercel, connected to this GitHub repo (auto-deploys on every push to `main`)

## Local preview
Just open `index.html` in a browser, or:
```
python3 -m http.server 8000
```

## Editing content
All trip data lives in the `ITINERARY`, `COSTS`, `PACKING`, `FOOD`, and `CHECKLIST`
JS objects near the top of the `<script>` tag in `index.html`. Edit, commit, push —
Vercel redeploys automatically.

## Supabase
Table `iceland_trip_data` (project `imagihnssgllampaqfbm` / `tlea`):
```sql
id text primary key,
data jsonb,
checks jsonb,   -- { "item-id": true/false }
updated_at timestamptz
```
Row-level security allows public select/insert/update — anon key is safe to keep client-side.
