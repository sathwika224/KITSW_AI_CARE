# KITSW AI CARE
Smart Campus Intelligence and Predictive Analytics Platform

## Main features
- Dashboard closely styled after the supplied KITSW AI CARE reference image
- KITSW branding/logo area at the top
- 13 campus problem modules
- Complaint registration from every problem card
- Automatic department/authority assignment
- Complaint ID generation
- Complaint status tracking
- Authority dashboard for updating complaint status
- CSV storage for complaints and campus datasets
- Campus insights and simple ML predictive analytics
- Reports and CSV downloads
- Responsive Streamlit interface

## Run
```powershell
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

If `streamlit run app.py` is not recognized in PowerShell, use:
```powershell
python -m streamlit run app.py
```

## Data
The included campus datasets are synthetic/demo data for project development and demonstration.
Replace them with authorized institutional data before making real operational decisions.

## Important files
- `app.py` - complete Streamlit application
- `data/complaints.csv` - registered complaints
- `data/authorities.csv` - department/authority mapping
- `data/*.csv` - campus datasets
- `assets/kitsw_logo.svg` - editable KITSW-style logo asset

## Complaint workflow
1. Select a problem area from Home.
2. Fill the complaint form.
3. System creates a complaint ID.
4. System automatically assigns the complaint to the mapped department/authority.
5. Track the complaint using the complaint ID.
6. Authority can update status from Department Routing.

## User and Administrator Access
- **User Login/Signup:** users can create an account and view only complaints linked to their email in **My Complaints**.
- **Administrator Login/Signup:** administrators use the official authority contact email and are linked to one authority. **My Assigned Problems** shows complaints routed to that authority and allows status/remarks updates.
- **Dashboard Access:** Home and the sidebar provide separate User and Administrator login/signup entry points.
- The KITSW campus image in `assets/kitsw_campus.jpg` is used as the dashboard background without removing the existing dashboard modules.

## Email notification system
The project now sends email notifications to BOTH sides of a complaint:
1. **User/complainant** — confirmation, complaint ID, assigned authority, current status and expected resolution time.
2. **Assigned administrator/authority** — new complaint assignment and every status update.

Emails are sent through SMTP and are controlled by environment variables; no email password is stored in the project CSV files. Delivery attempts are logged in `data/email_notifications.csv`.

### Configure Gmail SMTP on Windows PowerShell
Use a Gmail App Password for `KITSW_SMTP_PASSWORD` (enable 2-Step Verification on the Gmail account first). Then run:

```powershell
$env:KITSW_SMTP_HOST="smtp.gmail.com"
$env:KITSW_SMTP_PORT="587"
$env:KITSW_SMTP_USER="your-email@gmail.com"
$env:KITSW_SMTP_PASSWORD="YOUR_APP_PASSWORD"
$env:KITSW_FROM_EMAIL="your-email@gmail.com"
streamlit run app.py
```

For a permanent Windows setup, use **System Properties → Environment Variables** instead of setting them only for the current PowerShell window.

### Notification workflow
**Complaint registered → automatic authority assignment → user + authority email → expected resolution date → authority updates status → user + authority status email → user tracks the complaint in the dashboard.**

The expected resolution period is initially estimated from priority: Critical = 1 day, High = 2 days, Medium = 4 days, Low = 7 days. These are configurable demonstration targets, not institutional SLAs.
