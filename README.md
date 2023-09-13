| Parametrs | Metode     | Apraksts                |
| :-------- | :------- | :------------------------- |
| `driverId` | `GET` | Iegūt konkrēta vadītāja darba grafiku, iekļaujot detaļas par katru mēneša dienu. |

#### 2. Izsūtīt SMS paziņojumus:

```http
  Post: /api/driver-schedules/{driverId}
```

| Parametrs | Metode    | Apraksts                       |
| :-------- | :------- | :-------------------------------- |
| `driverId`      | `Post` | Nosūtīt SMS paziņojumu konkrētam vadītājam, kad ir pieejams jauns vai atjaunots darba grafiks |

#### 3. Izsekot grafika parasktiem:

```http
  GET: /api/track-signatures/{month}
```

| Parametrs | Metode     | Apraksts                |
| :-------- | :------- | :------------------------- |
| `month` | `GET` |Sekot vadītāju darba grafika parakstu statusam konkrētā mēnesī. Sniedz sarakstu ar vadītājiem, kuri vēl nav parakstījuši savus grafikus. |

#### 4. Endpoint for Setting Signing Deadlines:

```http
  POST: /api/set-signing-deadlines
```

| Parametrs | Metode     | Apraksts                |
| :-------- | :------- | :------------------------- |
| `date` | `POST` | QA personnel set signing deadlines.The API accepts POST requests with data specifying the month, driver identifier, and the new signing deadline. |

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




