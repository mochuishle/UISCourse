# Under Construction

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Anywhere on Earth Time</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

        body {
            font-family: 'Montserrat', sans-serif;
        }

        .container {
            text-align: left;
        }

        h1 {
            margin-bottom: 0;
        }

        .time {
            font-size: 7rem;
            font-weight: bold;
            margin: 0;
            text-align: center;
        }

        .date {
            font-size: 1.5rem;
            margin: 0;
            text-align: right;
        }

        .locations {
            display: flex;
            justify-content: right;
            gap: 1rem;
            font-size: 0.8rem;
            margin-top: 0.5rem;
        }

        .location {
            display: flex;
            flex-direction: column;
            align-items: flex-end;
            padding-right: 15px;
            background-color: rgba(0, 0, 0, 0.1);
            border-radius: 3px;
            box-shadow: 0 0px 0px rgba(0, 0, 0, 0.2);
            width: 130px;
            height: 60px;
            justify-content: center;
        }

        .location span {
            font-size: 0.6rem;
        }

        .location strong {
            font-size: 0.6rem;
        }
    </style>
    <script>
        function updateTime() {
            const now = new Date();
            const aoeOffset = -12;
            const aoeTime = new Date(now.getTime() + aoeOffset * 3600 * 1000);

            const hours = aoeTime.getUTCHours();
            const minutes = aoeTime.getUTCMinutes().toString().padStart(2, '0');
            const seconds = aoeTime.getUTCSeconds().toString().padStart(2, '0');
            const ampm = hours >= 12 ? 'pm' : 'am';
            const displayHours = (hours % 12 || 12).toString();

            document.getElementById('time').textContent = `${displayHours.padStart(2, '0')}:${minutes}:${seconds} ${ampm}`;

            updateLocationTime("new-york", -5);
            updateLocationTime("london", 0);
            updateLocationTime("paris", 1);
            updateLocationTime("beijing", 8);
            updateLocationTime("tokyo", 9);
        }

        function updateDate() {
            const now = new Date();
            const aoeOffset = -12;
            const aoeTime = new Date(now.getTime() + aoeOffset * 3600 * 1000);

            const formattedDate = aoeTime.toLocaleDateString('en-US', {
                weekday: 'long',
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            });
            document.getElementById('date').textContent = formattedDate;
        }

        function updateLocationTime(locationId, utcOffset) {
            const now = new Date();
            const localTime = new Date(now.getTime() + utcOffset * 3600 * 1000);

            const hours = localTime.getUTCHours().toString().padStart(2, '0');
            const minutes = localTime.getUTCMinutes().toString().padStart(2, '0');
            const ampm = localTime.getUTCHours() >= 12 ? 'pm' : 'am';
            const displayHours = (localTime.getUTCHours() % 12 || 12).toString();
            const formattedDate = localTime.toLocaleDateString('en-US', { month: 'short', day: 'numeric' });

            document.getElementById(locationId).textContent = `${displayHours}:${minutes}${ampm}, ${formattedDate}`;
        }

        function init() {
            updateTime();
            updateDate();
            setInterval(updateTime, 1000);
        }

        document.addEventListener('DOMContentLoaded', init);
    </script>
</head>
<body>
    <div class="container">
        <h1><span style="font-weight: Bold;">Anywhere on Earth </span>now</h1>
        <p class="time" id="time">03:56:20 am</p>
        <p class="date" id="date">Saturday, February 1</p>
        <div class="locations">
            <div class="location">
                <strong>New York</strong>
                <span id="new-york">10:56am, Feb 1</span>
            </div>
            <div class="location">
                <strong>London</strong>
                <span id="london">03:56pm, Feb 1</span>
            </div>
            <div class="location">
                <strong>Paris</strong>
                <span id="paris">04:56pm, Feb 1</span>
            </div>
            <div class="location">
                <strong>Beijing</strong>
                <span id="beijing">11:56pm, Feb 1</span>
            </div>
            <div class="location">
                <strong>Tokyo</strong>
                <span id="tokyo">12:56am, Feb 1</span>
            </div>
        </div>
    </div>
</body>
</html>


<!-- ![人机交互与虚拟现实](under.png) -->  