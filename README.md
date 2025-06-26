# Shipment-management-form-JPDB-
This project is a web-based Shipment Management Form that allows users to add, update, and manage shipment records using the JsonPowerDB (JPDB) REST API. It is built using HTML, jQuery, and Bootstrap 3.4.1, and is fully functional with real-time data operations.

![Screenshot 2025-06-26 181034](https://github.com/user-attachments/assets/6cac2a3d-d4b1-4277-a230-56ff49932987)

 The code for the form is as follows:
 <!DOCTYPE html>
<html lang="en">

<head>
    <title>Shipment Management Form</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.7/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-LN+7fdVzj6u52u30Kp6M/trliBMCMKTyK833zpbD+pXdCLuTusPj697FH4R/5mcr" crossorigin="anonymous">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.7/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-ndDqU0Gzau9qJ1lfW4pNLlhNTkCfHzAVBReH9diLvGRem5+R9g2FzA8ZGN954O5Q"
        crossorigin="anonymous"></script>
    <script src="https://login2explore.com/jpdb/resources/js/0.0.4/jpdb-commons.js"></script>
</head>

<body>
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">Login2Xplore</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown"
                aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNavDropdown">
                <ul class="navbar-nav">
                    <li class="nav-item">
                        <a class="nav-link active" aria-current="page" href="#">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Features</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Pricing</a>
                    </li>
                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown"
                            aria-expanded="false">
                            Dropdown link
                        </a>
                        <ul class="dropdown-menu">
                            <li><a class="dropdown-item" href="#">Action</a></li>
                            <li><a class="dropdown-item" href="#">Another action</a></li>
                            <li><a class="dropdown-item" href="#">Something else here</a></li>
                        </ul>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
    <div class="container">
        <div class="page-header text-center">
            <h2>Shipment Management Form (JPDB)</h2>
        </div>

        <form id="shipmentForm">
            <div class="form-group">
                <label>Shipment No.:</label>
                <input type="text" class="form-control" id="shipNo" placeholder="Enter Shipment Number">
            </div>
            <div class="form-group">
                <label>Description:</label>
                <input type="text" class="form-control" id="description" placeholder="Enter Description">
            </div>
            <div class="form-group">
                <label>Source:</label>
                <input type="text" class="form-control" id="source" placeholder="Enter Source">
            </div>
            <div class="form-group">
                <label>Destination:</label>
                <input type="text" class="form-control" id="destination" placeholder="Enter Destination">
            </div>
            <div class="form-group">
                <label>Shipping Date:</label>
                <input type="date" class="form-control" id="shipDate">
            </div>
            <div class="form-group">
                <label>Expected Delivery Date:</label>
                <input type="date" class="form-control" id="deliveryDate">
            </div>

            <div class="form-group text-center gap-2 mt-3   ">
                <button type="button" class="btn btn-primary" id="saveBtn" onclick="saveShipment()"
                    disabled>Save</button>
                <button type="button" class="btn btn-warning" id="updateBtn" onclick="updateShipment()"
                    disabled>Update</button> 
                <button type="button" class="btn btn-danger" id="resetBtn" onclick="resetForm()" disabled>Reset</button>
            </div>
        </form>
    </div>

    <script>
        var jpdbBaseURL = "http://api.login2explore.com:5577";
        var jpdbIRL = "/api/irl";
        var jpdbIML = "/api/iml";
        var dbName = "DELIVERY-DB";
        var relName = "SHIPMENT-TABLE";
        var connToken = "90934551|-31949210137276090|90959020";

        $(document).ready(function () {
            $("#shipNo").on("input", function () {
                getShipment();
            });
        });

        function resetForm() {
            $("#shipNo, #description, #source, #destination, #shipDate, #deliveryDate").val("");
            $("#shipNo").prop("disabled", false);
            $("#saveBtn, #updateBtn, #resetBtn").prop("disabled", true);
            $("#shipNo").focus();
        }

        function validateData() {
            var shipNo = $("#shipNo").val();
            var desc = $("#description").val();
            var src = $("#source").val();
            var dest = $("#destination").val();
            var shipDate = $("#shipDate").val();
            var delDate = $("#deliveryDate").val();

            if (new Date(delDate) < new Date(shipDate)) {
        alert("Delivery date cannot be earlier than shipping date.");
        $("#deliveryDate").focus();
        return "";
    }

            if (shipNo === "") {
                alert("Shipment No. is required.");
                $("#shipNo").focus();
                return "";
            }
            if (desc === "") {
                alert("Description is required.");
                $("#description").focus();
                return "";
            }
            if (src === "") {
                alert("Source is required.");
                $("#source").focus();
                return "";
            }
            if (dest === "") {
                alert("Destination is required.");
                $("#destination").focus();
                return "";
            }
            if (shipDat = "") {
                alert("Shipping date is required.");
                $("#shipDate").focus();
                return "";
            }
            if (delDate === "") {
                alert("Delivery date is required.");
                $("#deliveryDate").focus();
                return "";
            }

            let jsonObj = {
                "Shipment-No.": shipNo,
                "Description": desc,
                "Source": src,
                "Destination": dest,
                "Shipping-Date": shipDate,
                "Expected-Delivery-Date": delDate
            };

            return JSON.stringify(jsonObj);
        }

        function getShipKeyAsJson() {
            let shipNo = $("#shipNo").val();
            return JSON.stringify({ "Shipment-No.": shipNo });
        }

        function saveRecNoToLS(resObj) {
            let data = JSON.parse(resObj.data);
            localStorage.setItem("recno", data.rec_no);
        }

        function fillForm(resObj) {
            saveRecNoToLS(resObj);
            let data = JSON.parse(resObj.data).record;
            $("#description").val(data["Description"]);
            $("#source").val(data["Source"]);
            $("#destination").val(data["Destination"]);
            $("#shipDate").val(data["Shipping-Date"]);
            $("#deliveryDate").val(data["Expected-Delivery-Date"]);
        }

        function getShipment() {
            var key = getShipKeyAsJson();
            var getReq = createGET_BY_KEYRequest(connToken, dbName, relName, key);

            jQuery.ajaxSetup({ async: false });
            var result = executeCommandAtGivenBaseUrl(getReq, jpdbBaseURL, jpdbIRL);
            jQuery.ajaxSetup({ async: true });

            if (result.status === 400) {
                $("#saveBtn").prop("disabled", false);
                $("#resetBtn").prop("disabled", false);
                $("#description").focus();
            } else if (result.status === 200) {
                $("#shipNo").prop("disabled", true);
                fillForm(result);
                $("#updateBtn").prop("disabled", false);
                $("#resetBtn").prop("disabled", false);
                $("#description").focus();
            } else {
                alert("Unexpected response. Status: " + result.status);
            }
        }

        function saveShipment() {
            var jsonData = validateData();
            if (jsonData === "") return;

            var req = createPUTRequest(connToken, jsonData, dbName, relName);
            jQuery.ajaxSetup({ async: false });
            let result = executeCommandAtGivenBaseUrl(req, jpdbBaseURL, jpdbIML);
            jQuery.ajaxSetup({ async: true });

            alert("Shipment saved successfully.");
            resetForm();
        }

        function updateShipment() {
            var jsonData = validateData();
            if (jsonData === "") return;

            var recno = localStorage.getItem("recno");
            var req = createUPDATERecordRequest(connToken, jsonData, dbName, relName, recno);

            jQuery.ajaxSetup({ async: false });
            var result = executeCommandAtGivenBaseUrl(req, jpdbBaseURL, jpdbIML);
            jQuery.ajaxSetup({ async: true });

            alert("Shipment updated successfully.");
            resetForm();
        }
    </script>
</body>

</html>

✨ Features
🔍 Search by Shipment Number (primary key)
✅ Form Validation — prevents submission with missing or invalid data
🧠 Delivery Date Check — ensures delivery date is not earlier than shipping date
💾 Save and ✏️ Update shipment records using JPDB's PUT and UPDATE operations
🔄 Reset the form to enter a new record
🎨 Responsive Bootstrap layout for clean UI

🧾 Fields
👉Shipment No. (Primary Key)
👉Description
👉Source
👉Destination
👉Shipping Date
👉Expected Delivery Date

🔌 Technologies Used
👉JsonPowerDB (JPDB) for backend database
👉HTML5 and jQuery for dynamic interaction
👉Bootstrap 5.3.7 for styling and layout
👉Custom JavaScript for client-side validation and API integration

⚙️ How It Works
👉Enter a Shipment No.
👉If it exists, the form is auto-filled and the Update button is shown.
👉If not, the Save button is enabled to add a new shipment.
👉All data is validated before being submitted to the backend using JPDB API calls.

📁 Use Case
Ideal for small-scale logistics, delivery tracking apps, or demo projects using JsonPowerDB.
