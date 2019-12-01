# Tentamen 2018-12-04

## Uppgift 1 (10p)
Vi har följande kod:

![](images/2018-12-04&#32;-&#32;Code&#32;1.png)
Vad skrivs ut när följande kod utförs?
Om inget skrivs ut, skriv ***Inget***

```java
A a = new A(); 
B b = new B(); 
```

| Nr | Kod          | Utskrift    | Från rad              |
|----|--------------|-------------|:---------------------:|
|  1 | a.hej();     | Hej ifrån A | 3                     |
|  2 | b.hej();     | Hej ifrån B | 17                    |
|  3 | b.hej1();    | Hej ifrån B | 21 > 17               |
|  4 | b.hello1();  | Hej ifrån B | 7 > 17                |
|  5 | a.hello2();  | Hej ifrån A | 11 > 7 > 3            |
|  6 | b.hello2();  | Hej ifrån B | 33 > 11 > 7 > 17      |
|  7 | b.hej2a();   | Hej ifrån B | 29 > 33 > 11 > 7 > 17 |

 # Uppgift 2 (20p)

| Person                     |
|----------------------------|
| fnamn: String {id}         |
| enamn : String {id}        |
| address : String           |
| equals(Object t) : boolean |

Skriv/implementera metoden equals, om fnamn och enamn är unika tillsammans. DVS. Både för och efternamn måste vara lika för att det ska vara samma person. 

```java
public boolean equals(Object t) {
    // ...
}
```

Man ska kunna jämföra person1.equals(person2), vilket ska ge sant om båda personernas för och efternamn är lika. 

# Uppgift 3 (70p)

![](images/2018-12-04&#32;-&#32;Figure&#32;3.1.png)

* a) Implementera modellen ovan (Figur 3.1). Alla instansvariabler skall vara privata och ha
publika åtkomstmetoder. Associationen ska vara dubbelkopplad. 

    <div style="text-align: right; font-style: italic">(10p)</div>

    laggTillBatplats-metoden i Hamn ska lägga till en båtplats och hittaBatplats-metoden ska hitta och returnera en batplats (nr i Batplats är unikt). Om ingen båtplats med aktuellt nummer hittas ska null returneras. 

    laggTillBatplats och hittaBatplats i klassen Hamn samt laggTillHyrestagare  och hittaHyrestagare i klassen Batplats.

    <div style="text-align: right; font-style: italic">(10p)</div>

    <div style="text-align: right; font-style: italic">(Totalt: 25p)</div>

* b) Implementera metoden laggTillHyrestagare(...) i klassen Hamn. Hyrestagaren ska läggas till båtplatsen samt båtplatsen ska läggas till hyrestagaren (dubbelkoppling). 

    <div style="text-align: right; font-style: italic">(10p)</div>

* c) Implementera metoden **hittaHyrestagarensBatplats(...) : int** i klassen Hamn. Metoden ska hitta en hyrestagares båtplats. Om ingen hyrestagare hittas så ska 0 returneras. 

    <div style="text-align: right; font-style: italic">(15p)</div>

* d) Implementera en klass (testmetod/mainmetod).

    Programmet ska skapa en hamn, tre båtplatser och sex hyrestagare.

    Testprogrammet ska skapa en hamn enligt följande: 

    > Hamngatan 1 (adress), Aqua (namn) 

    som har följande båtplatser och hyrestagare:

    ```
    2 hyrestagare som hyr båtplats 1 med hyra 12000
       h1 (nr), Mats (namn)
       h2 (nr), Viktoria (namn)
    2 hyrestagare som hyr båtplats 2 med hyra 10000
       h3 (nr), Anders (namn)
       h4 (nr), Anna (namn)
    2 hyrestagare som hyr båtplats 1 med hyra 8000
       h5 (nr), Eva (namn)
       h6 (nr), Sven (namn)
    ```

- Skriv ut hyrestagaren h5:s båtplats med hjläp av metoden **hittaHyrestagarensBatplats** (bode bli båtplats 3). 

- Skriv ut alla hyrestagare (namn) som hyr någon båtplats i hamnen Aqua (namn räcker).

    Exempel på utskrift:

    ```
    Mats
    Viktoria
    Anders
    Anna
    Eva
    Sven
    ```

 <div style="text-align: right; font-style: italic">(Totalt: 20p)</div>