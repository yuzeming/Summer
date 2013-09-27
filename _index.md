---
layout: 
title: 实践小队主页
tagline: 
---
<html>
<head>
<title>中国IT版图调研实践主页 </title>
<link rel="stylesheet" href="./bootstrap/css/bootstrap.min.css">
<style type="text/css">
body {
	color: #CCCCCC;
	margin: 0px;
	background-image: url(./images/bg.png);
}
a {
	text-decoration: none;
}
#header{
	font-size: 25px;
	padding: 25px;
	text-align: center;
	height: 30px;
}
#allmap {
	text-align: center;
	height: 480px;
	overflow: hidden;
	margin:0;
}
#footer {
	text-align: center;
	padding: 25px;
	height: 60px;
}
.logo {width:100px;}
.intro {
	color: #333333;
	max-height: 500px;
}
</style>

</head>
<body>
<div id="header">
	中国IT版图调研
</div>
<div id="allmap">
	Loading Map...
</div>
<div id="footer">
	<button type="button" class="btn btn-success" onclick='showModal()'>支队简介</button>
	<a class="btn btn-info" role="button" href="categories.html">公司列表</a>
</div>

<div id="conModal" class="modal fade" aria-hidden="true" style="display:none">
	<div class="modal-dialog">
		<div class="modal-content">
			<div class="modal-body intro">
				<img src="./main.jpg"></img>
				       浙江杭州中国IT版图调研支队是计算机系团委的精品实践支队。支队由计算机系、软件学院、物理系的15位同学构成，有着较强的专业背景。同时，由不同性别、年级、专业的同学组成也使得支队有着较强的综合能力。支队将在七天的时间内，走访包括阿里巴巴在内的多家IT企业，与杭州IT产业界的风云人物对话。通过采访和实地调研，还原一个真实的杭州IT发展状况，以更加了解计算机信息产业的时代前沿和发展前景，对今后有意投身IT产业的同学起到良好的导向作用。
			</div>
		</div>
	</div>
</div>

<script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=9166a20402293fd2c5a30177f220f846"></script>
<script type="text/javascript" src="http://api.map.baidu.com/library/TextIconOverlay/1.2/src/TextIconOverlay_min.js"></script>
<script type="text/javascript" src="http://api.map.baidu.com/library/MarkerClusterer/1.2/src/MarkerClusterer_min.js"></script>
<script type="text/javascript" src="./map/map-data.js"></script>
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.0/jquery.min.js"></script>
<script type="text/javascript" src="./bootstrap/js/bootstrap.min.js"></script>

<script type="text/javascript">
//显示支队简介
function showModal() {
	$("#conModal").modal("show");
}

// 百度地图API功能
var map = new BMap.Map("allmap");
map.centerAndZoom(new BMap.Point(120, 30), 6);
map.enableScrollWheelZoom();

var markerArr = [];
var pt = null;
var infoWindow = null;
var marker = null;
for (i in mapdata) {
	pt = new BMap.Point(mapdata[i].x,mapdata[i].y);
	var sContent = new String("");
	for (j in mapdata[i].company) {
		sContent=sContent+"<a href='"+mapdata[i].company[j].url+"'>"+"<b>"+mapdata[i].company[j].name+"</b><br>"+"<img class='logo' src='map/"+mapdata[i].company[j].logo+"'></a><br>";
	}

	marker = new BMap.Marker(pt);
	marker.infoWindow = new BMap.InfoWindow(sContent);  

	marker.addEventListener("click", function(){          
			this.openInfoWindow(this.infoWindow);
			var mk = this;
			var logo = document.getElementsByClassName('logo');
			for (i in logo){
			logo[i].onload = function (){
			mk.infoWindow.redraw();   
			}
			}
			} )
	markerArr.push(marker);
}

//最简单的用法，生成一个marker数组，然后调用markerClusterer类即可。
var markerClusterer = new BMapLib.MarkerClusterer(map, {markers:markerArr});
</script>


</body>
</html>

