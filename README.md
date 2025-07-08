#### Book-Lending

Create your custom app locally
Push it to GitHub
Install it manually via Frappe Cloud.



Building a Book Lending app on Frappe + ERPNext is a practical way to learn custom app development within the ERPNext ecosystem. 

### Project Goal:

Create a **Book Lending System** where:

- Books can be added and tracked.
- Members can borrow books.
- Lending and return dates are recorded.
- Fine is optionally calculated if return is late.
- Reports can show current loans, overdue books, etc


### **Step 1: Create a Custom App**

```bash
bench new-app book_lending
# Provide:
# - App Name: book_lending
# - Publisher: your name/org
# - Description: A system for managing book loans
# - Email/License info as required

```

Then install it on your site:

```bash
bench --site [your-site-name] install-app book_lending

```

---

### **Step 2: Define the App Structure**

We'll need these **DocTypes**:

| DocType | Purpose |
| --- | --- |
| Book | Catalog of books |
| Member | People who can borrow books |
| Book Lending | Records of book loans |
| Book Return | Records of returns and fines |

If you want, we can extend ERPNext's **Customer** or **Employee** for Members, but to keep it clean, we’ll use custom DocTypes.

---

### **Step 3: Create DocTypes**

Use the following commands or the UI to scaffold:

### Create Book:

```bash
bench --site [your-site-name] console
# Inside console:
frappe.new_doc("DocType")
# Fill:
# - name: Book
# - module: Book Lending
# - fields: title, author, isbn, available_copies, total_copies, etc.

```

### Create Member:

Fields like name, email, membership_start_date.

### Create Book Lending:

Fields like:

- book (Link to Book)
- member (Link to Member)
- lending_date
- due_date
- status (e.g. Borrowed, Returned)

### Create Book Return:

- book_lending (Link to Book Lending)
- return_date
- fine_amount (if any)

Each DocType can have auto-naming, permissions, workflows if desired.

---

### **Step 4: Add Logic (Server Scripts or Python Hooks)**

Examples:

- **On Book Lending submit**: reduce available copies.
- **On Return**: mark book as available, calculate fine if overdue.

You can add logic via:

- `hooks.py`
- `validate`, `on_submit`, or `on_cancel` methods in Python
- OR Frappe Server Scripts for quick rules

---

### **Step 5: UI: Page, Report, or Dashboard**

- Add a **custom page** for “Lending Desk”.
- Add reports like:
    - “Overdue Books”
    - “Books Borrowed Per Member”
    - “Daily Lending Summary”

---

### **Step 6: Test the App**

- Create sample entries for books, members.
- Test borrow-return flows.
- Validate logic for fine calculation and book stock updates.

---

### Optional:

- Add **notifications** for due/overdue returns.
- Allow **QR code** scan for book returns.
- Add **email reminders**.