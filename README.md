# Our Stories, Our Lives — website starter

This folder contains a responsive, heritage-inspired front-end prototype for the 52-week family-history project.

## Preview
Open `index.html` in a modern browser. No build tools are required.

## Important prototype limitations
- Entries are stored in the browser's localStorage on the device where they are entered.
- This is not yet a shared or hosted website. Grandmother's and Grandfather's browsers will not sync.
- The photograph input records the selected filename only; it does not upload or permanently store image files.
- There is no authentication, family access code, server database, backup, or PDF book export yet.
- Do not use the prototype for private or sensitive family information.

## Production implementation plan

### Recommended stack
- Front end: Next.js (or a similarly maintained React framework).
- Database, authentication and image storage: Supabase (Postgres + Auth + Storage).
- Hosting: Vercel or another managed host with HTTPS.
- Access model: one family invitation link plus a family access code. For stronger privacy, use individual magic links for each grandparent and family members.
- Backups: scheduled database exports and a separate copy of uploaded photographs.

### Core data model
1. `families`: id, family_name, access_code_hash, created_at.
2. `members`: id, family_id, display_name, role, auth_user_id.
3. `questions`: id, week_number, chapter, title, prompt, release_at.
4. `entries`: id, family_id, member_id, question_id, answer_text, recipe_text, submitted_at, updated_at, visibility.
5. `media`: id, entry_id, storage_path, original_filename, media_type, caption.

### Access and privacy rules
- The public URL alone must not expose entries.
- Require a family access code or authenticated invite before showing the archive.
- Restrict each participant to editing their own entries.
- Permit family members to read entries only after access is granted.
- Validate uploads (image formats and file-size limits); use private storage and signed URLs.
- Provide a way to export and delete data.
- Obtain both grandparents' agreement before making their entries visible to the wider family.

### Weekly release logic
- Project start: 2026-12-25.
- Release one question every seven days, using the family's chosen timezone (recommend America/Halifax).
- Keep previous questions editable and allow late answers.
- Do not lock people out for missed weeks.
- Send reminders only if the family opts in.

### Build phases
1. Confirm names, family title, family access approach, and whether answers are visible immediately.
2. Create the database, access policies, storage bucket, and family invitation flow.
3. Connect the weekly question view and autosaving editor to the database.
4. Add image uploads, recipe fields, family archive, search, and progress tracking.
5. Add export to structured JSON/CSV and generate a print-ready PDF/book layout.
6. Test on a phone, tablet, and desktop with sample entries; verify that unauthorized visitors cannot view content.
7. Deploy with HTTPS, enable backups, and print a QR code for the Christmas card.

## Suggested print-book structure
- Cover: *Our Stories, Our Lives*
- Dedication and family tree (optional)
- 12 chapter dividers
- Each weekly question followed by both grandparents' responses
- Photographs, captions and selected family recipes
- Closing messages and an index of names/places

## Project calendar
Week 1 opens 2026-12-25. Week 52 opens 2027-12-17.
