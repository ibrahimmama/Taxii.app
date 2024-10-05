<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>طلب أقرب سيارة</title>
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-database.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }
        #map {
            height: 400px;
            width: 100%;
        }
        button {
            margin-top: 20px;
            padding: 10px 20px;
            background-color: green;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <h1>طلب أقرب سيارة</h1>
    <div id="map"></div>
    <button id="requestRide">طلب أقرب سائق</button>
    <p id="output"></p>

    <script>
        // إعداد Firebase
        var firebaseConfig = {
            apiKey: "AIzaSyCow0kJbcJ7OUzaHOBqXp1hF1LPSxb6dBo",
            authDomain: "alnashme-tawsel.firebaseapp.com",
            databaseURL: "https://alnashme-tawsel-default-rtdb.firebaseio.com",
            projectId: "alnashme-tawsel",
            storageBucket: "gs://alnashme-tawsel.appspot.com",
            messagingSenderId: "76863416572",
            appId: "1:76863416572:android:e75569b3ef02142baf8f79"
        };
        firebase.initializeApp(firebaseConfig);
        var database = firebase.database();

        // طلب إذن تحديد الموقع
        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(showPosition, showError);
        } else {
            alert("المتصفح الخاص بك لا يدعم تحديد الموقع.");
        }

        function showPosition(position) {
            var latitude = position.coords.latitude;
            var longitude = position.coords.longitude;

            // إرسال الموقع إلى Firebase
            database.ref('requests').push({
                customerLocation: {
                    lat: latitude,
                    lng: longitude
                },
                status: "waiting"
            });

            // عرض الخريطة باستخدام API
            fetch(`https://api.opencagedata.com/geocode/v1/json?q=${latitude},${longitude}&key=afa6985b839946d6ab60715d07e2af2c`)
                .then(response => response.json())
                .then(data => {
                    const map = document.getElementById('map');
                    map.innerHTML = `<iframe width="100%" height="100%" src="https://maps.google.com/maps?q=${latitude},${longitude}&z=15&output=embed"></iframe>`;
                });
        }

        function showError(error) {
            switch (error.code) {
                case error.PERMISSION_DENIED:
                    alert("تم رفض طلب الوصول إلى الموقع.");
                    break;
                case error.POSITION_UNAVAILABLE:
                    alert("الموقع غير متوفر.");
                    break;
                case error.TIMEOUT:
                    alert("انتهت مهلة الحصول على الموقع.");
                    break;
                case error.UNKNOWN_ERROR:
                    alert("حدث خطأ غير معروف.");
                    break;
            }
        }

        // طلب أقرب سائق
        document.getElementById('requestRide').addEventListener('click', function() {
            alert('تم إرسال طلب السائق. يرجى الانتظار حتى يتم قبول الطلب.');
        });
    </script>
</body>
</html>
