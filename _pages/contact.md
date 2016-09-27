---
layout: single
title: Contact
permalink: /contact/
author_profile: true
header:
  overlay_color: "#5e616c"
  overlay_image: bg.jpg
---

<body>
  <form action="https://formspree.io/chambrierg@gmail.com" method="POST">
       Name:
       <input type="text" name="Guillaume de Chambrier">
       Email:
       <input type="email" name="_replyto">
       Message:
       <textarea name="message"></textarea>
      <input type="submit" value="Send">
  </form>
</body>


# I AM HERE

<div id="map-canvas" style="width:100%; height:650px"></div>
<script src="https://maps.googleapis.com/maps/api/js?v=3.exp"></script>

<script>

var markers = [{
  "latitude": 46.5196535,
  "longitude": 6.632,
  "title": "Wellington Outlet"
}];

	function initializeMap() {
		var bounds = new google.maps.LatLngBounds(),
			mapOptions = {
				mapTypeId: 'roadmap',
				styles: [{"featureType":"water","elementType":"geometry","stylers":[{"visibility":"on"},{"color":"#aee2e0"}]},{"featureType":"landscape","elementType":"geometry.fill","stylers":[{"color":"#abce83"}]},{"featureType":"poi","elementType":"geometry.fill","stylers":[{"color":"#769E72"}]},{"featureType":"poi","elementType":"labels.text.fill","stylers":[{"color":"#7B8758"}]},{"featureType":"poi","elementType":"labels.text.stroke","stylers":[{"color":"#EBF4A4"}]},{"featureType":"poi.park","elementType":"geometry","stylers":[{"visibility":"simplified"},{"color":"#8dab68"}]},{"featureType":"road","elementType":"geometry.fill","stylers":[{"visibility":"simplified"}]},{"featureType":"road","elementType":"labels.text.fill","stylers":[{"color":"#5B5B3F"}]},{"featureType":"road","elementType":"labels.text.stroke","stylers":[{"color":"#ABCE83"}]},{"featureType":"road","elementType":"labels.icon","stylers":[{"visibility":"off"}]},{"featureType":"road.local","elementType":"geometry","stylers":[{"color":"#A4C67D"}]},{"featureType":"road.arterial","elementType":"geometry","stylers":[{"color":"#9BBF72"}]},{"featureType":"road.highway","elementType":"geometry","stylers":[{"color":"#EBF4A4"}]},{"featureType":"transit","stylers":[{"visibility":"off"}]},{"featureType":"administrative","elementType":"geometry.stroke","stylers":[{"visibility":"on"},{"color":"#87ae79"}]},{"featureType":"administrative","elementType":"geometry.fill","stylers":[{"color":"#7f2200"},{"visibility":"off"}]},{"featureType":"administrative","elementType":"labels.text.stroke","stylers":[{"color":"#ffffff"},{"visibility":"on"},{"weight":4.1}]},{"featureType":"administrative","elementType":"labels.text.fill","stylers":[{"color":"#495421"}]},{"featureType":"administrative.neighborhood","elementType":"labels","stylers":[{"visibility":"off"}]}]
			};

		// Display a map on the page
		var map = new google.maps.Map(document.getElementById("map-canvas"), mapOptions);
		map.setTilt(45);

		for (var i = 0; i < markers.length; i++ ) {
			var position = new google.maps.LatLng(markers[i].latitude, markers[i].longitude);
			bounds.extend(position);
			marker = new google.maps.Marker({
				position: position,
				map: map,
				title: markers[i].title
			});

			// Automatically center the map fitting all markers on the screen
			map.fitBounds(bounds);
		}

		// Override our map zoom level once our fitBounds function runs (Make sure it only runs once)
		var boundsListener = google.maps.event.addListener((map), 'bounds_changed', function(event) {
			this.setZoom(5);
			google.maps.event.removeListener(boundsListener);
		});
	}

	google.maps.event.addDomListener(window, 'load', initializeMap);
</script>