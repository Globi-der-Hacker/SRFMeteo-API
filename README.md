# SRF Meteo Mobile App API
Die von der beliebten SRF Meteo Mobile App genutzt API kann von jedermann aufgerufen werden. 
Die SRF Meteo Mobile APP nutzt eine API zur Abfrage von Wetterprognosen.

Um die Wetterprognose für einen beliebigen Ort auf der Welt abzufragen, benötigen wir zuerst dessen GeoLocation-ID. Dies kann entweder mit dem Ortsnamen oder der Postleitzahl abgefragt werden:

```
https://www.srf.ch/meteoapi/geolocationNames?name=Zürich
```

Als Antwort erhält man eine Liste mit passenden Locations und allerhand nützlicher Informationen wie Höhe über Meer, Anzahl Einwohner einer Stadt usw.
Uns interessiert hier aber nur das Feld "location_id":

[
    {
        "district": "",
        "description_short": "Zürich",
        "description_long": "Zürich, 408 m ü.M.",
        "id": "4cdc93de6ddc36141f7493213eeedaee",
        "geolocation": {
            "geolocation_names": [
                ...
            ],
            "id": "47.3797,8.5342",
            "lat": 47.3797,
            "lon": 8.5342,
            "station_id": "S12724",
            "timezone": "Europe/Zurich",
            "default_name": "Zürich",
            "alarm_region_id": "11",
            "alarm_region_name": "Stadt ZH",
            "district": ""
        },
        "location_id": "417204077",
        "type": "city",
        "language": 0,
        "translation_type": "orig",
        "name": "Zürich",
        "country": "Schweiz",
        "province": "Zürich",
        "inhabitants": 365132,
        "height": 408,
        "ch": 1
    }
]
