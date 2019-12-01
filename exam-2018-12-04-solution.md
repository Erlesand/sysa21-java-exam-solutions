# Tentamen 2018-12-04

## Uppgift 1 (10p)
Vi har följande kod:

```java
public class A {
    public void hej() {
        System.out.println("Hej ifrån A");
    }

    public void hello1() {
        this.hej(); 
    }

    public void hello2() {
        this.hello1(); 
    }
}

public class B extends A {
    public void hej() {
        System.out.println("Hej ifrån B");
    }

    public void hej1() {
        this.hej(); 
    }

    public void hej2() {
        this.hello1(); 
    }

    public void hej2a() {
        this.hello2(); 
    }

    public void hello2() {
        super.hello2(); 
    }
}
```

Vad skrivs ut när följande kod utförs?
Om inget skrivs ut, skriv ***Inget***

```java
A a = new A(); 
B b = new B(); 
```

| Nr | Kod          |
|----|--------------|
|  1 | a.hej();     | 
|  2 | b.hej();     |
|  3 | b.hej1();    |
|  4 | b.hello1();  |
|  5 | a.hello2();  |
|  6 | b.hello2();  |
|  7 | b.hej2a();   |

 
 # Uppgift 2 (20p)

| Person                     |
|----------------------------|
| fnamn: String {id}         |
| enamn : String {id}        |
| address : String           |
| equals(Object t) : boolean |

Skriv/implementera metoden equals, om fnamn och enamn är unika tillsammans. DVS. Både för och efternamn måste vara lika för att det ska vara samma person. 

```java
public class Person {
    private String fnamn; 
    private String enamn; 
    private String address; 

    public String getFnamn() {
        return this.fnamn;
    }

    public void setFnamn(String fnamn) {
        this.fnamn = fnamn;
    }

    public String getEnamn() {
        return this.enamn; 
    }

    public void setEnamn(String enamn) {
        this.enamn = enamn;
    }

    public String getAddress() {
        return this.address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public boolean equals(Object t) {
        return this.getFnamn().equals(((Person) t).getFnamn()) &&
            this.getEnamn().equals(((Person) t).getEnamn());
    }
}
```

Man ska kunna jämföra person1.equals(person2), vilket ska ge sant om båda personernas för och efternamn är lika. 

# Uppgift 3 (70p)

![](images/2018-12-04&#32;-&#32;Figure&#32;3.1.png)

* a) Implementera modellen ovan (Figur 3.1). Alla instansvariabler skall vara privata och ha
publika åtkomstmetoder. Associationen ska vara dubbelkopplad. 

    <div style="text-align: right; font-style: italic">(10p)</div>

    ```java
    import java.util.HashMap; 

    public class Hamn {
        private String adress;
        private String namn; 
        private HashMap<Integer, Batplats> batplats = new HashMap<Integer, Batplats>();

        public String getAdress() {
            return this.adress;
        }

        public void setAdress(String adress) {
            this.adress = adress;
        }

        public String getNamn() {
            return this.namn;
        }

        public void setNamn(String namn) {
            this.namn = namn; 
        }

        public HashMap<Integer, Batplats> getBatplats() {
            return this.batplats;
        }

        public void setBatplats(HashMap<Integer, Batplats> batplats) {
            this.batplats = batplats;
        }
    }
    ```

    ```java
    import java.util.HashMap; 

    public class Batplats {
        private int nr;
        private double hyra;
        private Hamn hamn;
        private HashMap<String, Hyrestagare> hyrestagare = new HashMap<String, Hyrestagare>();

        public int getNr() {
            return this.nr; 
        }

        public void setNr(int nr) {
            this.nr = nr;
        }

        public double getHyra() {
            return this.hyra;
        }

        public void setHyra(double hyra) {
            this.hyra = hyra;
        }

        public Hamn getHamn() {
            return this.hamn;
        }

        public void setHamn(Hamn hamn) {
            this.hamn = hamn;
        }

        public HashMap<String, Hyrestagare> getHyrestagare() {
            return this.hyrestagare;
        }

        public void setHyrestagare(HashMap<String, Hyrestagare> hyrestagare) {
            this.hyrestagare = hyrestagare;
        }
    }
    ```

    ```java
    public class Hyrestagare {
        public String nr; 
        public String namn;
        public Batplats batplats;

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

        public Batplats getBatplats() {
            return this.batplats;
        }

        public void setBatplats(Batplats batplats) {
            this.batplats = batplats; 
        }
    }
    ```

    **laggTillBatplats**-metoden i Hamn ska lägga till en båtplats och **hittaBatplats**-metoden ska hitta och returnera en batplats (nr i Batplats är unikt). Om ingen båtplats med aktuellt nummer hittas ska null returneras. 

    **laggTillBatplats** och **hittaBatplats** i klassen Hamn samt **laggTillHyrestagare**  och **hittaHyrestagare** i klassen Batplats.

    <div style="text-align: right; font-style: italic">(10p)</div>

    ```java
    public class Hamn {
        // ...

        public void laggTillBatplats(Batplats p) {
            this.getBatplats().put(p.getNr(), p);
        }

        public Batplats hittaBatplats(int nr) {
            return this.getBatplats().get(nr);
        }
    }
    ```

    ```java
    public class Batplats {
        // ...

        public void laggTillHyrestagare(Hyrestagare h) {
            this.getHyrestagare().put(h.getNr(), h);
        }

        public Hyrestagare hittaHyrestagare(String nr) {
            return this.getHyrestagare().get(nr);
        }
    }
    ```

    <div style="text-align: right; font-style: italic">(Totalt: 25p)</div>

