
# API darbības apraksts
 
#### Vadītāju grafiku digitalizēšana:

#### 1. Vadītāja darba grafiks:
```
  GET: /api/driver-schedules/{driverId}
```

| Parametrs | Metode     | Apraksts                |
| :-------- | :------- | :------------------------- |
| `driverId` | `GET` | Iegūt konkrēta vadītāja darba grafiku, iekļaujot detaļas par katru mēneša dienu. |

#### 2. Izsūtīt SMS paziņojumus:

```
  Post: /api/driver-schedules/{driverId}
```

| Parametrs | Metode    | Apraksts                       |
| :-------- | :------- | :-------------------------------- |
| `driverId`      | `Post` | Nosūtīt SMS paziņojumu konkrētam vadītājam, kad ir pieejams jauns vai atjaunots darba grafiks |

#### 3. Izsekot grafika parasktiem:

```
  GET: /api/track-signatures/{month}
```

| Parametrs | Metode     | Apraksts                |
| :-------- | :------- | :------------------------- |
| `month` | `GET` |Sekot vadītāju darba grafika parakstu statusam konkrētā mēnesī. Sniedz sarakstu ar vadītājiem, kuri vēl nav parakstījuši savus grafikus. |

#### 4. Izveidot parakstīšanas termiņus:

```
  POST: /api/set-signing-deadlines
```

| Parametrs | Metode     | Apraksts                |
| :-------- | :------- | :------------------------- |
| `date` | `POST` | Tiek nostatīts grafika parakstīšanas termiņš. API pieņem POST pieprasījumu ar datiem, kuros norādīts : mēnesis, vadītāja identifikātors un parakstīšanas termiņš.

#### 5. Atjaunināta JSON atbildes struktūra:

   - Dienas tips: API atbilde tagad iekļauj papildu lauku, kas norāda katras dienas veidu (piemēram, darbdiena, sestdiena, svētdiena vai svētku diena).
   - Tūres detaļas: Detalizēta informācija par tūrēm tiek sniegta, iekļaujot tūres numuru, traucējumu veidu (piemēram, elektrisks, dīzeļs), sākuma un beigu laiku, atpūtas informāciju (ja piemērojams) un jebkādas papildu piezīmes.
   - Maiņu piešķiršana manevru vadītājiem: Manevru vadītājiem API atbilde iekļauj diennakts maiņu piešķiršanas apzīmējumus (piemēram, X, O).
   - Mēneša darba normas un kopējais darba stundu skaits: Katram vadītājam tiek parādītas mēneša stundu normas un kopējais plānoto darba stundu skaits kalendāra mēnesī.
   - Paziņojumi: API tagad ievieš SMS paziņojumus, lai informētu vadītājus, kad ir pieejami jauni vai atjaunoti darba grafiki.
   - Kontroles un sekotāju informācija: Ir izveidotas mehānismi, kas seko, vai vadītāji ir parakstījuši savus grafikus, un var izgūt sarakstus ar tiem vadītājiem, kuri vēl nav parakstījuši grafikus.
   - Papildu piezīmes vai skaidrojumi: API ļauj iekļaut skaidrojošas piezīmes vai papildu informāciju, lai sniegtu kontekstu vai skaidrojumus.
   - Kļūdu apstrādes informācija: API nosaka, kā tiek apstrādātas kļūdas saistībā ar grafiku piegādi vai apstiprināšanu, sniedzot skaidras kļūdu ziņas un statusa kodus.

Atjaunināta JSON atbilde: 

```JSON
{
    "driverId": "12345",
    "month": "September",
    "year": "2023",
    "monthlyWorkNorms": "160 hours",
    "totalPlannedHours": "150 hours",
    "schedule": [
        {
            "date": "1",
            "dayType": "weekday",
            "shift": "morning",
            "tourDetails": {
                "tourNumber": "T101",
                "tractionType": "electric",
                "startTime": "06:00",
                "endTime": "14:00",
                "restInformation": "Lunch break from 12:00 to 12:30",
                "notes": "Special event in the city. Expect delays."
            }
        },
        {
            "date": "2",
            "dayType": "Saturday",
            "shift": "night",
            "tourDetails": {
                "tourNumber": "T102",
                "tractionType": "diesel",
                "startTime": "20:00",
                "endTime": "04:00",
                "restInformation": "No scheduled breaks",
                "notes": "Track maintenance on route 5."
            },
            "shiftAssignmentForManoeuvreDrivers": "X"
        },
        {
            "date": "30",
            "dayType": "Sunday",
            "shift": "afternoon",
            "tourDetails": {
                "tourNumber": "T130",
                "tractionType": "electric",
                "startTime": "12:00",
                "endTime": "20:00",
                "restInformation": "Lunch break from 15:00 to 15:30",
                "notes": "Standard route."
            }
        }
    ],
    "notifications": [
        {
            "date": "1",
            "message": "Your schedule for September 2023 is now available."
        },
        {
            "date": "15",
            "message": "Please sign your September schedule by the deadline."
        }
    ],
    "controlAndTracking": {
        "signatureStatus": "Pending",
        "signedDate": null,
        "deadlineForSigning": "10"
    },
    "additionalNotes": "Keep track of daily updates due to ongoing track work."
}

#### API darbības shematisks attēlojums : 
(./API_MD_PV/PV_majas_darbs_API_Karlis_Golubovs.drawio.png)

