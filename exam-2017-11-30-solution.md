# Tentamen 2017-11-30

## Uppgift 1 (20p)
Vi har följande kod:

![](images/2017-11-30&#32;-&#32;Code&#32;1.png)

Vad skrivs ut när följande kod utförs?
Om inget skrivs ut, skriv ***inget***

```java
Parrot polly = new Parrot(); 
Dog snoopy = new Dog(); 
```

| Nr | Kod                                  | Utskrift             | Från rad |
|----|--------------------------------------|----------------------|:--------:|
|  1 | snoopy.beQuiet();                    | I won't bark much    | 58       |
|  2 | snoopy.talk();                       | Woof                 | 43       |
|  3 | snoopy.beNoisy();                    | I bark a lot         | 52       |
|  4 | snoopy.talk();                       | Wow Wow Wow Wow      | 45       |
|  5 | polly.talk();                        | I can not talk       | 17       |
|  6 | polly.learn("Polly want a cracker"); | Polly want a cracker | 88       |
|  7 | polly.talk();                        | Polly want a cracker | 88       |
|  8 | snoopy.setName("Polly");             | Inget                | -        |
|  9 | polly.whatsYourName();               | I have no name       | 24       |
| 10 | snoopy.whatsYourName();              | My name is Polly     | 22       |
 
 # Uppgift 2 (80p)

![](images/2017-11-30&#32;-&#32;Figure&#32;3.1.png)

* a) Implementera modellen ovan (Figur 3.1). Alla instansvariabler skall vara privata och ha
publika åtkomstmetoder. 

    laggTillFordon-metoden i Register ska lägga till ett fordon och hittaFordon-metoden ska hitta och returnera ett fordon (regNr i Fordon är unikt). Om inget fordon med aktuellt registreringsnummer hittas ska null returneras. 
    
    Vidare ska laggTillFordon-metoden i Agare lägga till ett fordon till ägaren och hittaFordon-metoden ska hitta ett visst fordon hos ägaren. Om inget fordon hittas ska null returneras.

    hittaFordon i Register, hittaFordon i Agare, laggTillFordon Register samt laggTillFordon i Agare

    <div style="text-align: right; font-style: italic">(10p)</div>
    <div style="text-align: right; font-style: italic">(Totalt: 30p)</div>

* b) Implementera metoden skrivutAllaAgarensFordon(String pnr): void i klassen Register. 

    Metoden ska skriva ut alla fordon som en viss ägare äger (både regNr och märke). Om ingen ägare hittas skrivs ingenting ut. 

<div style="text-align: right; font-style: italic">(20p)</div>

* c) Implementera en klass (testmetod/mainmetod).

    Programmet ska skapa ett register, samt 4 fordon (1 motorcykel).

    Alla relationer ska dubbelkopplas, utom Register.

    Skapa följande fordon med tillhörande ägare och lägg in fordonen i registret.

    Skapa följande fordon:
    > regNr: ABC123, marke: Volvo och arsmodell: 99.
    > regNr: CBA123, marke: SAAB och arsmodell: 02.
    > regNr: ABC321, marke: Hyundai och arsmodell: 14.
    
    Samt motorcykeln:
    > regNr: BAB222, marke: BMW och arsmodell: 15.
    
    Skapa följande ägare till fordonen ovan:
    > personnummer: 111, namn: Rolke af Sturup
    > personnummer: 222, namn: Kristin af Kastrup
    
    Lägg fordon ABC123 och fordon CBA123 till Rolke.
    
    Lägg till fordon ABC321 och fordon (Motorcykel) BAB222 till Kristin.
    
    - Lägg till alla fyra fordonen till registret.
    - Skriv ut en ägares alla bilar via metoden skrivutAllaAgarensFordon
    - Skriv ut alla fordon (regnr, märke samt ägarens namn) som finns i registret. (10 p)

    Exempel på utskrift:

    ```
    ABC123 Volvo Rolke af Sturup
    CBA123 SAAB Rolke af Sturup
    ABC321 Hyundai Kristin af Kastrup
    BAB222 BMW Kristin af Kastrup
    ```

 <div style="text-align: right; font-style: italic">(30p)</div>