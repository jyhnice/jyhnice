<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>네이버 지도 API 예제</title>
    <!-- CSS 파일 로드 -->
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <input type="text" id="addressInput" placeholder="주소를 입력하세요">
    <button onclick="searchAddress()">검색</button>
    <div id="map" style="width:100%;height:400px;margin-top:10px;"></div>
    <div id="info"></div>
    
    <!-- JavaScript 파일 로드 -->
    <script src="script.js"></script>
</body>
</html>
