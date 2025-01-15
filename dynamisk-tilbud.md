# Tilbudsevaluering for nye abonnement

## Introduksjon

**Denne oppgaven er designet for å vurderes på rundt tre timers arbeid.** Målet er å forstå hvordan du tilnærmer deg oppgaven, ikke å levere et komplett og perfekt system.

Hos Morgenbladet ønsker vi å tilby en sømløs opplevelse for abonnenter, samtidig som vi vil unngå overdreven utnyttelse av våre rabatter. Derfor er det viktig for oss å tilby riktige tilbud til brukere basert på deres nåværende status og abonnementshistorikk. Denne oppgaven reflekterer et relevant scenario: å segmentere brukere og generere passende tilbud basert på predefinerte regler.

---

## Krav

Du skal bygge et system som evaluerer tilbud basert på brukerens input og presenterer resultatet i et enkelt brukergrensesnitt. Du står fritt til å velge teknologi og fremgangsmåte, enten det er et API-basert system, eller en ren server-side applikasjon. Velg en tilnærming som best reflekterer dine styrker, samtidig som kravene oppfylles. Du kan bruke de verktøyene, språkene eller rammeverkene du er mest komfortabel med.

### Eksempler på fremgangsmåte

1. **API-basert**:
   - Et backend API som:
     - Aksepterer en e-postadresse som input.
     - Prosesserer input og finner passende segment og tilbud for brukeren.
     - Returnerer resultatet som JSON.
   - En enkel frontend som:
     - Lar brukeren skrive inn sin e-postadresse.
     - Kaller på API-et og viser segment og tilbud fra responsen.
2. **Serverside MVC**:
   - En enkel nettside hvor:
     - Brukere kan skrive inn sin e-postadresse.
     - En prosess på serveren evaluerer input og returnerer en side med segmentet og tilbudet til brukeren.

---

### Systemets egenskaper

Systemet burde:

1. **Ta imot en e-postadresse som input.**
2. **Finne bruker- og abonnementsinfo fra to JSON-datasett:**
   - **`users.json`**: Inneholder brukerdetaljer.
   - **`subscriptions.json`**: Inneholder abonnementshistorikk.
3. **Klassifisere brukere inn i ett av de følgende segmentene:**
   - **Nåværende abonnent**: Brukeren har et aktivt abonnement (ingen `subscription_end_date`).
     - Output: "Du er allerede abonnent og har tilgang til Morgenbladet."
   - **Ny abonnent**: E-posten finnes ikke i `users.json`.
     - Output: En velkomstrabatt.
   - **Risiko for churn**: Abonnementet er fortsatt aktivt, men har blitt kansellert (har `subscription_end_date` i fremtiden).
     - Output: Et insentiv for å fornye abonnementet (f.eks. 10% rabatt hvis brukeren reaktiverer).
   - **Tidligere abonnent**: Abonnementet er avsluttet (har `subscription_end_date` i fortiden).
     - Output: En rabatt for å lokke dem tilbake.
   - **Potensiell tilbudsrytter**: Historikk med flere kanselleringer og hyppig bruk av rabatt.
     - Output: Abonnement til full pris.
4. **Presentere segmentet og tilbudet tydelig i brukergrensesnittet.**

---

### Eksempler på output

- **API Output (JSON)**:
  ```json
  {
    "email": "loyaluser@example.test",
    "segment": "Nåværende abonnent",
    "message": "Du er allerede abonnent og har tilgang til Morgenbladet."
  }
  ```
- **MVC Output (HTML)**:
  > "Du er allerede abonnent og har tilgang til Morgenbladet."

---

## Beskrivelse av datasettet

Du får to JSON-filer som representerer henholdsvis brukerinformasjon og abonnementshistorikk. Disse er koblet sammen ved hjelp av `user_id`, som fungerer som en unik identifikator mellom datasettene. Disse datasettene vil brukes til å hente nødvendige data for å evaluere brukersegmenter og tilbud:

1. **`users.json`**:

   ```json
   [
     { "user_id": 1, "email": "loyaluser@example.test", "signups": 1 },
     { "user_id": 2, "email": "abuser@example.test", "signups": 2 }
   ]
   ```

2. **`subscriptions.json`**:

   ```json
   [
     {
       "user_id": 1,
       "subscription_start_date": "2023-01-01",
       "subscription_end_date": null,
       "discount_used": false
     },
     {
       "user_id": 2,
       "subscription_start_date": "2024-10-15",
       "subscription_end_date": "2024-11-14",
       "discount_used": true
     },
     {
       "user_id": 2,
       "subscription_start_date": "2024-12-01",
       "subscription_end_date": null,
       "discount_used": true
     }
   ]
   ```

---

## Leveranse

Leveransen burde inneholde:

1. **Koden din:**
   - En fungerende løsning som tilfredsstiller kravene.
   - En godt organisert implementasjon med dine foretrukne språk eller rammeverk.
2. **Dokumentasjon:**
   - En README-fil som inneholder:
     - Instruksjoner for hvordan man kjører applikasjonen, inkludert steg for oppsett og avhengigheter.
     - En kort beskrivelse av valg, antagelser, kompromisser og utfordringer du har møtt på under utviklingen.

---

## Forventninger

Vi ser ikke etter perfeksjon eller blankpolert kode. I stedet ser vi etter:

- **Problemløsning**: Hvordan du har taklet problemet og brutt det ned.
- **Fullstack-ferdigheter**: Din evne til å bygge komponenter både på front- og backend.
- **Klarhet og struktur**: Hvordan du strukturerer og dokumenterer arbeidet ditt.
- **Håndtering av data**: Hvordan du kombinerer og prosesserer relaterte datasett.

For vår del trenger du ikke å bruke mer enn maks **tre timer**. Hvis tidsbegrensninger forhindrer deg i å implementere alle kravene, fokuser heller på å levere en godt strukturert og gjennomtenkt løsning. Vi ønsker at du prioriterer en klar struktur og tankegang, selv om det betyr at ikke alle krav blir oppfylt. Delvise implementasjoner er helt akseptable så lenge de demonstrerer en god problemløsningstilnærming og tydelig dokumentasjon.

---

## Leveringsinstruksjon

- Pakk sammen koden din (f.eks. i en zip-fil eller et repo på GitHub).
- Inkluder tydelige instruksjoner for å kjøre appen lokalt.

## Datafiler

- [users.json](https://github.com/Mentor-Medier/hiring/blob/main/tillegg/dynamisk-tilbud/users.json)
- [subscriptions.json](https://github.com/Mentor-Medier/hiring/blob/main/tillegg/dynamisk-tilbud/subscriptions.json)
