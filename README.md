# Explosive Run — MS Dhoni Birthday Game

Single-file browser game for the Explosive Whey #7 campaign.
Static site — no build step. Vercel serves `index.html` at the root.

## Deploy (Git + Vercel)
1. Create a repo and push these files:
   ```bash
   git init
   git add .
   git commit -m "Explosive Run"
   git branch -M main
   git remote add origin <your-repo-url>
   git push -u origin main
   ```
2. In Vercel: **Add New… → Project → Import** this repo.
   - Framework Preset: **Other**
   - Build Command: *(leave empty)*
   - Output Directory: *(leave empty / root)*
   Deploy.
3. Project → **Settings → Domains** → add `win.explosivewhey.com`.
4. Add this DNS record on explosivewhey.com:
   ```
   Type:  CNAME
   Name:  win
   Value: cname.vercel-dns.com
   ```
   (Vercel shows the exact value on the Domains screen and issues HTTPS automatically.)

Every `git push` to `main` redeploys.

## Leaderboard
Already wired to Supabase (project `sorted-agency-portal`):
table `ew7_scores`, function `ew7_submit_score`. Scores write/read live.

## Go-live checklist
- In `index.html`, set `var TESTING = true;` → **false**
  (restores phone/OTP verification + the 5-runs-per-player limit and real entered names).
- Recommended: move the leaderboard to a dedicated Supabase project so the
  public anon key isn't shared with the agency CRM (ask Claude to set this up).
