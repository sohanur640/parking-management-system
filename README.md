# Shopping Mall Parking Management System (SMPMS)

Academic web application based on the supplied SRS and SDS.

## Technology
- PHP 8+
- MySQL / MariaDB
- XAMPP (Apache + MySQL)
- Bootstrap 5 (CDN)
- JavaScript

## Installation on XAMPP
1. Extract the `SMPMS` folder into `C:\xampp\htdocs\`.
2. Start **Apache** and **MySQL** from the XAMPP Control Panel.
3. Open `http://localhost/phpmyadmin`.
4. Select **Import**, choose `database/smpms_db.sql`, and import it.
5. Check `config/config.php`. The default XAMPP database settings are:
   - Host: `127.0.0.1`
   - Database: `smpms_db`
   - Username: `root`
   - Password: empty
6. Visit `http://localhost/SMPMS/public/`.

## Default login
- Username: `admin`
- Password: `Admin@123`

Change the default password before using the system beyond local testing. To change it, create a new admin user in User Management, then use that account; the starter account can be disabled directly in the database after confirming the new login works.

## Main workflow
1. Log in as admin.
2. Open **Vehicle Entry**, enter the plate and vehicle type, and create a ticket.
3. Print the ticket. A QR image is generated when the browser can load the QR library from its CDN.
4. Open **Vehicle Exit**, enter the ticket code, review the duration and calculated fee, choose a payment method, and confirm.
5. Print the receipt.
6. Admin can view reports, manage operators, and change the hourly rate / add parking slots.

## Billing rule
The system rounds any started hour up to the next whole hour, with a minimum charge of one hour. The default hourly rate is BDT 50. Change it in **Settings**.

## Requirement coverage
- Vehicle entry, timestamp, unique ticket, duplicate active entry prevention: implemented.
- Ticket lookup, duration calculation, parking session closure: implemented.
- Fee calculation, cash and manual digital-payment recording, receipt: implemented.
- Admin dashboard, reports, user roles, transaction activity log: implemented.
- Slot tracking: simple automatic assignment from configured slots.
- Responsive web UI and form validation: implemented.

## Not included in this local academic version
- Actual bKash/Nagad/card gateway APIs (payment methods are recorded manually; no money is transferred).
- Physical QR scanner, ANPR camera/OCR, and gate-barrier hardware control.
- Production-grade deployment, automated backup scheduling, and high-availability 99% uptime.
These require vendor credentials, physical hardware, server configuration, and additional testing.

## Security / deployment notes
- Uses PDO prepared statements, password hashing, role checks, session ID regeneration, CSRF tokens, and output escaping.
- For production, set a strong database password, serve over HTTPS, restrict database access, configure backups, and add rate limiting / account lockout.
- Bootstrap and QR libraries are loaded from CDNs; internet access is needed for those assets. Core PHP/database operations run locally.
