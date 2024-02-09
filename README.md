
# STASY Elevators Unofficial API

Recently STASY published a mini-app on the https://stasy.gr website for the status of the elevators in each station in real time (https://www.stasy.gr/elevators/), so that people with special needs / disabilities can be informed. So yeah this is an Unofficial API that gathers in real-time information from the official stasy.gr website and outputs the elevator statuses in JSON / Rest-API format for all the lines or a specific line.

## Disclaimer
This project is under active development. The creator is not responsible for any malicious action that could damage his own systems or those of third parties (STASY Infrastructure). In case of a legal problem, the creator upon request has the right to terminate the operation of the service at any time, without further notice. Only for personal use, not commercial. Stasy ToS (https://www.stasy.gr/en/terms-of-use/)


## About this version
#### Current Version: v1 (09/02/2024)
- Fetch all elevator statuses from all lines
- Fetch all elevator statuses from a specific line

## Tech Stack
- Node.JS (https://nodejs.org/en)
- Express (https://expressjs.com/)
- Axios (https://axios-http.com/docs/intro)
- Cheerio (https://cheerio.js.org/)

## API Reference

#### Domain

```https
  https://stasy-elevators.georgetomzaridis.eu
```

#### Authentication / Authorazation

You don't need anything, in order to access the API endpoints. It's open for public usage.

#### Content Language

All the content / data is only available in the Greek language as provided from stasy.gr website

### Get all elevators statuses

``` https
  GET https://stasy-elevators.georgetomzaridis.eu/api/status
```

##### Example Response
``` json
[
    {
        "lineID": "1",
        "lineDescr": "Γραμμή 1",
        "lineName": "Πειραιάς - Κηφισία",
        "station_name": "Κηφισιά",
        "elevators": [
            {
                "name": "Οδός Τατοΐου -Υπόγεια Διάβαση",
                "isWorking": 1
            },
            {
                "name": "Αποβάθρα - Υπόγεια Διάβαση",
                "isWorking": 1
            }
        ],
        "accessibilityType": 1,
        "accessibilityDescr": "Όλοι οι ανελκυστήρες του σταθμού λειτουργούν και είναι o σταθμός είναι προσβάσιμος"
    },
    {
        "lineID": "3",
        "lineDescr": "Γραμμή 3",
        "lineName": "Δημοτικό Θέατρο - Αεροδρόμιο",
        "station_name": "Αεροδρόμιο",
        "elevators": [],
        "accessibilityType": 0,
        "accessibilityDescr": "Η συντήρηση των ανελκυστήρων σε αυτόν τον σταθμό δεν γίνεται από τη ΣΤΑ.ΣΥ."
    },
    {
        "lineID": "1",
        "lineDescr": "Γραμμή 1",
        "lineName": "Πειραιάς - Κηφισία",
        "station_name": "Ειρήνη",
        "elevators": [
            {
                "name": "Επίπεδο Έκδοσης Εισιτηρίων - Δρόμος ΣΕΛΕΤΕ",
                "isWorking": 0
            },
            {
                "name": "Μεσαία Αποβάθρα προς Πειραιά",
                "isWorking": 1
            },
            {
                "name": "Προς Πειραιά",
                "isWorking": 1
            },
            {
                "name": "Προς Κηφισιά",
                "isWorking": 1
            }
        ],
        "accessibilityType": 2,
        "accessibilityDescr": "Υπάρχει τουλάχιστον ένας ανελκυστήρας μη λειτουργικός, με τον σταθμό να παραμένει προσβάσιμος"
    }
]

```

| Field | Type     | Notes                |
| :-------- | :------- | :------------------------- |
| `lineID` | `string` | LineID |
| `lineDescr` | `string` | Line Short Name / Route |
| `lineName` | `string` | Line Full Name / Route |
| `station_name` | `string` | Station Name |
| `elevators` | `array` | This maybe be empty [] |
| `elevators.name` | `string` | Elevator Name |
| `elevators.isWorking` | `integer` | 1 true / 0 false |
| `elevators.accessibilityType` | `integer` | See below |
| `elevators.accessibilityDescr` | `string` | Short explanation in greek language |



| accessibilityType | Type | What does this mean? |
| :-------- | :------- | :------- |
| `0` | `integer` | `Unkown or elevator maintenance is not from STASY` |
| `1` | `integer` | `All elevators are working and station is accessible` |
| `2` | `integer` | `At least one elevator is working and station still accessible` |
| `3` | `integer` | `No elevators working, station not accessible` |

### Get all elevators statuses for specific line

```https
  GET https://stasy-elevators.georgetomzaridis.eu/api/status/${lineID}
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `lineID`      | `string` | **Required**. Id of line (see below) |

#### Available Line ID Options
| lineID | LineDescr | LineName |
| :-------- | :------- | :------- |
| `1` | `Γραμμή 1 (Πράσινη) / Line 1 (Green)` | `Πειραιάς - Κηφισία / Peiraias - Kifisia` |
| `2` | `Γραμμή 2 (Κόκκινη) / Line 2 (Red)` | `Ανθούπολη - Ελληνικό / Anthoupoli - Elliniko` |
| `3` | `Γραμμή 3 (Μπλέ) / Line 3 (Blue)` | `Δημοτικό Θέατρο - Αεροδρόμιο / Dimotiko Theatro - Airport` |

##### Example Response
``` json
[
    {
        "lineID": "1",
        "lineDescr": "Γραμμή 1",
        "lineName": "Πειραιάς - Κηφισία",
        "station_name": "Κηφισιά",
        "elevators": [
            {
                "name": "Οδός Τατοΐου -Υπόγεια Διάβαση",
                "isWorking": 1
            },
            {
                "name": "Αποβάθρα - Υπόγεια Διάβαση",
                "isWorking": 1
            }
        ],
        "accessibilityType": 1,
        "accessibilityDescr": "Όλοι οι ανελκυστήρες του σταθμού λειτουργούν και είναι o σταθμός είναι προσβάσιμος"
    },
    {
        "lineID": "1",
        "lineDescr": "Γραμμή 1",
        "lineName": "Πειραιάς - Κηφισία",
        "station_name": "ΚΑΤ",
        "elevators": [
            {
                "name": "Προς Πειραιά",
                "isWorking": 0
            },
            {
                "name": "Προς Κηφισιά",
                "isWorking": 1
            }
        ],
        "accessibilityType": 2,
        "accessibilityDescr": "Υπάρχει τουλάχιστον ένας ανελκυστήρας μη λειτουργικός, με τον σταθμό να παραμένει προσβάσιμος"
    },
]

```

### API Status Codes
| Code | What does this mean? |
| :-------- | :------- |
| `200` | `Everything went well, you are happy` |
| `400` | `Bad request - maybe you forgot to pass a correct lineID value or left it empty` |
| `500` | `Something went wrong, either from my service or from stasy.gr`|

#### Example Error Responses
In general if you are not getting a json that contains status / error fields you are fine :)
``` json
{
    "status": 400,
    "error": "Bad Request"
}

{
    "status": 500,
    "error": "Internal Server Error"
}


```

## Bugs/Suggestions

For bugs/suggestions please send me a email: georgetomzaridis@gmail.com
