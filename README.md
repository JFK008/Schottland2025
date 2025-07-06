<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="description" content="Finaler interaktiver Reiseplaner für die Schottland-Rundreise 2025 von Chrissy & Jan-Felix. Optimiert für GitHub Pages." />
    <title>Schottland 2025 | Finaler Reiseplaner</title>
    
    <link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>🏴󠁧󠁢󠁳󠁣󠁴󠁿</text></svg>">

    <!-- React-Bibliotheken -->
    <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>

    <!-- CSS-Stile direkt in der HTML-Datei -->
    <style>
        :root {
            --primary-color: #2563eb; --primary-color-light: #eff6ff; --primary-color-dark: #1e40af;
            --text-light: #e2e8f0; --text-dark: #111827; --bg-light: #f9fafb; --bg-dark: #111827;
            --card-bg-light: #ffffff; --card-bg-dark: #1f2937; --border-light: #e5e7eb; --border-dark: #374151;
            --gray-light: #4b5563; --gray-dark: #9ca3af;
        }
        body { margin: 0; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen', 'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif; -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; background-color: var(--bg-light); color: var(--text-dark); line-height: 1.6; }
        html.dark body { background-color: var(--bg-dark); color: var(--text-light); }
        .container { max-width: 900px; margin: 0 auto; padding: 1rem; }
        .header { text-align: center; border-bottom: 1px solid var(--border-light); padding-bottom: 1.5rem; margin-bottom: 2rem; position: relative; }
        html.dark .header { border-bottom-color: var(--border-dark); }
        .dark-mode-toggle { position: absolute; top: 0; right: 0; background: transparent; border: 1px solid var(--border-light); border-radius: 0.5rem; padding: 0.5rem 0.75rem; cursor: pointer; color: inherit; font-size: 0.8rem; }
        html.dark .dark-mode-toggle { border-color: var(--border-dark); }
        .info-box { background-color: var(--primary-color-light); border: 1px solid var(--primary-color); border-radius: 0.75rem; padding: 1.5rem; margin-bottom: 2rem; }
        html.dark .info-box { background-color: rgba(37, 99, 235, 0.2); }
        .day-card { border: 1px solid var(--border-light); border-radius: 0.75rem; background-color: var(--card-bg-light); margin-bottom: 1rem; overflow: hidden; transition: box-shadow 0.3s ease; }
        html.dark .day-card { border-color: var(--border-dark); }
        .day-card:hover { box-shadow: 0 4px 10px -2px rgba(0,0,0,0.1); }
        html.dark .day-card:hover { box-shadow: 0 0 15px rgba(0,0,0,0.2); }
        .day-header { padding: 1rem 1.5rem; cursor: pointer; display: flex; justify-content: space-between; align-items: center; transition: background-color 0.2s ease; }
        .day-header:hover { background-color: var(--primary-color-light); }
        html.dark .day-header:hover { background-color: rgba(37, 99, 235, 0.1); }
        .day-header.active { border-bottom: 1px solid var(--border-light); }
        html.dark .day-header.active { border-bottom-color: var(--border-dark); }
        .day-card-body { max-height: 0; overflow: hidden; transition: max-height 0.7s ease-in-out; }
        .day-card-body.open { max-height: 3000px; }
        .day-card-content { padding: 1.5rem; display: grid; grid-template-columns: 1fr; gap: 1.5rem; }
        @media (min-width: 768px) { .day-card-content { grid-template-columns: 1fr 1fr; } }
        .map-container { width: 100%; height: 450px; border-radius: 0.75rem; border: 1px solid var(--border-light); overflow: hidden; margin-bottom: 2rem; background-color: #e0e0e0; }
        .day-card-map { width: 100%; height: 100%; min-height: 400px; border: 1px solid var(--border-light); border-radius: 0.5rem; background-color: #f9fafb; }
        html.dark .map-container, html.dark .day-card-map { border-color: var(--border-dark); background-color: #1f2937; }
        h1 { font-size: clamp(2rem, 5vw, 2.5rem); font-weight: 800; color: var(--primary-color); margin: 0 0 0.25rem 0; }
        h2 { font-size: 1.5rem; font-weight: 600; margin: 0; flex-grow: 1; }
        h3 { font-size: 1.1rem; font-weight: 600; margin-top: 0; margin-bottom: 1rem; border-bottom: 1px solid var(--border-light); padding-bottom: 0.5rem; }
        html.dark h3 { border-color: var(--border-dark); }
        .route-info-header { font-size: 0.9rem; color: var(--gray-light); margin-left: 1rem; white-space: nowrap; }
        html.dark .route-info-header { color: var(--gray-dark); }
        .info-block { display: flex; align-items: flex-start; gap: 1rem; margin-bottom: 1rem; }
        .info-block-icon { font-weight: 600; color: var(--primary-color); flex-shrink: 0; width: 80px; text-align: right; }
        .info-block-title { font-weight: 600; }
        .info-block-desc { font-size: 0.9rem; color: var(--gray-light); margin-top: 0.25rem;}
        html.dark .info-block-desc { color: var(--gray-dark); }
        .link-icons a { color: var(--primary-color-dark); text-decoration: none; font-size: 0.8rem; margin-left: 0.75rem; display: inline-block; font-weight: 600; }
        .link-icons a:hover { text-decoration: underline; }
        .accordion-arrow { font-size: 1.2rem; transition: transform 0.3s ease; }
        .accordion-arrow.open { transform: rotate(90deg); }
        .footer { text-align: center; padding: 2rem; color: var(--gray-light); font-size: 0.9rem; }
        html.dark .footer { color: var(--gray-dark); }
    </style>
</head>
<body>
    <div id="root"></div>

    <script>
        "use strict";

        const { useEffect, useState } = React;

        const createGoogleMapsLink = query => `https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(query)}`;

        // *** WICHTIGE ÄNDERUNG: DATEN MIT GPS-KOORDINATEN FÜR SEHENSWÜRDIGKEITEN ***
        const REISEPLAN_DATEN = [{
          tag: 1,
          titel: "Ankunft & Edinburgh",
          startCoords: { lat: 55.923, lon: -3.358 },
          zielCoords: { lat: 55.908, lon: -3.193 },
          distanz: "15 km",
          fahrzeit: "30min",
          infos: [
            { icon: "Burg", title: "Edinburgh Castle", gmaps: "Edinburgh Castle", web: "https://www.edinburghcastle.scot/", desc: "Das Wahrzeichen der Stadt. Tickets unbedingt 2-3 Wochen vorbuchen!", coords: { lat: 55.9486, lon: -3.2009 } }, 
            { icon: "Aussicht", title: "Calton Hill", gmaps: "Calton Hill, Edinburgh", web: "https://www.visitscotland.com/info/see-do/calton-hill-p255151", desc: "Leichter Aufstieg für den besten Panoramablick. Perfekt für den Sonnenuntergang.", coords: { lat: 55.9552, lon: -3.1822 } }, 
            { icon: "Essen", title: "Kulinarik-Tipp", desc: "Probiert Haggis, Neeps and Tatties in einem Pub am Grassmarket oder in der Rose Street." }, 
            { icon: "Tipp", title: "Praktischer Hinweis", desc: "Lasst den Camper stehen! Nutzt den Bus ins Zentrum. Kauft ein Tagesticket ('DAYticket')." }]
        }, {
          tag: 2,
          titel: "Kelpies & Tor nach Loch Lomond",
          startCoords: { lat: 55.908, lon: -3.193 },
          zielCoords: { lat: 56.101, lon: -4.633 },
          distanz: "100 km",
          fahrzeit: "1h 45min",
          infos: [
            { icon: "Tiere", title: "The Kelpies", gmaps: "The Kelpies, Falkirk", web: "https://www.thehelix.co.uk/", desc: "Gigantische Pferdeköpfe. Plant mind. 1-2 Stunden für einen Spaziergang im Helix Park ein.", coords: { lat: 56.0150, lon: -3.7570 } }, 
            { icon: "Burg", title: "Stirling Castle (Optional)", gmaps: "Stirling Castle", web: "https://www.stirlingcastle.scot/", desc: "Eine großartige Alternative zu Edinburgh Castle, oft als noch beeindruckender empfunden.", coords: { lat: 56.1239, lon: -3.9469 } }, 
            { icon: "Dorf", title: "Luss Village", gmaps: "Luss, Scotland", web: "https://www.lochlomond-trossachs.org/things-to-do/visiting-the-national-park/luss/", desc: "Besucht das malerische Dorf mit seinen hübschen Cottages direkt am Seeufer.", coords: { lat: 56.1009, lon: -4.6341 } }]
        }, {
          tag: 3,
          titel: "Durch Glen Coe",
          startCoords: { lat: 56.101, lon: -4.633 },
          zielCoords: { lat: 56.666, lon: -5.103 },
          distanz: "100 km",
          fahrzeit: "2h",
          infos: [
            { icon: "Foto", title: "Three Sisters Viewpoint", gmaps: "Three Sisters Viewpoint, Glencoe", web: "https://www.walkhighlands.co.uk/fortwilliam/glencoe.shtml", desc: "Der berühmteste Fotostopp. Seid früh da oder habt Geduld, es kann voll werden.", coords: { lat: 56.6698, lon: -4.9602 } }, 
            { icon: "Film", title: "Skyfall-Location (Glen Etive)", gmaps: "Dalness, Glen Etive", web: "https://www.visitscotland.com/info/towns-villages/glen-etive-p1208931", desc: "Ein Abstecher auf der einspurigen Straße Glen Etive führt euch zur berühmten Filmkulisse.", coords: { lat: 56.6219, lon: -4.9497 } }, 
            { icon: "Pub", title: "Clachaig Inn", gmaps: "Clachaig Inn, Glencoe", web: "https://clachaig.com/", desc: "Eine Institution in Glen Coe. Perfekt für ein herzhaftes Mittagessen oder ein lokales Ale.", coords: { lat: 56.6789, lon: -5.0683 } }]
        }, {
          tag: 4,
          titel: "Glenfinnan & Fort William",
          startCoords: { lat: 56.666, lon: -5.103 },
          zielCoords: { lat: 56.819, lon: -5.107 },
          distanz: "55 km",
          fahrzeit: "1h",
          infos: [
            { icon: "Zug", title: "Glenfinnan Viaduct", gmaps: "Glenfinnan Viaduct View Point", web: "https://www.nts.org.uk/visit/places/glenfinnan-monument", desc: "Prüft online die genauen Zeiten, wann der Jacobite-Zug das Viadukt überquert! Ein Muss.", coords: { lat: 56.8762, lon: -5.4339 } }, 
            { icon: "Berg", title: "Ben Nevis (Blick)", gmaps: "Ben Nevis Visitor Centre", web: "https://www.walkhighlands.co.uk/fortwilliam/bennevis.shtml", desc: "Das Visitor Centre ist der Startpunkt für Wanderungen zum höchsten Berg Großbritanniens.", coords: { lat: 56.8000, lon: -5.0883 } }, 
            { icon: "Shop", title: "Vorbereitung", desc: "Fort William ist der letzte große Supermarkt vor Skye. Füllt eure Vorräte für die nächsten Tage auf." }]
        }, {
          tag: 5,
          titel: "Fähre & Isle of Skye (Süden)",
          startCoords: { lat: 56.819, lon: -5.107 },
          zielCoords: { lat: 57.291, lon: -6.177 },
          distanz: "100 km",
          fahrzeit: "2h + Fähre",
          infos: [
            { icon: "Fähre", title: "Fähre nach Skye (CalMac)", gmaps: "Mallaig Ferry Terminal", web: "https://www.calmac.co.uk/mallaig-armadale-skye-ferry-summer-timetable", desc: "Fahrt die 'Road to the Isles' nach Mallaig und nehmt die Fähre. MUSS vorgebucht werden!", coords: { lat: 57.0061, lon: -5.8288 } }, 
            { icon: "Natur", title: "Fairy Pools", gmaps: "Fairy Pools Car Park, Glenbrittle", web: "https://www.isleofskye.com/things-to-do/fairy-pools", desc: "Magische Wasserfälle. Benötigt gutes Schuhwerk. Kann bei viel Regen sehr matschig sein.", coords: { lat: 57.2505, lon: -6.2573 } }, 
            { icon: "Whisky", title: "Talisker Distillery", gmaps: "Talisker Distillery, Carbost", web: "https://www.malts.com/en-row/distilleries/talisker", desc: "Besuch der berühmten Destillerie in Carbost. Touren müssen fast immer online vorgebucht werden.", coords: { lat: 57.2831, lon: -6.3562 } }]
        }, {
          tag: 6,
          titel: "Isle of Skye (Norden)",
          startCoords: { lat: 57.291, lon: -6.177 },
          zielCoords: { lat: 57.625, lon: -6.206 },
          distanz: "60 km",
          fahrzeit: "1h 15min",
          infos: [
            { icon: "Wandern", title: "Old Man of Storr", gmaps: "Old Man of Storr Car Park", web: "https://www.isleofskye.com/things-to-do/the-old-man-of-storr", desc: "Die lohnende Wanderung zur Felsnadel. Geht früh los, um den Massen zu entgehen.", coords: { lat: 57.5065, lon: -6.1793 } }, 
            { icon: "Auto", title: "Quiraing Loop", gmaps: "Quiraing Car Park", web: "https://www.theskyeguide.com/walking-main/trotternish-ridge/quiraing", desc: "Eine der spektakulärsten Passstraßen. Der Parkplatz oben ist oft voll.", coords: { lat: 57.6423, lon: -6.2737 } }, 
            { icon: "Dorf", title: "Hafen von Portree", gmaps: "Portree Harbour", web: "https://www.isleofskye.com/portree", desc: "Die Hauptstadt von Skye. Hier könnt ihr tanken, einkaufen und die berühmten bunten Häuser fotografieren.", coords: { lat: 57.4124, lon: -6.1927 } }]
        }, {
          tag: 7,
          titel: "Start der North Coast 500",
          startCoords: { lat: 57.625, lon: -6.206 },
          zielCoords: { lat: 57.897, lon: -5.159 },
          distanz: "200 km",
          fahrzeit: "3h 30min",
          infos: [
            { icon: "Burg", title: "Eilean Donan Castle", gmaps: "Eilean Donan Castle", web: "https://www.eileandonancastle.com/", desc: "Ein kurzer Abstecher von der Skye Bridge. Die meistfotografierte Burg Schottlands.", coords: { lat: 57.2740, lon: -5.5161 } }, 
            { icon: "Landschaft", title: "Wester Ross Coastal Trail", web: "https://www.northcoast500.com/blog/your-guide-to-wester-ross/", desc: "Dies ist der schönste Teil der NC500. Die Strecke über Gairloch nach Ullapool ist phänomenal." }, 
            { icon: "Essen", title: "The Seafood Shack", gmaps: "The Seafood Shack, Ullapool", web: "https://www.seafoodshack.co.uk/", desc: "In Ullapool angekommen, gönnt euch superfrischen Fisch und Meeresfrüchte.", coords: { lat: 57.8967, lon: -5.1585 } }]
        }, {
          tag: 8,
          titel: "Höhepunkte der Nordküste",
          startCoords: { lat: 57.897, lon: -5.159 },
          zielCoords: { lat: 57.477, lon: -4.224 },
          distanz: "95 km",
          fahrzeit: "1h 30min",
          infos: [
            { icon: "Strand", title: "Achmelvich Bay", gmaps: "Achmelvich Bay", web: "https://www.northcoast500.com/listing/achmelvich-beach/", desc: "Ein Abstecher zu einem der schönsten Strände Schottlands mit weißem Sand und türkisfarbenem Wasser.", coords: { lat: 58.1691, lon: -5.3033 } }, 
            { icon: "Brücke", title: "Kylesku Bridge", gmaps: "Kylesku Bridge Viewpoint", web: "https://www.thestorybehindthestructure.co.uk/kylesku-bridge/", desc: "Eine elegant geschwungene, ikonische Brücke und ein fantastisches Fotomotiv.", coords: { lat: 58.2570, lon: -5.0215 } }, 
            { icon: "Natur", title: "Loch Ness & Urquhart Castle", gmaps: "Urquhart Castle", web: "https://www.historicenvironment.scot/visit-a-place/places/urquhart-castle/", desc: "Haltet Ausschau nach Nessie! Urquhart Castle bietet die beste Aussicht auf den See.", coords: { lat: 57.3242, lon: -4.4418 } }]
        }, {
          tag: 9,
          titel: "Speyside Whisky & Moray Firth",
          startCoords: { lat: 57.477, lon: -4.224 },
          zielCoords: { lat: 57.706, lon: -2.855 },
          distanz: "110 km",
          fahrzeit: "2h",
          infos: [
            { icon: "Geschichte", title: "Culloden Battlefield", gmaps: "Culloden Battlefield", web: "https://www.nts.org.uk/visit/places/culloden", desc: "Ein sehr bewegender und wichtiger Ort der schottischen Geschichte, direkt bei Inverness.", coords: { lat: 57.4777, lon: -4.0984 } }, 
            { icon: "Whisky", title: "Speyside Cooperage", gmaps: "Speyside Cooperage Visitor Centre", web: "https://www.speysidecooperage.co.uk/", desc: "Erlebt, wie Whiskyfässer von Hand gefertigt werden. Eine faszinierende Tour.", coords: { lat: 57.4608, lon: -3.0970 } }, 
            { icon: "Foto", title: "Bow Fiddle Rock", gmaps: "Bow Fiddle Rock, Portknockie", web: "https://www.visitscotland.com/info/see-do/bow-fiddle-rock-p2562111", desc: "Euer Zielort ist berühmt für diesen außergewöhnlichen Felsbogen im Meer.", coords: { lat: 57.7065, lon: -2.8465 } }]
        }, {
          tag: 10,
          titel: "Dunnottar Castle & Ostküste",
          startCoords: { lat: 57.706, lon: -2.855 },
          zielCoords: { lat: 56.962, lon: -2.210 },
          distanz: "90 km",
          fahrzeit: "1h 45min",
          infos: [
            { icon: "Burg", title: "Dunnottar Castle", gmaps: "Dunnottar Castle Car Park", web: "https://www.dunnottarcastle.co.uk/", desc: "Das Highlight des Tages. Eine dramatisch auf einer Klippe gelegene Burgruine.", coords: { lat: 56.9458, lon: -2.1973 } }, 
            { icon: "Tiere", title: "RSPB Fowlsheugh", gmaps: "RSPB Fowlsheugh car park", web: "https://www.rspb.org.uk/reserves-and-events/reserves-a-z/fowlsheugh/", desc: "Nahe Dunnottar befindet sich eine riesige Klippe voller Seevögel (inkl. Papageientaucher im Sommer).", coords: { lat: 56.9142, lon: -2.2033 } }, 
            { icon: "Essen", title: "Kulinarik-Tipp", gmaps: "The Carron Fish Bar, Stonehaven", web: "https://www.facebook.com/carronfishbar/", desc: "Stonehaven gilt als Geburtsort des 'Deep-fried Mars Bar'. Wenn nicht hier, wo dann?", coords: { lat: 56.9629, lon: -2.2078 } }]
        }, {
          tag: 11,
          titel: "St. Andrews & Fischerdörfer",
          startCoords: { lat: 56.962, lon: -2.210 },
          zielCoords: { lat: 56.339, lon: -2.796 },
          distanz: "95 km",
          fahrzeit: "1h 30min",
          infos: [
            { icon: "Sport", title: "St. Andrews", gmaps: "St Andrews Cathedral", web: "https://www.standrews.com/", desc: "Die Heimat des Golfs. Besucht den Old Course, die Ruinen der Kathedrale und die Universität.", coords: { lat: 56.3397, lon: -2.7885 } }, 
            { icon: "Dorf", title: "Fife Fishing Villages", web: "https://www.visitscotland.com/info/tours/fife-coastal-route-p247501", desc: "Fahrt die Küstenstraße ('East Neuk') und haltet in Crail, Anstruther und Pittenweem." }, 
            { icon: "Essen", title: "Bestes Fish & Chips", gmaps: "Anstruther Fish Bar", web: "https://www.anstrutherfishbar.co.uk/", desc: "Gewinnt regelmäßig Preise für das beste Fish & Chips in Großbritannien. Rechnet mit einer Warteschlange.", coords: { lat: 56.2238, lon: -2.6989 } }]
        }, {
          tag: 12,
          titel: "Forth Bridges & Abschied",
          startCoords: { lat: 56.339, lon: -2.796 },
          zielCoords: { lat: 55.923, lon: -3.358 },
          distanz: "75 km",
          fahrzeit: "1h 15min",
          infos: [
            { icon: "Brücke", title: "Forth Bridges Viewpoint", gmaps: "Forth Bridges Viewpoint, South Queensferry", web: "https://www.theforthbridges.org/", desc: "Macht einen letzten Stopp, um die drei imposanten Brücken aus drei Jahrhunderten zu bestaunen.", coords: { lat: 55.9936, lon: -3.3915 } }, 
            { icon: "Pause", title: "Letzter Kaffee", gmaps: "Hawes Inn, South Queensferry", web: "https://www.vintageinn.co.uk/restaurants/scotland-northernireland/thehawesinnsouthqueensferry", desc: "Das historische Hawes Inn ist perfekt, um die Reise ausklingen zu lassen.", coords: { lat: 55.9902, lon: -3.3894 } }, 
            { icon: "Camper", title: "Camper-Rückgabe", desc: "Plant genug Zeit ein! Ihr müsst tanken, Wasser ablassen, putzen und auf die Abnahme warten." }]
        }];

        const GesamtroutenKarte = () => {
          const markers = REISEPLAN_DATEN.map(tag => `marker=${tag.zielCoords.lat},${tag.zielCoords.lon}`).join('&');
          const mapSrc = `https://www.openstreetmap.org/export/embed.html?bbox=-8.6,54.6,-0.7,59&layer=mapnik&${markers}`;
          return React.createElement("div", { className: "map-container" },
            React.createElement("iframe", { width: "100%", height: "100%", src: mapSrc, style: { border: 0 }, loading: "lazy", referrerPolicy: "no-referrer-when-downgrade" })
          );
        };

        const Tageskarte = ({ tagData, isActive, onHeaderClick }) => {
          // *** WICHTIGE ÄNDERUNG: KARTE MIT ROUTE UND SEHENSWÜRDIGKEITEN ***
          const poiMarkers = tagData.infos
            .filter(info => info.coords) // Nur Infos mit Koordinaten verwenden
            .map(info => `marker=${info.coords.lat},${info.coords.lon}`)
            .join('&');
          
          const routeParams = `from=${tagData.startCoords.lat}%2C${tagData.startCoords.lon}&to=${tagData.zielCoords.lat}%2C${tagData.zielCoords.lon}`;
          const mapSrc = `https://www.openstreetmap.org/directions/embed?${routeParams}&route=car&${poiMarkers}`;

          return React.createElement("div", { className: "day-card" },
            React.createElement("div", { className: `day-header ${isActive ? 'active' : ''}`, onClick: onHeaderClick },
              React.createElement("span", { className: `accordion-arrow ${isActive ? 'open' : ''}` }, "\u25B6"),
              React.createElement("h2", null, "Tag ", tagData.tag, ": ", tagData.titel),
              React.createElement("div", { className: "route-info-header" }, React.createElement("span", null, tagData.distanz, " / ca. ", tagData.fahrzeit))
            ),
            React.createElement("div", { className: `day-card-body ${isActive ? 'open' : ''}` },
              React.createElement("div", { className: "day-card-content" },
                React.createElement("div", null,
                  React.createElement("h3", null, "Tagesplan & Empfehlungen"),
                  tagData.infos.map(item => React.createElement("div", { key: item.title, className: "info-block" },
                    React.createElement("div", { className: "info-block-icon" }, item.icon, ":"),
                    React.createElement("div", null,
                      React.createElement("div", { className: "info-block-title" },
                        React.createElement("span", null, item.title),
                        React.createElement("span", { className: "link-icons" },
                          item.gmaps && React.createElement("a", { href: createGoogleMapsLink(item.gmaps), target: "_blank", rel: "noopener noreferrer", title: `Navigation zu ${item.title} starten` }, "(Karte)"),
                          item.web && React.createElement("a", { href: item.web, target: "_blank", rel: "noopener noreferrer", title: `Website für ${item.title} öffnen` }, "(Web)")
                        )
                      ),
                      React.createElement("div", { className: "info-block-desc" }, item.desc)
                    )
                  ))
                ),
                React.createElement("div", null,
                  React.createElement("h3", null, "Tagesroute & Highlights"),
                  React.createElement("iframe", {
                    className: "day-card-map",
                    src: isActive ? mapSrc : 'about:blank',
                    referrerPolicy: "no-referrer-when-downgrade",
                    title: `Karte für Tag ${tagData.tag}`
                  })
                )
              )
            )
          );
        };

        function App() {
          const [isDarkMode, setIsDarkMode] = useState(() => window.matchMedia?.("(prefers-color-scheme: dark)").matches ?? false);
          const [activeDay, setActiveDay] = useState(null);
          useEffect(() => {
            document.documentElement.classList.toggle('dark', isDarkMode);
          }, [isDarkMode]);

          const handleDayClick = dayTag => {
            setActiveDay(activeDay === dayTag ? null : dayTag);
          };

          return React.createElement("div", { className: "container" },
            React.createElement("header", { className: "header" },
              React.createElement("button", { onClick: () => setIsDarkMode(!isDarkMode), className: "dark-mode-toggle", title: "Dark Mode umschalten" }, isDarkMode ? 'Licht' : 'Dunkel'),
              React.createElement("h1", null, "Schottland 2025"),
              React.createElement("p", null, "Interaktiver Reiseplaner für Chrissy & Jan-Felix")
            ),
            React.createElement("main", null,
              React.createElement("h3", null, "Gesamtübersicht der Reise-Etappen"),
              React.createElement(GesamtroutenKarte, null),
              React.createElement("div", { className: "info-box" },
                React.createElement("div", { className: "info-block" },
                  React.createElement("div", { className: "info-block-icon" }, "Camper:"),
                  React.createElement("div", null,
                    React.createElement("div", { className: "info-block-title" },
                      React.createElement("span", null, "Camper Abholung & Rückgabe: Spaceships Rentals"),
                      React.createElement("span", { className: "link-icons" },
                        React.createElement("a", { href: createGoogleMapsLink("Spaceships Rentals, Old Liston, Edinburgh EH29 9NR"), target: "_blank", rel: "noopener noreferrer", title: "Navigation zu Spaceships Rentals starten" }, "(Karte)"),
                        React.createElement("a", { href: "https://www.spaceshipsrentals.co.uk/contact-us/", target: "_blank", rel: "noopener noreferrer", title: "Website von Spaceships Rentals öffnen" }, "(Web)")
                      )
                    ),
                    React.createElement("div", { className: "info-block-desc" }, "Euer Abenteuer beginnt und endet hier. Plant am letzten Tag genug Zeit für die Rückgabe ein!")
                  )
                )
              ),
              React.createElement("h3", null, "Tages-Etappen"),
              REISEPLAN_DATEN.map(tag => React.createElement(Tageskarte, { key: tag.tag, tagData: tag, isActive: activeDay === tag.tag, onHeaderClick: () => handleDayClick(tag.tag) }))
            ),
            React.createElement("footer", { className: "footer" },
              React.createElement("p", null, "Gute Reise und unvergessliche Erlebnisse in Schottland!")
            )
          );
        }

        const container = document.getElementById('root');
        const root = ReactDOM.createRoot(container);
        root.render(React.createElement(App, null));
    </script>
</body>
</html>
