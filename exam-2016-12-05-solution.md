# Tentamen 2018-01-08

## Uppgift 1 (20p)
Vi har följande kod:

```java
int max = 5;
int[] minArray = {4, 6, -2, -12, 1};
for (int k=0; k<max; k++) {
    System.out.println("["+k+"] = " + (minArray[k]+1));
}

System.out.println();

minArray[3-1] = minArray[3] + (max+1);
minArray [4] = minArray[2-1] + minArray[2];
minArray [2] += minArray[2-1];

for (int k=0; k<max; k++) {
    System.out.println("["+k+"] = " + minArray[k]);
}
```

Vad skrivs ut när följande kod utförs?

```
[0] = 5
[1] = 7
[2] = -1
[3] = -11
[4] = 2

[0] = 4
[1] = 6
[2] = 0
[3] = -12
[4] = 0
```
 
 # Uppgift 2 (10p)

![](images/2016-12-05&#32;-&#32;Figure&#32;2.1.png)

```java
public class Test {
    public static void main(String[] args) {
        Customer c = new Customer();
        c.setName("K1");

        Customer c2 = c;
        c.setNbrOf(4+1);
        c2.setNbrOf(c.getNbrOf()+1);
        int tal = c.getNbrOf()+5;
        System.out.println("Namn: "+c.getName()+" ålder: "+c2.getNbrOf());
        andra(c, ++tal);
        System.out.println("Namn: "+c.getName()+" ålder: "+c.getNbrOf()+", Tal: "+tal);
    }

    public static void andra(Customer p, int tal) {
        p.setName("K2");
        tal=9;
        p.setNbrOf(tal);
    }
}
```

Vad skrivs ut när följande kod (klassen Test) utförs?

```java
Namn: K1 ålder: 6 
Namn: K2 ålder: 9, Tal: 12
```

# Uppgift 3 (70p)

![](images/2016-12-05&#32;-&#32;Figure&#32;3.1.png)

* a) Implementera modellen ovan (Figur 3.1). Alla instansvariabler skall vara privata och ha publika åtkomstmetoder. 

    ```java
    import java.util.ArrayList; 

    public class Hus {
        private String address;
        private int inkopspris;
        private ArrayList<Lagenhet> lagenheter = new ArrayList<Lagenhet>();

        public String getAddress() {
            return this.address;
        }

        public void setAddress(String address) {
            this.address = address;
        }

        public int getInkopspris() {
            return this.inkopspris;
        }

        public void setInkopspris(int inkopspris) {
            this.inkopspris = inkopspris;
        }

        public ArrayList<Lagenhet> getLagenheter() {
            return this.lagenheter;
        }

        public void setLagenheter(ArrayList<Lagenhet> lagenheter) {
            this.lagenheter = lagenheter;
        }
    }
    ```

    ```java
    import java.util.ArrayList; 

    public class Lagenhet {
        private int nummer;
        private int hyra;
        private int yta;

        public int getNummer() {
            return this.nummer;
        }

        public void setNummer(int nummer) {
            this.nummer = nummer;
        }

        public int getHyra() {
            return this.hyra;
        }

        public void setHyra(int hyra) {
            this.hyra = hyra;
        }

        public int getYta() {
            return this.yta;
        }

        public void setYta(int yta) {
            this.yta = yta;
        }

        public Hus getHus() {
            return this.hus;
        }

        public void setHus(Hus hus) {
            this.hus = hus;
        }
    }
    ```

    ```java
    public class Hyrestagare {
        private String personnummer; 
        private String namn; 
        private Lagenhet lagenhet; 

        public String getPersonnummer() {
            return this.personnummer;
        }

        public void setPersonnummer(String personnummer) {
            this.personnummer = personnummer; 
        } 

        public String getNamn() {
            return this.namn;
        }

        public void setNamn(String namn) {
            this.namn = namn; 
        }

        public Lagenhet getLagenhet() {
            return this.lagenhet;
        }

        public void setLagenhet(Lagenhet lagenhet) {
            this.lagenhet = lagenhet;
        }
    }
    ```

    **laggTillLagenhet**-metoden i Hus ska lägga till en lägenhet och
**hittaLagenhet**-metoden ska hitta och returnera en lägenhet (nummer i Lagenhet är
unikt). Om ingen lägenhet med aktuellt nummer hittas ska null returneras. 

    Vidare ska **laggTillHyrestagare**-metoden i Lagenhet lägga till en hyrestagare till lägenheten och **hittaHyrestagare**-metoden ska hitta en viss hyrestagare. Om hyrestagaren inte hittas ska null returneras.

    **hittaLagenhet**, **hittaHyrestagare**, **laggTillLagenhet** samt **laggTillHyrestagare**.

    ```java
    public class Hus {
        // ...

        public void laggTillLagenhet(Lagenhet lagenhet) {
            this.lagenheter.add(lagenhet);
        }

        public Lagenhet hittaLagenhet(int lNr) {
            for (Lagenhet lagenhet : this.lagenheter) {
                if (lagenhet.getNummer() == lNr) {
                    return lagenhet;
                }
            }

            return null;
        }
    }

    public class Lagenhet {
        private Hus hus;
        private ArrayList<Hyrestagare> hyrestagare = new ArrayList<Hyrestagare>();

        // ...

        public ArrayList<Hyrestagare> getHyrestagare() {
            return this.hyrestagare;
        }

        public void setHyrestagare(ArrayList<Hyrestagare> hyrestagare) {
            this.hyrestgare = hyrestagare;
        }

        public Hyrestagare hittaHyrestagare(String pnr) {
            for (Hyrestagare hyrestagare : this.hyrestagare) {
                if (hyrestagare.getPersonnummer().equals(pnr)) {
                    return hyrestagare;
                }
            }

            return null;
        }

        public void läggTillHyrestagare(Hyrestagare hyrestagare) {
            this.hyrestagare.add(hyrestagare);
        }
    }
    ```

    <div style="text-align: right; font-style: italic">(10p)</div>

    totalHyra som returnerar den totala månadshyran för ett hus. (hyra attributet i Lagenhet är månadshyra). TotalHyra-metoden ska alltså returnera den sammanlagda hyran för alla lägenheterna i ett hus.

    ```java
    class Hus {
        // ...

        public int totalHyra() {
            int total = 0;

            for (Lagenhet lagenhet : this.getLagenheter()) {
                total += lagenhet.getHyra(); 
            }

            return total;
        }
    }
    ```

    <div style="text-align: right; font-style: italic">(10p)</div>

    <div style="text-align: right; font-style: italic">(Totalt: 30p)</div>

* b) Implementera metoden **vemHyrLagenhet**(int lagenhetsnummer): ArrayList\<Hyrestagare> i klassen Hus.

    Om inte lägenheten finns ska null returneras. Om inte någon hyrestagare finns ska en tom ArrayList\<Hyrestagare> returneras. Metoden ska returnera alla hyrestagarna för en viss lägenhet. 

    <div style="text-align: right; font-style: italic">(20p)</div>

    ```java
    public class Hus {
        // ...

        public ArrayList<Hyrestagare> vemHyrLagenhet(int lagenhetsnummer) {
            ArrayList<Hyrestagare> allaHyrestagare = new ArrayList<Hyrestagare>();

            Lagenhet lagenhet = this.hittaLagenhet(lagenhetsnummer); 
            if (lagenhet != null) {
                for (Hyrestagare hyrestagare : lagenhet.getHyrestagare()) {
                    if (hyrestagare.getLagenhet().getNummer() == lagenhetsnummer) {
                        allaHyrestagare.add(hyrestagare);
                    }
                }
            }

            return allaHyrestagare;
        }
    }
    ```

