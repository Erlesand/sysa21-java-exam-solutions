# Tentamen 2019-05-11

## Uppgift 1 (20p)
Vi har följande kod:

![](images/2019-05-11&#32;-&#32;Code&#32;1.png)

Vad skrivs ut när följande kod utförs?
Om inget skrivs ut, skriv ***Nada***

| Nr | Kod                  | Utskrift                                                    | Från rad      |
|----|----------------------|-------------------------------------------------------------|:-------------:|
| 1 | A.whatAreYou();       | Jag är inte klass B/C                                       | 7             |
| 2 | B.whatAreYou();       | Jag är klass B                                              | 18            |
| 3 | C.whatAreYou();       | Jag är inte klass C                                         | 29            |
| 4 | new A().whoAreYou();  | Jag är objekt A                                             | 3             |
| 5 | new A().whatAreYou(); | Jag är inte klass B/C                                       | 7             |
| 6 | new B().whoAreYou();  | Jag är objekt A<br>Jag är objekt av A                       | 3<br>14       |
| 7 | new C().whoAreYou();  | Jag är objekt av C<br>Jag är objekt A<br>Jag är objekt av A | 24<br>3<br>14 |

 # Uppgift 2 (80p)

![](images/2019-05-11&#32;-&#32;Figure&#32;2.1.png)


* a) Implementera modellen ovan (Figur 2.1). Alla instansvariabler skall vara privata och ha
publika åtkomstmetoder. 

    <div style="text-align: right; font-style: italic">(10p)</div>

```java
public class Tenant {
    private String nbr;
    private String name;
    private Mooring mooring;

    public String getNbr() {
        return this.nbr;
    }

    public void setNbr(String nbr) {
        this.nbr = nbr;
    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Mooring getMooring() {
        return this.mooring;
    }

    public void setMooring(Mooring mooring) {
        this.mooring = mooring;
    }
}
```

```java
public class Mooring {
    import java.util.ArrayList;

    private int nbr;
    private double rent;
    private String type;
    private ArrayList<String, Tenant> tenants = new ArrayList<Tenant>();
    private Marina marina;

    public int getNbr() {
        return this.nbr;
    }

    public void setNbr(int nbr) {
        this.nbr = nbr;
    }

    public double getRent() {
        return this.getRent;
    }

    public void setRent(double rent) {
        this.rent = rent;
    }

    public String getType() {
        return this.type;
    }

    public void setType(String type) {
        this.type = type;
    }

    public Tenant getTenants() {
        return this.tenants;
    }

    public void setTenants(ArrayList<Tenant> tenants) {
        this.tenants = tenants;
    }

    public Marina getMarina() {
        return this.marina;
    }

    public void setMarina(Marina marina) {
        this.marina = marina;
    }
}
```

```java
public class Marina {
    import java.util.ArrayList;
    
    private String address;
    private String name;
    private ArrayList<Mooring> moorings = new ArrayList<Mooring>();

    public String getAddress() {
        return this.address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public ArrayList<Mooring> getMoorings() {
        return this.moorings;
    }

    public void setMoorings(ArrayList<Mooring> moorings) {
        this.moorings = moorings;
    }
}
```

add-metoden i Marina ska lägga till en båtplats, find-metoden ska hitta och returnera en båtplats
(nbr i Mooring är unik). Om ingen båtplats med aktuellt nummer hittas ska null returneras. Vidare
ska findTenant metoden i klassen Marina hitta en hyresgäst (nbr i Tenant är unik), om ingen
hyresgäst med aktuellt nummer finns ska null returneras.
add, find och findTenant (10 poäng) i klassen Marina samt addTenant och findTenant i klassen
Mooring. 

    <div style="text-align: right; font-style: italic; margin-bottom: 2em;">(20p)</div>
    <div style="text-align: right; font-style: italic">(Totalt 30p)</div>

```java
public class Marina {
    // ...

    public void add(Mooring p) {
        this.moorings.add(p);
    }

    public Mooring find(int nbr) {
        for (Mooring mooring : this.moorings) {
            if (mooring.getNbr() == nbr) {
                return mooring;
            }

            return null;
        }
    }

    public Tenant findTenant(String tenantNbr) {
        for (Mooring mooring : this.moorings) {
            for (Tenant tenant : mooring.getTenants()) {
                if (tenant.getNbr().equals(tenantNbr)) {
                    return tenant;
                }
            }

            return null;
        }
    }
}
```

```java
public class Mooring {
    // ...

    public void addTenant(Tenant tenant) {
        this.tenants.add(tenant);
    }

    public Tenant findTenant(String nbr) {
        for (Tenant tenant : this.tenants) {
            if (tenant.getNbr().equals(nbr)) {
                return tenant;
            }
        }

        return null;
    }
}
```

* b) Implementera metoden nbrOfTenants():int i klassen Marina. Den ska returnera antalet hyresgäster som hyr båtplatser. 

<div style="text-align: right; font-style: italic">(10p)</div>

```java
class Marina {
    // ...

    public int nbrOfTenants() {
        int total = 0; 

        for (Mooring mooring : this.moorings) {
            total += mooring.getTenants().size();
        }

        return total;
    }
}
```

* c) Implementera metoderna getMarinaName():String i klassen Tenant och getMarinaName():String i klassen Mooring.

    getMarinaName():String i klassen Tenant ska returnera namnet på marinan, där hyresgästen hyr en båtplats

    getMarinaName():String i klassen Mooring ska returnera namnet på marinan, där båtplasen finns.

    <div style="text-align: right; font-style: italic">(10p)</div>

