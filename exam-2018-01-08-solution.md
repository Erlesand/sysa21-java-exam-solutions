# Tentamen 2019-05-11

## Uppgift 1 (20p)
Vi har följande kod:

img[]()

Vad skrivs ut när följande kod utförs?
Om inget skrivs ut, skriv ***inget***

```java
Parrot birdy = new Parrot(); 
birdy.setName("Birdy");
Dog fido = new Dog(); 
fido.setName("Fido");
```

| Nr | Kod                                 | Utskrift             | Från rad |
|----|-------------------------------------|----------------------|:--------:|
|  1 | fido.talk()                         | I can not talk.      | 17       |
|  2 | birdy.talk();                       | I can not talk.      | 17       |
|  3 | fido.beQuiet()                      | Inget                | -        |
|  4 | fido.talk()                         | Woof                 | 43       |
|  5 | birdy.talk()                        | I can not talk.      | 17       |
|  6 | birdy.learn("Birdy want a cracker") | Birdy want a cracker | 13       |
|  7 | birdy.talk()                        | Birdy want a cracker | 13       |
|  8 | fido.setName("Doggy")               | Inget                | -        |
|  9 | birdy.whatsYourName()               | My name is Birdy     | 22       |
| 10 | fido.whatsYourName()                | My name is Fido      | 22       |
 
 # Uppgift 2 (80p)

![](images/2018-01-08&#32;-&#32;Figure&#32;2.1.png)

* a) Implementera modellen ovan (Figur 2.1). Alla instansvariabler skall vara privata och ha
publika åtkomstmetoder. 

    ```java
    import java.util.HashMap; 

    public class OOAB {
        private String nr;
        private String namn;
        public HashMap<String, Dotterbolag> dotterbolag = new HashMap<String, Dotterbolag>(); 

        public String getNr() {
            return this.nr;
        } 

        public void setNr(String nr) {
            this.nr = nr;
        }

        public String getNamn() {
            return this.namn; 
        }

        public void setNamn(String namn) {
            this.namn = namn; 
        }

        public HashMap<String, Dotterbolag> getDotterbolag() {
            return this.dotterbolag; 
        }

        public void setDotterbolag(HashMap<String, Dotterbolag> dotterbolag) {
            this.dotterbolag = dotterbolag;
        }
    }
    ```

    ```java
    import java.util.HashMap; 

    public class Dotterbolag {
        private String nr;
        private String namn;
        private HashMap<String, Projekt> projekt = new HashMap<String, Projekt>();
        private HashMap<String, Anstalld> anstallda = new HashMap<String, Anstalld>();

        public String getNr() {
            return this.nr;
        } 

        public void setNr(String nr) {
            this.nr = nr;
        }

        public String getNamn() {
            return this.namn; 
        }

        public void setNamn(String namn) {
            this.namn = namn; 
        }

         public HashMap<String, Projekt> getProjekt() {
            return this.projekt; 
        }

        public void setProjekt(HashMap<String, Projekt> projekt) {
            this.projekt = projekt;
        }

         public HashMap<String, Anstalld> getAnstalld() {
            return this.anstallda; 
        }

        public void setAnstalld(HashMap<String, Anstalld> anstallda) {
            this.anstallda = anstallda;
        }
    }
    ```

    ```java
    public class Anstalld {
        private String pnr;
        private String namn;
        private Dotterbolag dotterbolag;

        public String getPnr() {
            return this.pnr;
        } 

        public void setPnr(String pnr) {
            this.pnr = pnr;
        }

        public String getNamn() {
            return this.namn; 
        }

        public void setNamn(String namn) {
            this.namn = namn; 
        }

        public Dotterbolag getDotterbolag() {
            return this.dotterbolag;
        }

        public void setDotterbolag(Dotterbolag dotterbolag)
        {
            this.dotterbolag = dotterbolag; 
        }
    }
    ```

    ```java
    public class Projekt {
        private String namn;
        private double budget;
        private Dotterbolag dotterbolag;

        public String getNamn() {
            return this.namn; 
        }

        public void setNamn(String namn) {
            this.namn = namn; 
        }

        public double getBudget() {
            return this.budget;
        } 

        public void setBudget(double budget) {
            this.budget = budget;
        }

        public Dotterbolag getDotterbolag() {
            return this.dotterbolag;
        }

        public void setDotterbolag(Dotterbolag dotterbolag)
        {
            this.dotterbolag = dotterbolag; 
        }
    }
    ```

    **laggTillDotterbolag**-metoden i OOAB ska lägga till ett dotterbolag och
**hittaDotterbolag**-metoden ska hitta och returnera ett dotterbolag (nr i Dotterbolag är unikt). Om
inget dotterbolag med aktuellt nummer hittas ska null returneras.

    Vidare ska **laggTillProjekt**-metoden i OOAB lägga till ett projekt till ett givet dotterbolag.

    **laggTillAnstalld** i Dotterbolag ska lägga till en anställd och **laggTillProjekt** ska lägga till ett projekt
till dotterbolaget.

    **laggTillDotterbolag**, **laggTillProjekt** och **hittaDotterbolag** i OOAB samt **laggTillAnstalld** och
