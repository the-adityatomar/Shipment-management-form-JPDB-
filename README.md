# Shipment Management Form (JPDB + jQuery + Bootstrap)

This project is a web-based Shipment Management Form that allows users to add, update, and manage shipment records using the JsonPowerDB (JPDB) REST API. It is built using HTML, jQuery, and Bootstrap 5.3.7, and is fully functional with real-time data operations.
<br><br><br><br>

![Screenshot 2025-06-26 181034](https://github.com/user-attachments/assets/eea87a0b-8b43-4dcb-97e1-171125045268)
<br><br><br><br>
## ✨Features


🔍 Search by Shipment Number (primary key)
<br>
✅ Form Validation — prevents submission with missing or invalid data

🧠 Delivery Date Check — ensures delivery date is not earlier than shipping date

💾 Save and ✏️ Update shipment records using JPDB's PUT and UPDATE operations

🔄 Reset the form to enter a new record

🎨 Responsive Bootstrap layout for clean UI
<br><br>

## 🧾Fields
<br>

👉Shipment No. (Primary Key)

👉Description

👉Source

👉Destination

👉Shipping Date

👉Expected Delivery Date

<br><br>

## 🔌Technologies Used

<br>
👉JsonPowerDB (JPDB) for backend database

👉HTML5 and jQuery for dynamic interaction

👉Bootstrap 5.3.7 for styling and layout

👉Custom JavaScript for client-side validation and API integration

<br><br>

## ⚙️How It Works
<br>

👉Enter a Shipment No.

👉If it exists, the form is auto-filled and the Update button is shown.

👉If not, the Save button is enabled to add a new shipment.

👉All data is validated before being submitted to the backend using JPDB API calls.

<br><br>


## 📁Use Case
<br>
👉Ideal for small-scale logistics, delivery tracking apps, or demo projects using JsonPowerDB.