```java
class Tenant {
    // ...

    public String getMarinaName() {
        return this.mooring.getMarinaName();
    }
}
```

```java
class Mooring {
    // ...

    public String getMarinaName() {
        return this.marina.getName(); 
    }
}
```

* d) Implementera metoden getAllMooringsByType(String type):ArrayList<Mooring> i klassen Marina. 

    Metoden ska returnera alla lediga båtplatser av en viss typ.
    
    <div style="text-align: right; font-style: italic">(10p)</div>

```java
class Marina {
    // ...

    public ArrayList<Marina> getAllMooringsByType(String type) {
        ArrayList<Marina> moorings = new ArrayList<Marina>();

        for(Mooring mooring : this.moorings) {
            if (mooring.getType().equals(type)
                && mooring.getTenants().isEmpty()) {
                    this.moorings.add(mooring);
            }
        }

        return moorings;
    }
}
```

* e) Implementera en klass (testmetod/mainmetod).
    
    Programmet ska skapa en marina, 4 båtplatser och 6 hyrestagare.
    
    Testprogrammet skall skapa en Marina enligt följande:

    Hamngatan 1(adress), Aqua(namn) som har följande båtplatser och hyrestagare:

    2 hyrestagare som hyr båtplats 1 med hyra 12000 och typ Large
    - h1 (nr), Mats (namn)
    - h2 (nr), Viktoria (namn)

    2 hyrestagare som hyr båtplats 2 med hyra 10000 och typ Medium
    - h3 (nr), Anders (namn)
    - h4 (nr), Anna (namn)

    2 hyrestagare som hyr båtplats 3 med hyra 8000 och typ Small
    - h5 (nr), Eva (namn)
    - h6 (nr), Sven (namn)
 
    0 hyrestagare, men båtplats 4 med hyra 9000 och typ Medium 
    
    <div style="text-align: right; font-style: italic">(10p)</div>

  * Skriv ut antalet hyresgäster med hjälp av metoden nbrOfTenants(). (borde bli 6 st.)

  * Skriv ut hamnens namn ifrån hyresgästen h4.
(Använd metoden findTenant i klassen Marina för att hitta hyresgästen.)

  * Skriv ut marinans alla lediga båtplatser av typen Medium.
(Använd metoden getAllMooringsByType i klassen Marina)

    <div style="text-align: right; font-style: italic">(10p)</div>

    Exempel på utskrift:

    > Nbr: 4 Hyra: 9000.0
 
 <div style="text-align: right; font-style: italic">(Totalt : 20 p)</div>

 ```java
 public class Test {
     public static void main(String[] args) {
         Marina marina = new Marina(); 
         marina.setAddress("Hamngatan 1");
         marina.setName("Aqua");
         
         // Initiate all 4 moorings
         Mooring mooring1 = new Mooring(); 
         mooring1.setNbr("1");
         mooring1.setRent("12000");
         mooring1.setType("Large");

         Mooring mooring2 = new Mooring(); 
         mooring2.setNbr("2");
         mooring2.setRent("10000");
         mooring2.setType("Medium");

         Mooring mooring3 = new Mooring(); 
         mooring3.setNbr("3");
         mooring3.setRent("8000");
         mooring3.setType("Small");

         Mooring mooring4 = new Mooring(); 
         mooring4.setNbr("4");
         mooring4.setRent("9000");
         mooring4.setType("Medium");

        // Initiate 6 tenants and associate with moorings
        Tenant tenant1 = new Tenant(); 
        tenant1.setNr("h1");
        tenant1.setName("Mats");

        Tenant tenant2 = new Tenant(); 
        tenant2.setNr("h2");
        tenant2.setName("Viktoria");

        Tenant tenant3 = new Tenant(); 
        tenant3.setNr("h3");
        tenant3.setName("Anders");

        Tenant tenant4 = new Tenant(); 
        tenant4.setNr("h4");
        tenant4.setName("Anna");

        Tenant tenant5 = new Tenant(); 
        tenant5.setNr("h5");
        tenant5.setName("Eva");

        Tenant tenant6 = new Tenant(); 
        tenant6.setNr("h6");
        tenant6.setName("Sven");

        // Association: Marina -> Mooring [*]
        marina.add(mooring1);
        marina.add(mooring2);
        marina.add(mooring3);
        marina.add(mooring4);

        // Association: Mooring -> Marina [1]
        mooring1.setMarina(marina);
        mooring2.setMarina(marina);
        mooring3.setMarina(marina);
        mooring4.setMarina(marina);

        // Association: Mooring -> Tenant [*]
        mooring1.addTenant(tenant1);
        mooring1.addTenant(tenant2);
        mooring2.addTenant(tenant3);
        mooring2.addTenant(tenant4);
        mooring3.addTenant(tenant5);
        mooring3.addTenant(tenant6);

        // Association: Tenant -> Mooring [1]
        tenant1.setMooring(mooring1);
        tenant2.setMooring(mooring1);
        tenant3.setMooring(mooring2);
        tenant4.setMooring(mooring2);
        tenant5.setMooring(mooring3);
        tenant6.setMooring(mooring3);

        System.out.println("Antal hyresgäster: " + marina.nbrOfTenants());
        System.out.println("Hamn: " + findTenant("h4").getMarinaName());
        for(Mooring tmpMooring : marina.getAllMooringsByType("Medium")) {
            System.out.println("Nbr: " + tmpMooring.getNbr()) + " Hyra: " + tmpMooring.getRent());
        }
    }
 }
 ```