**laggTillProjekt** i Dotterbolag.

    ```java
    public class OOAB {
        // ...

        public void laggTillDotterbolag(Dotterbolag d) {
            this.dotterbolag.put(d.getNr(), d);
        }

        public Dotterbolag hittaDotterbolag(String nr) {
            return this.dotterbolag.get(nr);
        }

        public void laggTillProjekt(String dotterNr, Projekt projekt) {
            Dotterbolag dotterbolag = this.hittaDotterbolag(dotterNr);

            if (dotterbolag != null) {
                dotterbolag.laggTillProjekt(projekt);
            }
        }
    }
    ```

    ```java
    public class Dotterbolag {
        // ...

        public void laggTillAnstalld(Anstalld anstalld) {
            this.anstallda.put(anstalld.getPnr(), anstalld);
        }

        public void laggTillProjekt(Projekt projekt) {
            this.projekt.put(projekt.getNamn(), projekt);
        }
    }
    ```

    <div style="text-align: right; font-style: italic">(10p)</div>
    <div style="text-align: right; font-style: italic">(Totalt: 30p)</div>

* b) Implementera metoden totalBudget() i klassen OOAB samt totalBudget() i klassen Dotterbolag

    Metoden totalBudget() i klassen Dotterbolag ska returnera totalbudget for alla projekt som ingår i ett dotterbolag.

    Metoden totalBudget() i klassen OOAB ska returnera alla ingående dotterbolags totala budget. 

    ```java
    public class Dotterbolag {
        // ...

        public double totalBudget() {
            double total = 0.0; 

            for (Projekt tmpProjekt : this.getProjekt().values()) {
                total += tmpProjekt.getBudget(); 
            }

            return total; 
        }
    }
    ```

    ```java
    public class OOAB {
        // ...

        public double totalBudget() {
            double total = 0.0;

            for (Dotterbolag tmpDotterbolag : this.getDotterbolag().values()) {
                total += tmpDotterbolag.totalBudget(); 
            }

            return total;
        }
    }
    ```

<div style="text-align: right; font-style: italic">(20p)</div>

* c) Implementera en klass (testmetod/mainmetod).

    Programmet ska skapa ett OOAB, samt 2 dotterbolag.
    Dotterbolag-Anstalld associationen ska dubbelkopplas.

    Testprogrammet skall skapa ett OOAB enligt följande:

    ```
    556512(OOAB nr), Acme AB( OOAB namn)
        1a (Dotterbolagets bolagsnummer), Acme Sweden (namn)
            Nyinvestering (projektets namn), 1 000 000 (Budget)
        1b (Dotterbolagets bolagsnummer), Acme Denmark (namn)
            Databaser (projektets namn), 300 000 (Budget)
            Underhåll (projektets namn), 500 000 (Budget)
            2 personer som arbetar på Acme Denmark. (Dubbel kopplas)
    ```

- Lägg till ett projekt mha. laggTillProjekt-metoden i OOAB.
 <div style="text-align: right; font-style: italic">(5p)</div>

- Skriv ut OOAB’s (Acme AB) totala budget.
- Skriv ut alla dottebolag (namn) som finns i Acme AB samt dess projekt (namn räcker). (10 p)

    Exempel på utskrift:

    ```
    Acme Sweden
    - Nyinvestering
    Acme Denmark
    - Databaser
    - Underhåll
    Total budget:1800000
    ```

    ```java
    public class Test {
        public static void main(String[] args) {
            OOAB ooab = new OOAB(); 
            ooab.setNr("556512");
            ooab.setNamn("Acme AB");

            Dotterbolag dotterbolag1a = new Dotterbolag(); 
            dotterbolag1a.setNr("1a");
            dotterbolag1a.setNamn("Acme Sweden");

            Dotterbolag dotterbolag1b = new Dotterbolag(); 
            dotterbolag1b.setNr("1b");
            dotterbolag1b.setNamn("Acme Denmark");

            Projekt projektA = new Projekt(); 
            projektA.setNamn("Nyinvestering");
            projektA.setBudget(1000000);

            Projekt projektB = new Projekt(); 
            projektB.setNamn("Databaser");
            projektB.setBudget(300000);

            Projekt projektC = new Projekt(); 
            projektC.setNamn("Underhåll");
            projektC.setBudget(500000);

            Anstalld anstalldA = new Anstalld();
            anstalldA.setPnr("010203-0405");
            anstalldA.setNamn("John Doe");
            Anstalld anstalldB = new Anstalld(); 
            anstalldB.setPnr("020404-0506");
            anstalldA.setNamn("Jane Doe");

            // Association: Dotterbolag <---> Anstalld
            anstalldA.setDotterbolag(dotterbolag1b);
            dotterbolag1b.laggTillAnstalld(anstalldA);
            anstalldB.setDotterbolag(dotterbolag1b);
            dotterbolag1b.laggTillAnstalld(anstalldB);

            // Association: OOAB <---> Dotterbolag
            ooab.laggTillDotterbolag(dotterbolag1a);
            ooab.laggTillDotterbolag(dotterbolag1b);
            
            // Association: Dotterbolag --> Projekt
            dotterbolag1a.laggTillProjekt(projektA);
            dotterbolag1b.laggTillProjekt(projektB);
            ooab.laggTillProjekt(dotterbolag1b.getNr(), projektC);

            for(Dotterbolag dotterbolag : ooab.getDotterbolag().values())  {
                System.out.println(dotterbolag.getNamn());

                for (Projekt projekt : dotterbolag.getProjekt().values()) {
                    System.out.println("- " + projekt.getNamn());
                }
            }

            System.out.println("Total budget: " + ooab.totalBudget());
        }
    }
    ```
 <div style="text-align: right; font-style: italic">(30p)</div>