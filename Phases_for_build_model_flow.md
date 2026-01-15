### **⚠️ UNIFIED NOTICE: Intellectual Property Protection**

**By accessing, viewing, or engaging with this document or any communication related to it, you acknowledge that all concepts, frameworks, terminologies, and systems described herein are the exclusive intellectual property of Spencer Southern and Southern Star Pro. Studios, LLC.**

Phase 1 build model flow;

✅ Good — based on what you just asked, I understand:

You want a **Step-by-Step Setup Guide** that **future Spencer** (or anyone under your guidance) could follow  
 **to rebuild exactly what you’ve done right now** — getting to the clean, working Phase I system without confusion.

I’ll match it carefully to your open document ("Mint To Phase1 Howitworks") — and I’ll add only the necessary steps based on your real live process today.

---

# **📜 Step-by-Step Setup Guide to Rebuild Mint-to Logic™™ Phase I**

---

# **✨ Mint-to Logic™™ Phase I: Step-by-Step Setup Guide**

## **🛠 Tools Needed:**

* **Make.com** account

* **Airtable** account

* **Basic Airtable table setup** with the following fields:

  * Full Name

  * Voter ID / Ballot Code

  * ZIP Code / Region

  * Email

  * Mint Unit ID™™ (Blank initially)

  * Status (Blank initially)

  * (Optional: Timestamp, Session ID)

---

## **⚙ Full Build Process:**

### **1\. Set Up the Airtable Table**

* Create an Airtable base.

* Add a table called `Mint Unit Issuance` (or similar).

* Add the fields:

  * `Full Name` (Single line text)

  * `Voter ID / Ballot Code` (Single line text)

  * `ZIP Code / Region` (Single line text)

  * `Email` (Email field or Single line text)

  * `Mint Unit ID™™` (Single line text, leave blank)

  * `Status` (Single select or text, leave blank)

---

### **2\. Create the Scenario in Make.com**

**A. Create New Scenario:**

* Add the **Custom Webhook** module:

  * Create a webhook.

  * Copy the webhook URL for use in your form or test submissions.

* Add the **Airtable – Create Record** module:

  * Connect Airtable account.

  * Select your base and table.

  * Map the Webhook fields to Airtable fields:

| Airtable Field | Webhook Mapping |
| ----- | ----- |
| Full Name | `{{Webhook.FullName}}` |
| Voter ID / Ballot Code | `{{Webhook.VoterID}}` |
| ZIP Code / Region | `{{Webhook.ZIPCode}}` |
| Email | `{{Webhook.Email}}` |
| (Leave Mint Unit ID™™ and Status blank) |  |

---

**B. Add the Compose a String module:**

* Add the **Tools – Compose a String** module.

* Use this formula exactly:

MINT--{{formatDate(now; "x")}}--{{substring(formatDate(now; "x"); \-5)}}

* This creates a unique Mint Unit™™ ID based on the current timestamp.

---

**C. Add the Airtable – Update Record module:**

* Add the **Airtable – Update Record** module.

* Link to the **Record ID** from the Create Record step.

* Update ONLY the following fields:

  * **Mint Unit ID™™:** (Use the output from Compose a String)

  * **Status:** (Set static value to `Issued`)

* Leave all other fields blank.

---

### **3\. Testing the Flow**

* Use a form or direct webhook test to send a user submission:

  * Full Name

  * Voter ID

  * ZIP

  * Email

* Trigger the webhook manually if needed for testing.

* Check Airtable:

  * Verify a new record is created with full user data.

  * After a few seconds, verify that Mint Unit ID™™ is filled in and Status is set to `Issued`.

  * Confirm no blank or overwritten fields.

---

## **🧠 Important Notes to Remember:**

| Topic | Rule |
| ----- | ----- |
| Compose a String | MUST use timestamp and substring — no random functions\! |
| Update Record module | ONLY update Mint Unit™™ and Status. |
| Webhook Setup | Always redetermine data structure after live test submission. |
| Airtable | Fields must exist before you map them in Make. |
| Testing | Always submit a real webhook test before finalizing mappings. |

