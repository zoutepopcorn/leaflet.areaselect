var map;
var test = "aaa";
var isSelect = false;
var select = [];


var selectStyle = L.divIcon({ 
    iconSize: new L.Point(0, 0), 
    html: '<div class="circle selector"></div><div class="clickable"></div>'
});

L.Map.mergeOptions({
  colors: []  // TODO
});

L.Map.addInitHook(function () {
  map = this;
});


L.Map.include({
  setSelect: function(state) {
      isSelect = state;
      map.on('click', function(e) {
        console.log("Kliiiik" + test);
        onMapClick(e);
      });
  },
  getBounds: function() {
    return ""; // TODO return the bounds
  }
});

function onMapClick(e) {
    if(isSelect) { 
        l = select.length;
        if(l < 2) {
            select[l] = L.marker([e.latlng.lat, e.latlng.lng], {icon: selectStyle, draggable: true});        
            select[l].addTo(map);
            select[l].id = l;
            select[l].on('drag', dragBox);
            if(l == 1) {
                coord1 = select[0].getLatLng();
                coord2 = select[1].getLatLng();
                // Marker 1
                l = select.length;
                select[l] = L.marker([coord1.lat, coord2.lng], {icon: selectStyle, draggable: true});        
                select[l].id = l;
                select[l].on('drag', dragBox);
                select[l].addTo(map);
                // Marker 2
                l = select.length;
                select[l] = L.marker([coord2.lat, coord1.lng], {icon: selectStyle, draggable: true});        
                select[l].id = l;
                select[l].on('drag', dragBox);
                select[l].addTo(map); 
                
                
                var polygon = L.polygon(
                    [[coord1.lat, coord1.lng],
                     [coord2.lat, coord1.lng],
                     [coord2.lat, coord2.lng],
                     [coord1.lat, coord2.lng]]);
                polygon.addTo(map);
                l = select.length;
                select[l] = polygon;
		//$('#header').html($('#downBut').clone());
		//console.log($('#downBut'));
		//$('#header').trigger('create');
            }
        } 
        console.log("You clicked the map at " + e.latlng.lat + " - " +e.latlng.lat);
        console.log(map.getZoom());
    }
}

function dragBox(e, map) {
    id = e.target.id;
    coord1 = select[id].getLatLng();
    console.log("LAT: " + coord1.lat);
    // Id's van de box markers
    //   0 ------ 2
    //   |        |
    //   3 ------ 1
    // vierkant zelf: 4
    if(id == 0) {  // update 2 en 3
        select[2].setLatLng(new L.LatLng(coord1.lat, select[2].getLatLng().lng));  // u: lat
        select[3].setLatLng(new L.LatLng(select[3].getLatLng().lat, coord1.lng));  // u: lng
    }
    if(id == 2) {  // update 0 en 1
        select[0].setLatLng(new L.LatLng(coord1.lat, select[0].getLatLng().lng));  // u: lat 
        select[1].setLatLng(new L.LatLng(select[1].getLatLng().lat, coord1.lng));  // u: lng
    }
    if(id == 3) {  // update 0 en 1
        select[1].setLatLng(new L.LatLng(coord1.lat, select[1].getLatLng().lng));  // u: lat 
        select[0].setLatLng(new L.LatLng(select[0].getLatLng().lat, coord1.lng));  // u: lng
    }
    if(id == 1) {  // update 2 en 3
        select[3].setLatLng(new L.LatLng(coord1.lat, select[3].getLatLng().lng));  // u: lat
        select[2].setLatLng(new L.LatLng(select[2].getLatLng().lat, coord1.lng));  // u: lng
    }
    // update poly
    coord1 = select[0].getLatLng();
    coord2 = select[1].getLatLng();
    coords = [[coord1.lat, coord1.lng],
	      [coord2.lat, coord1.lng],
	      [coord2.lat, coord2.lng],
	      [coord1.lat, coord2.lng]];
    select[4].setLatLngs(coords);
}
