<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Energy Consumption Calculator</title>
<style>
    body {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background-color: #f4f4f4;
        margin: 0;
        padding: 0;
    }
    .container {
        max-width: 600px;
        margin: 50px auto;
        padding: 20px;
        border-radius: 10px;
        background-color: #fff;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    h1 {
        text-align: center;
        color: #333;
        margin-bottom: 20px;
    }
    label {
        display: block;
        margin-bottom: 10px;
        color: #666;
    }
    input, select, button {
        width: 100%;
        padding: 12px;
        margin-bottom: 20px;
        border: 1px solid #ccc;
        border-radius: 5px;
        box-sizing: border-box;
        font-size: 16px;
    }
    button {
        background-color: #007bff;
        color: #fff;
        cursor: pointer;
    }
    button:hover {
        background-color: #0056b3;
    }
    #result {
        margin-top: 20px;
        padding: 20px;
        border-radius: 5px;
        background-color: #f9f9f9;
        font-size: 16px;
    }
    .result-item {
        margin-bottom: 10px;
    }
    .result-label {
        font-weight: bold;
    }
    .result-value {
        float: right;
    }
    .error {
        color: #ff0000;
        margin-top: 5px;
    }

    /* Media query for mobile screens */
    @media only screen and (max-width: 600px) {
        .container {
            padding: 10px;
        }
    }
</style>
</head>
<body>

<div class="container">
    <h1>Energy Consumption Calculator</h1>
    <form id="calculator-form">
        <label for="energy-board">Select Energy Board (APEPDCL):</label>
        <select id="energy-board" name="energy-board">
            <option value="APEPDCL">APEPDCL</option>
        </select>
        <label for="meter-number">Enter Energy Meter Number (16 digits):</label>
        <input type="text" id="meter-number" name="meter-number" placeholder="Enter meter number...">
        <label for="previous-reading">Enter Previous Reading:</label>
        <input type="number" id="previous-reading" name="previous-reading" placeholder="Enter previous reading...">
        <label for="current-reading">Enter Current Reading:</label>
        <input type="number" id="current-reading" name="current-reading" placeholder="Enter current reading...">
        <button type="button" id="calculate-btn">Calculate Consumption</button>
        <div id="error-message" class="error"></div>
    </form>
    <div id="result"></div>
</div>

<script>
    document.getElementById('calculate-btn').addEventListener('click', function() {
        var previousReading = parseFloat(document.getElementById('previous-reading').value);
        var currentReading = parseFloat(document.getElementById('current-reading').value);
        var meterNumber = document.getElementById('meter-number').value;
        
        // Check if meter number is 16 digits
        if (meterNumber.length !== 16) {
            document.getElementById('error-message').innerHTML = "Meter number must be 16 digits.";
            return;
        } else {
            document.getElementById('error-message').innerHTML = "";
        }

        // Check if previous reading is less than current reading
        if (previousReading >= currentReading) {
            document.getElementById('error-message').innerHTML = "Previous reading must be less than current reading.";
            return;
        } else {
            document.getElementById('error-message').innerHTML = "";
        }

        var unitsConsumed = currentReading - previousReading;
        var energyCharges = unitsConsumed * 3.12;
        var fixedCharges = 10;
        var customerCharges = 45;
        var edCharges = 6.36;
        var totalCharges = energyCharges + fixedCharges + customerCharges + edCharges;
        var resultMessage = "<div class='result-item'><span class='result-label'>Units Consumed:</span><span class='result-value'>" + unitsConsumed + "</span></div>";
        resultMessage += "<div class='result-item'><span class='result-label'>Energy Charges:</span><span class='result-value'>₹" + energyCharges.toFixed(2) + "</span></div>";
        resultMessage += "<div class='result-item'><span class='result-label'>Fixed Charges:</span><span class='result-value'>₹" + fixedCharges.toFixed(2) + "</span></div>";
        resultMessage += "<div class='result-item'><span class='result-label'>Customer Charges:</span><span class='result-value'>₹" + customerCharges.toFixed(2) + "</span></div>";
        resultMessage += "<div class='result-item'><span class='result-label'>ED Charges:</span><span class='result-value'>₹" + edCharges.toFixed(2) + "</span></div>";
        resultMessage += "<div class='result-item' style='font-size: 18px; font-weight: bold; margin-top: 10px;'>Total Charges: ₹" + totalCharges.toFixed(2) + "</div>";
        document.getElementById('result').innerHTML = resultMessage;
    });
</script>

</body>
</html>
