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

var script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'https://openapi.map.naver.com/openapi/v3/maps.js?ncpClientId=jncgbf3ald';
document.head.appendChild(script);

// 지도 API가 로드된 후 실행할 함수를 정의
script.onload = function() {
    var map = new naver.maps.Map('map', {
        center: new naver.maps.LatLng(37.5665, 126.9780), // 서울을 초기 지도 중심으로 설정
        zoom: 10
    });

    window.searchAddress = function() {
        var address = document.getElementById('addressInput').value;

        naver.maps.Service.geocode({query: address}, function(status, response) {
            if (status !== naver.maps.Service.Status.OK) {
                alert('주소 검색에 실패했습니다.');
                return;
            }

            var result = response.v2.addresses[0];
            var point = new naver.maps.Point(result.x, result.y);

            map.setCenter(point);

            var marker = new naver.maps.Marker({
                position: point,
                map: map
            });

            // 마커 클릭 시 건축물 정보 표시
            naver.maps.Event.addListener(marker, 'click', function() {
                loadBuildingInfo(result);
            });
        });
    }

    function loadBuildingInfo(address) {
        var infoWindow = new naver.maps.InfoWindow({
            content: '<div style="padding:10px;min-width:200px;line-height:150%;">' +
                     '<h4>건축물 정보</h4>' +
                     '<p>주소: ' + address.roadAddress + '</p>' +
                     '<p>건축물 대장 정보를 불러옵니다...</p>' +
                     '</div>'
        });

        infoWindow.open(map, new naver.maps.Point(address.x, address.y));
    }
}
