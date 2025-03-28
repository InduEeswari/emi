<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EMI Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f5f5f5;
            margin: 0;
        }
        .container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            text-align: center;
            width: 90%;
            max-width: 400px;
            transition: all 0.3s ease;
            border: 4px solid transparent;
            box-shadow: 0 0 10px rgba(128, 0, 255, 0.7);
        }
        .container:hover {
            
            box-shadow: 0 0 15px rgba(51, 255, 0, 0.7);
        }
        input, button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            background: #6a28a7;
            color: white;
            border: none;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        button:hover {
            background: #3c00ff;
            box-shadow: 0 0 10px rgba(255, 69, 0, 0.7);
        }
        .result {
            margin-top: 20px;
            font-weight: bold;
        }
        @media screen and (min-width: 768px) {
            .container {
                max-width: 600px;
                padding: 30px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>EMI Calculator</h2>
        <input type="number" id="loanAmount" placeholder="Loan Amount">
        <input type="number" id="interestRate" placeholder="Annual Interest Rate (%)">
        <input type="number" id="loanTenure" placeholder="Loan Tenure (years)">
        <button onclick="calculateEMI()">Calculate EMI</button>
        <div class="result" id="emiResult"></div>
    </div>

    <script>
        function calculateEMI() {
            let loanAmount = parseFloat(document.getElementById('loanAmount').value);
            let annualInterestRate = parseFloat(document.getElementById('interestRate').value);
            let loanTenure = parseInt(document.getElementById('loanTenure').value) * 12;
            
            if (isNaN(loanAmount) || isNaN(annualInterestRate) || isNaN(loanTenure) || loanAmount <= 0 || annualInterestRate <= 0 || loanTenure <= 0) {
                document.getElementById('emiResult').innerHTML = "Please enter valid inputs.";
                return;
            }

            let monthlyInterestRate = annualInterestRate / 12 / 100;
            let emi = (loanAmount * monthlyInterestRate * Math.pow(1 + monthlyInterestRate, loanTenure)) / (Math.pow(1 + monthlyInterestRate, loanTenure) - 1);
            let totalPayment = emi * loanTenure;
            let totalInterest = totalPayment - loanAmount;

            document.getElementById('emiResult').innerHTML = 
                `EMI: ₹${emi.toFixed(2)}<br>
                 Total Interest Payable: ₹${totalInterest.toFixed(2)}<br>
                 Total Payment: ₹${totalPayment.toFixed(2)}`;
        }
    </script>
</body>
</html>
