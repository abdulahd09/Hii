# Hii
<!DOCTYPE html>
<html>
<head>
    <title>Big Small Predictor</title>
    <style>
        body {
            font-family: Arial;
            text-align: center;
            margin-top: 50px;
        }
        input {
            width: 40px;
            text-align: center;
            font-size: 18px;
            margin: 5px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            margin-top: 10px;
        }
        h2 {
            color: green;
        }
    </style>
</head>
<body>

<h1>Big / Small Predictor</h1>
<p>Enter from <b>5th last → last</b></p>

<input id="r1" maxlength="1" placeholder="B/S">
<input id="r2" maxlength="1" placeholder="B/S">
<input id="r3" maxlength="1" placeholder="B/S">
<input id="r4" maxlength="1" placeholder="B/S">
<input id="r5" maxlength="1" placeholder="B/S">

<br>
<button onclick="predict()">Predict</button>

<h2 id="result"></h2>

<script>
function predict() {
    let results = [
        document.getElementById("r1").value.toUpperCase(),
        document.getElementById("r2").value.toUpperCase(),
        document.getElementById("r3").value.toUpperCase(),
        document.getElementById("r4").value.toUpperCase(),
        document.getElementById("r5").value.toUpperCase()
    ];

    let last = results[4];

    // Count streak
    let streak = 1;
    for (let i = 3; i >= 0; i--) {
        if (results[i] === last) streak++;
        else break;
    }

    let prediction;

    // Rule 1: 3 same → reverse
    if (streak >= 3) {
        prediction = (last === "B") ? "S" : "B";
    } 
    else {
        // Rule 2: alternating
        let alternating = true;
        for (let i = 1; i < 5; i++) {
            if (results[i] === results[i - 1]) {
                alternating = false;
                break;
            }
        }

        if (alternating) {
            prediction = (last === "B") ? "S" : "B";
        } 
        else {
            // Rule 3: count
            let big = 0, small = 0;
            for (let r of results) {
                if (r === "B") big++;
                else if (r === "S") small++;
            }

            if (big > small) prediction = "B";
            else if (small > big) prediction = "S";
            else prediction = last;
        }
    }

    document.getElementById("result").innerText = "Next: " + prediction;
}
</script>

</body>
</html>
