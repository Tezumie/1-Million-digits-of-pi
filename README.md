# 1-Million-digits-of-pi
A comprehensive JSON structure for a π (Pi), including one million decimal place values.


Easy and quick access to 1 million digits of PI with or without space every 10 decimal places.

Full application example;

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fetch First 100 Digits of Pi</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        #result {
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <h2>Fetch First 100 Digits of Pi</h2>
    <p>Click the button to fetch the first 100 digits of pi from the JSON file.</p>
    <button onclick="fetchPiData()">Fetch 100 Digits</button>

    <div id="result">
        <h3>Formatted (with spaces every 10 digits):</h3>
        <p id="formatted"></p>
        
        <h3>Unformatted (no spaces):</h3>
        <p id="unformatted"></p>
    </div>

    <script>
        async function fetchPiData() {
            try {
                const response = await fetch('https://raw.githubusercontent.com/Tezumie/1-Million-digits-of-pi/refs/heads/main/pi.json');
                
                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }
                
                const data = await response.json();
                
                // Access the nested million_decimals and million_decimals_with_spaces attributes
                const formattedPi = data.pi.basic_approximations.million_decimals_with_spaces;
                const unformattedPi = data.pi.basic_approximations.million_decimals;
                
                // Get the first 100 digits from each version
                const formattedDigits = formattedPi.replace(/\s+/g, '').slice(0, 100).match(/.{1,10}/g).join(' ');
                const unformattedDigits = unformattedPi.slice(0, 100);
                
                // Display results
                document.getElementById('formatted').innerText = formattedDigits;
                document.getElementById('unformatted').innerText = unformattedDigits;
                
            } catch (error) {
                console.error('Error fetching pi data:', error);
                document.getElementById('result').innerText = 'Failed to fetch data. Please try again later.';
            }
        }
    </script>

</body>
</html>
```
