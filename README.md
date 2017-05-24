<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <title>Oficina | Cigeracar </title>
        <meta content="text/html; charset=ISO-8859-1" http-equiv="Content-Type"/>
   
    <script
src="http://maps.google.com/maps?file=api&amp;v=2&amp;sensor=true&amp;key=ABQIAAAAAaVFxs6kNq7gWY59qf5XMxSec6s_uUscdbTyPSy8oWl8zYzqFRRanjFebOU60thMmEQQDEPx3A3y5Q"
type="text/javascript"></script>
        <script type="text/javascript">
            var map = null;
            var geocoder = null;
            var from;
            var to;
            var directionsPanel = null;
            var directions = null;
            
            function inicializa() {
                if (GBrowserIsCompatible()) {
                    map = new GMap2(document.getElementById("mapa_base"));
                    map.setCenter(new GLatLng(-22.5489433, -46.6388182), 7);
                    geocoder = new GClientGeocoder();
                    map.addControl( new GSmallMapControl() );
                    map.addControl( new GMapTypeControl() );
                    directionsPanel = document.getElementById("");
                    directions = new GDirections(map, directionsPanel);
                    
                  }
            }
    
            function gerarRota(){
                from = document.getElementById("partida").value;
                to = document.getElementById("destino").value;
                if ( geocoder ) {
                    geocoder.getLatLng(from, 
                        function(point){ 
                            if ( !point ) {
                                alert(from + " não encontrado");
                            } 
                        }
                    );
                    geocoder.getLatLng(to, 
                        function(point){
                            if ( !point ) {
                                alert(to + " não encontrado");
                            } 
                        }
                    );
                    
                    var string = "from: " + from + " to: "+to;
                    directions.clear();
                    directions.load(string);
                    GEvent.addListener(directions, "error", erroGetRoute);
                } else {
                    alert("GeoCoder não identificado");
                }
            }
            
            function erroGetRoute(){
                alert("Não foi possivel traçar a rota de: " + from + " para: " + to );
            }
            
            
    </script>
    </head>
    <body onload="inicializa()" onunload="GUnload()">
        <form id="form_mapa" action="#" method="get">
		<h3>Cigera Car</h3>
            <label for="partida">usuario</label> 
            <input type="text" name="partida" id="partida" value="São Paulo" size="50" />
            <br />
            <label for="destino">oficina</label> 
            <input type="text" name="destino" id="destino" value="Rio de Janeiro" size="50" /> 
            <br />
            <input type="button" name="enviar" id="enviar" value="Gerar Oficinas" onclick="gerarRota()"/>
        </form>
        <div id="mapa_base" style="width: 800px; height: 500px;"></div>
        <div id="route" style="width: 300px; height: 500px; position: absolute; right: 0; top: 0;"></div>
    </body>
</html>