* c) Implementera en klass (testmetod/mainmetod) som provar **ALLA** metoder.

    Programmet ska skapa ett hus, samt 2 lägenheter som har 2 hyrestagare vardera. Alla
    relationer ska dubbelkopplas, utom Hus.

    Skapa följande lägenheter med tillhörande hyrestagare och lägg in lägenheterna till huset.

    Skapa följande lägenhet:
    ```
    nummer: L1, hyra: 6800 och yta: 69.
    nummer: L2, hyra: 8700 och yta: 82.
    ```

    Skapa följande hyrestagare till lägenheterna ovan:
    ```
    personnummer: 111, namn: Rolke af Sturup
    personnummer: 222, namn: Kristin af Sturup
    personnummer: 333, namn: Sten Stensson
    personnummer: 444, namn: Tove Stensson
    ```

    Lägg till Rolke och Kristin till lägenhet L1 och Sten och Tove till lägenhet L2.

    Lägg till båda lägenheterna till huset.
    
    Skriv ut totalhyran för huset via metoden totalHyra
    
    Skriv ut alla hyrestagarna via vemHyrLagenhet

    ```java
    public class Test {
        public static void main(String[] args) {
            Hus hus = new Hus(); 
            hus.setAddress("Norrmalmstorg 1");
            hus.setInkopspris(18000000);

            Lagenhet lagenhetA = new Lagenhet(); 
            lagenhetA.setNummer(1);
            lagenhetA.setHyra(6800);
            lagenhetA.setYta(69);

            Lagenhet lagenhetB = new Lagenhet(); 
            lagenhetB.setNummer(2);
            lagenhetB.setHyra(8700);
            lagenhetB.setYta(82);
            
            Hyrestagare hyrestagareA = new Hyrestagare(); 
            hyrestagareA.setPersonnummer("111");
            hyrestagareA.setNamn("Rolke af Sturup");
            
            Hyrestagare hyrestagareB = new Hyrestagare(); 
            hyrestagareB.setPersonnummer("222");
            hyrestagareB.setNamn("Kristin af Sturup");
            
            Hyrestagare hyrestagareC = new Hyrestagare(); 
            hyrestagareC.setPersonnummer("333");
            hyrestagareC.setNamn("Sten Stensson");
            
            Hyrestagare hyrestagareD = new Hyrestagare(); 
            hyrestagareD.setPersonnummer("444");
            hyrestagareD.setNamn("Tove Stensson");

            // Association: Hus --> Lagenhet
            hus.laggTillLagenhet(lagenhetA);
            hus.laggTillLagenhet(lagenhetB);

            // Association: Lagenhet <---> Hyrestagare
            lagenhetA.laggTillHyrestagare(hyrestagareA);
            lagenhetA.laggTillHyrestagare(hyrestagareB);
            lagenhetB.laggTillHyrestagare(hyrestagareC);
            lagenhetB.laggTillHyrestagare(hyrestagareD);

            hyrestagareA.setLagenhet(lagenhetA);
            hyrestagareB.setLagenhet(lagenhetA);
            hyrestagareC.setLagenhet(lagenhetB);
            hyrestagareD.setLagenhet(lagenhetB);

            System.out.println("Totalhyran för huset är: " + hus.totalHyra());

            for (Hyrestagare hyrestagare : hus.vemHyrLagenhet(lagenhetA.getNummer())) {
                System.out.println(lagenhetA.getNummer() + ": " + hyrestagare.getNamn());
            }

            Lagenhet hittaLagenhetB = hus.hittaLagenhet(lagenhetB.getNummer());
            for (Hyrestagare hyrestagare : hus.vemHyrLagenhet(hittaLagenhetB.getNummer())) {
                System.out.println(hyrestagare.getLagenhet().getNummer() + ": " + hyrestagare.getNamn());
            }
        }
    }
    ```

 <div style="text-align: right; font-style: italic">(20p)</div>