* b) Implementera metoden laggTillHyrestagare(...) i klassen Hamn. Hyrestagaren ska läggas till båtplatsen samt båtplatsen ska läggas till hyrestagaren (dubbelkoppling). 

    <div style="text-align: right; font-style: italic">(10p)</div>

    ```java
    public class Hamn {
        public void laggTillHyrestagare(Hyrestagare h, int batPlatsNr) {
            Batplats batplats = this.hittaBatplats(batPlatsNr);

            batplats.laggTillHyrestagare(h); 
            h.setBatplats(batplats);
        }
    }
    ```

* c) Implementera metoden **hittaHyrestagarensBatplats(...) : int** i klassen Hamn. Metoden ska hitta en hyrestagares båtplats. Om ingen hyrestagare hittas så ska 0 returneras. 

    <div style="text-align: right; font-style: italic">(15p)</div>

    ```java
    public class Hamn {
        public int hittaHyrestagarensBatplats(String hyrestagareNr) {
            for (Batplats batplats : this.getBatplats().values()) {
                if (batplats.getHyrestagare().getNr().equals(hyrestagareNr)) {
                    return batplats.getNr(); 
                }
            }

            return 0;
        }
    }
    ```

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

```java
public class Test {
    public static void main(String[] args) {
        Hamn hamn = new Hamn(); 
        hamn.setAdress("Hamngatan 1");
        hamn.setNamn("Aqua");

        Batplats batplats1 = new Batplats(); 
        batplats1.setNr(1);
        batplats1.setHyra(12000);
        
        Batplats batplats2 = new Batplats(); 
        batplats2.setNr(2);
        batplats2.setHyra(10000);

        Batplats batplats3 = new Batplats(); 
        batplats3.setNr(3);
        batplats3.setHyra(8000);

        Hyrestagare hyrestagare1 = new Hyrestagare(); 
        hyrestagare1.setNr("h1");
        hyrestagare1.setNamn("Mats");

        Hyrestagare hyrestagare2 = new Hyrestagare(); 
        hyrestagare2.setNr("h2");
        hyrestagare2.setNamn("Viktoria");
        
        Hyrestagare hyrestagare3 = new Hyrestagare(); 
        hyrestagare3.setNr("h3");
        hyrestagare3.setNamn("Anders");
        
        Hyrestagare hyrestagare4 = new Hyrestagare(); 
        hyrestagare4.setNr("h4");
        hyrestagare4.setNamn("Anna");
        
        Hyrestagare hyrestagare5 = new Hyrestagare(); 
        hyrestagare5.setNr("h5");
        hyrestagare5.setNamn("Eva");
        
        Hyrestagare hyrestagare6 = new Hyrestagare(); 
        hyrestagare6.setNr("h6");
        hyrestagare6.setNamn("Sven");

        hamn.laggTillBatplats(batplats1);
        hamn.laggTillBatplats(batplats2);
        hamn.laggTillBatplats(batplats3);
        
        hamn.laggTillHyrestagare(hyrestagare1, batplats1.getNr());
        hamn.laggTillHyrestagare(hyrestagare2, batplats1.getNr());
        hamn.laggTillHyrestagare(hyrestagare3, batplats2.getNr());
        hamn.laggTillHyrestagare(hyrestagare4, batplats2.getNr());
        hamn.laggTillHyrestagare(hyrestagare5, batplats3.getNr());
        hamn.laggTillHyrestagare(hyrestagare6, batplats3.getNr());

        hamn.hittaHyrestagarensBatplats(hyrestagare5.getNr());

        for (Batplats batplats : hamn.getBatplats().values()) {
            for (Hyrestagare hyrestagare : batplats.getHyrestagare().values()) {
                System.out.println(hyrestagare.getNamn());
            }
        }
    }
}
```