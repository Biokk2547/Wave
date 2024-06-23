<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>โปรแกรมคำนวณความเร็วคลื่น</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
        }
        h1 {
            color: #333;
        }
        .container {
            max-width: 600px;
            margin: auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 8px;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
        }
        .form-group input, .form-group select {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
            margin-bottom: 10px;
        }
        .form-group button {
            padding: 10px 15px;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        .form-group button:hover {
            background-color: #0056b3;
        }
        .result {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>โปรแกรมคำนวณความเร็วคลื่น</h1>
        <div class="form-group">
            <label for="wavelength">ความยาวคลื่น:</label>
            <input type="number" id="wavelength" step="0.01" placeholder="ใส่ความยาวคลื่น">
            <select id="wavelengthUnit">
                <option value="m">เมตร (m)</option>
                <option value="cm">เซนติเมตร (cm)</option>
                <option value="mm">มิลลิเมตร (mm)</option>
            </select>
        </div>
        <div class="form-group">
            <label for="frequency">ความถี่ของคลื่น:</label>
            <input type="number" id="frequency" step="0.01" placeholder="ใส่ความถี่ของคลื่น">
            <select id="frequencyUnit">
                <option value="Hz">เฮิร์ตซ์ (Hz)</option>
                <option value="kHz">กิโลเฮิร์ตซ์ (kHz)</option>
                <option value="MHz">เมกะเฮิร์ตซ์ (MHz)</option>
            </select>
        </div>
        <div class="form-group">
            <button onclick="calculateWaveSpeed()">คำนวณความเร็วคลื่น</button>
        </div>
        <div class="result">
            <p id="speedResult">ความเร็วคลื่น: </p>
            <p id="periodResult">คาบของคลื่น: </p>
            <p id="reflectionResult">มุมสะท้อน: </p>
            <p id="soundSpeedResult">ความเร็วเสียงในอากาศ: </p>
            <p id="planeSpeedResult">ความเร็วเครื่องบิน: </p>
        </div>
    </div>
    <script>
        function calculateWaveSpeed() {
            let wavelength = parseFloat(document.getElementById('wavelength').value);
            let wavelengthUnit = document.getElementById('wavelengthUnit').value;
            let frequency = parseFloat(document.getElementById('frequency').value);
            let frequencyUnit = document.getElementById('frequencyUnit').value;

            if (wavelengthUnit === 'cm') {
                wavelength /= 100;
            } else if (wavelengthUnit === 'mm') {
                wavelength /= 1000;
            }

            if (frequencyUnit === 'kHz') {
                frequency *= 1000;
            } else if (frequencyUnit === 'MHz') {
                frequency *= 1000000;
            }

            let speed = wavelength * frequency;
            speed = speed.toFixed(2);

            document.getElementById('speedResult').innerText = 'ความเร็วคลื่น: ' + speed + ' เมตรต่อวินาที';

            let period = (1 / frequency).toFixed(3);

            document.getElementById('periodResult').innerText = 'คาบของคลื่น: ' + period + ' วินาทีต่อรอบ';

            if (period >= 5) {
                alert('ช้ามากไอน้อง');
            } else {
                alert('ข้าคือความเร็ว');
            }

            let reflectionAngle = parseFloat(prompt("มุมตกกระทบ (องศา):"));
            document.getElementById('reflectionResult').innerText = 'มุมสะท้อน: ' + reflectionAngle + ' องศา';

            let temperature = parseFloat(prompt("อุณหภูมิ (°C):"));
            let waveSoundSpeed = 331 + (temperature * 0.6);
            waveSoundSpeed = waveSoundSpeed.toFixed(2);
            document.getElementById('soundSpeedResult').innerText = 'ความเร็วเสียงในอากาศ: ' + waveSoundSpeed + ' เมตรต่อวินาที';

            let angleDeg = parseFloat(prompt("มุมเงยมองเครื่องบิน (องศา):"));
            let sinValue = Math.sin(angleDeg * Math.PI / 180);
            let planeSpeed = waveSoundSpeed / sinValue;
            planeSpeed = planeSpeed.toFixed(3);
            document.getElementById('planeSpeedResult').innerText = 'ความเร็วเครื่องบิน: ' + planeSpeed + ' เมตรต่อวินาที';
        }
    </script>
</body>
</html>
