# SRF Meteo Mobile App API
Die von der beliebten SRF Meteo Mobile App genutzt API kann von jedermann aufgerufen werden. 
Die SRF Meteo Mobile APP nutzt eine API zur Abfrage von Wetterprognosen.

Um die Wetterprognose für einen beliebigen Ort auf der Welt abzufragen, benötigen wir zuerst dessen GeoLocation-ID. Dies kann entweder mit dem Ortsnamen oder der Postleitzahl mittels einens simplen GET-Requests abgefragt werden:

```
https://www.srf.ch/meteoapi/geolocationNames?name=Zürich
```
oder
```
https://www.srf.ch/meteoapi/geolocationNames?zip=8000
```

Als Antwort erhält man eine Liste mit passenden Locations und allerhand nützlicher Informationen wie Höhe über Meer, Anzahl Einwohner einer Stadt usw.:

```JSON
[
    {
        "district": "",
        "description_short": "Zürich",
        "description_long": "Zürich, 408 m ü.M.",
        "id": "4cdc93de6ddc36141f7493213eeedaee",
        "geolocation": {
            "geolocation_names": [
                {
                    "district": "",
                    "description_short": "Zürich",
                    "description_long": "Zürich, 408 m ü.M.",
                    "id": "1192045f06b811b701d8d7fcfd9dec64",
                    "location_id": "417204077",
                    "type": "city",
                    "language": 33,
                    "translation_type": "trans",
                    "name": "Zurich",
                    "country": "Schweiz",
                    "province": "Zürich",
                    "inhabitants": 365132,
                    "height": 408,
                    "ch": 1
                },
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
```

Uns interessiert hier aber nur das Feld ```id``` innerhalb von ```geolocation```:

```JSON
"id": "47.3797,8.5342",
```

Diese id kann jetzt beim Aufruf des nächsten Web-Services verwendet werden:

```
https://www.srf.ch/meteoapi/forecastpoint/47.3797,8.5342
```

Bei der GeoLocation-ID handelt es sich um ein Koordinatenpaar. Es ist aber falsch anzunehmen, dass hier einfach ein beliebiges Koordinaten-Paar verwendet werden kann!

Als Antwort enthält man eine JSON-Struktur mit den Grobprognosen auf Tagesbasis, einer etwas detaillierteren Prognose im 3-Stunden-Raster und einer Detailprognose im Stundenraster:

```JSON
{
    "days": [
        ...
    ],
    "three_hours": [
        ...
    ],
    "hours": [
        ...
    ],
    "geolocation": {
        ...
    }
}
```

Schauen wir und einen Prognosedatensatz genauer an:

```JSON
{
    "date_time": "2024-12-25T00:00:00+01:00",
    "symbol_code": 10,
    "symbol24_code": 1,
    "PROBPCP_PERCENT": 4,
    "RRR_MM": 0.0,
    "FF_KMH": 6,
    "FX_KMH": 15,
    "DD_DEG": 50,
    "SUNSET": "2024-12-25T16:40:00+01:00",
    "SUNRISE": "2024-12-25T08:12:00+01:00",
    "SUN_H": 3,
    "UVI": 24,
    "TX_C": 2,
    "TN_C": -2,
    "min_color": {
        "temperature": -2,
        "background_color": "#0c429e",
        "text_color": "#ffffff"
    },
    "max_color": {
        "temperature": 2,
        "background_color": "#0c527c",
        "text_color": "#ffffff"
    }
}
```