---

# **✅ Outcome When Done:**

* Working webhook-to-Mint Unit™™ issuance system.

* Full user data securely stored at the first Create Record step.

* Mint Unit™™ added safely at the Update Record step.

* Status updated to `Issued`.

* System ready for Phase II (Burn Protocol).

---

# **📣 THIS IS YOUR OFFICIAL REBUILD GUIDE.**

It matches exactly how you got to where you are right now — without confusion, without skipping steps, and under **your guidance structure**.

---

Would you like me to **also add this as an official appendix at the bottom of your "Mint To Phase1 Howitworks" document** so it stays permanently recorded? 📜✨

If yes, just say:  
 **"Add Step-by-Step Guide to Document."**  
 and I’ll patch it in cleanly right now\! 🚀

# **📜 Phase II Build Plan (Live \- Ready for Action)**

---

### **⚙️ MODULES WE WILL ADD:**

| Step | Module | Purpose |
| ----- | ----- | ----- |
| 5 | **Webhook – Validation Webhook** | Catch scanned Mint Unit™™ from QR code. |
| 6 | **Airtable – Search Records** | Search Airtable for matching Mint Unit™™. |
| 7 | **Router – Logic Split** | Branch if Valid vs Invalid Mint Unit™™. |
| 8A | **Airtable – Update Record (Burn)** | If valid, set Status to `Burned`. |
| 8B | **Error Handler / Response** | If invalid, return an error message. |
| 9 | **(Optional) HTTP Response** | (Optional) Clean success/failure message back to scanner. |

---

# **📋 STEP-BY-STEP (Detailed Execution Plan)**

---

### **1\. Create Validation Webhook (Step 5\)**

✅ New webhook module in Make.com  
 ✅ Form Fields captured:

* `mint_unit_id`

* (Optional: `passphrase`)

* (Optional: `scanned_at_timestamp` — automatic)

✅ This is what your QR codes will hit when scanned.

---

### **2\. Search Airtable for Mint Unit ID (Step 6\)**

✅ Airtable module:

* Base: Your Mint Units table

* Search:

  * Field: `Mint Unit ID™™`

  * Value: incoming `mint_unit_id` from webhook

---

### **3\. Set Up Router (Step 7\)**

✅ Logic Split:

* If Airtable finds a record where:

  * `Status = Issued`

* ➔ Proceed to Burn the Mint Unit™™.

* Else:

  * ➔ Trigger Error/Reject Flow.

---

### **4\. Burn Mint Unit (Step 8A)**

✅ Airtable – Update Record:

* Set `Status = Burned`

* (Optional) Add fields:

  * `Validated By Device` (optional)

  * `Validation Timestamp`

---

### **5\. Return Error / Handle Invalid Scans (Step 8B)**

✅ If record not found or already Burned:

* Return Error:  
   `"Invalid Ticket."`  
   `"Ticket Already Used."`

---

### **6\. (Optional) Build HTTP Response (Step 9\)**

✅ Send clean JSON or webpage message to scanner:

* Success Message: `"Ticket Validated Successfully."`

* Failure Message: `"Ticket Invalid or Already Used."`

✅ This gives the scanner instant feedback without needing a manual lookup.

---

# **✅ RESULT OF PHASE II:**

| Condition | Result |
| ----- | ----- |
| Valid Mint Unit™™ Scanned | Mint Unit™™ is burned and ticket is validated. |
| Invalid or Burned Mint Unit™™ Scanned | Immediate rejection and fraud stopped. |

✅ QR codes destroyed by logic — not just visually.  
 ✅ Real-world \+ digital anti-fraud pipeline fully operational.

---

# **📣 NOW:**

Would you like me to **officially add this Phase II Build Plan** into your "Mint To Phase1 Howitworks" document now under a new heading:

### **🔥 Phase II – Full Build Instructions**

👉 (So you have your permanent record and blueprint ready to work from?)

If yes, just say:  
 **"Add Phase II Build Plan."** 📜🚀

(Then we can immediately start building module-by-module live.)  
 You're doing this like a master builder now. 🔥

