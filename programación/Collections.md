- **Què és una col·lecció?**
    - És una agrupació d’elements (objectes) en la qual s’hi han de poder executar diverses accions: afegir, recórrer, cercar, extreure…
- **Què és el framework de col·leccions de Java?**
    - És una arquitectura unificada per representar i gestionar col·leccions, independent dels detalls de la implementació.
- **Per quines 3 tipologies de components està format el framework de col·leccions de Java?**
    - 1a tipologia: Interfícies.
    - 2a tipologia: Implementacions.
    - 3a tipologia: Algorismes.
- **Què són les interfícies de Java?**
    - Tipus abstractes de dades (TAD) que defineixen la funcionalitat de les col·leccions i funcionalitats de suport.
- **Què són les implementacions de Java?**
    - Classes que implementen les interfícies de les col·leccions, de manera que una interfície pot tenir més d’una implementació (classe que la implementi).
- **Què són els Algorismes de Java?**
    - Mètodes que efectuen càlculs (cerques, ordenacions…) en els objectes de les implementacions.

* * *

## 1.2.1. Classes genèriques

- **A quin tipus de classes especials pertanyen les Col·leccions que proporciona Java?**
    - Pertanyen a les classes genèriques.
- **Què són les classes genèriques?**
    - Són classes que encapsulen dades i mètodes basats en tipus de dades genèrics i serveixen de plantilla per generar classes a partir de concretar els tipus de dades genèrics.
- **Quan es dóna la utilització més habitual de les classes genèriques?**
    - En el disseny de classes pensades per a la gestió de conjunts de dades (llistes, piles, cues, arbres...) en els quals, si no existís aquest concepte, hauríem de dissenyar tantes classes com diferents tipus de dades s'haguessin de gestionar.
- **Exemples de classes genèriques:**

```java
class llistaInteger.../* Gestió de llista d'objectes Integer
class llistaPersona.../* Gestió de llista d'objectes Persona
class llistaDate.../* Gestió de llista d'objectes Date
```

- **Què caldria fer si no disposèssim de les classes genèriques i volguessim fer tres llistes que emmagatzemen dades diferents ?**
    - Hauríem d'implementar tres llistes diferents amb la repetició de codi idèntic, ja que els mètodes que implementarien les tres llistes serien idèntics, com per exemple afegitPerInici, afegirPelFinal, recorregut, extreurePrimerElement, etc.
- **Quina és la sintaxi per definir una classe genèrica en Java?**

```java
//T1, T2... fan referència als tipus de dades genèrics gestionats
//pels mètodes de la classe genèrica
    [public] [final|abstract] class NomClasse <T1, T2...>
    {
    ...                        
    }
```

- **On s'han d'explicitar els tipus de dades genèrics gestionats pels mètodes de la classe genèrica?**
    - En la declaració de les referències a la classe genèrica
        - NomClasse obj&lt;nomTipusConcret1, nomTipusConcret2...&gt;;
    - En la creació dels objectes de la classe genèrica:
        - obj = new NomClasse&lt;nomTipusConcret1, nomTipusConcret2...&gt;(...);
- **Exemple de classe genèrica amb diversos tipus parametritzats:**

```java
import java.util.Date;
    import java.awt.Color;
     
    public class ExempleClasseGenerica <T1, T2> {
       private T1 x1;
       private T2 x2;
     
       public ExempleClasseGenerica (T1 p1, T2 p2) {
          x1=p1;
          x2=p2;
       }
     
       public String toString() {
          return x1.toString()+" - " +x2.toString();
       }
     
       public T1 getX1() { return x1; }
     
       public T2 getX2() { return x2; }
     
       public static void main (String args[]) {
          ExempleClasseGenerica <Integer, Float> obj1 = 
             new ExempleClasseGenerica <Integer,Float> (new Integer(20), new Float(42.45));
          ExempleClasseGenerica <Double, Double> obj2 = 
             new ExempleClasseGenerica <Double,Double> (new Double(4.32), new Double(7.45));
//obj3 s'hauria d'haver creat així:
//ExempleClasseGenerica <Integer, Date> obj3 = new ExempleClasseGenerica <Integer, Date> new Integer(22), new Date());
          ExempleClasseGenerica obj3 = new ExempleClasseGenerica (new Integer(22), new Date());
          ExempleClasseGenerica obj4 = new ExempleClasseGenerica (50, 'a');
          System.out.println(obj1.toString());
          System.out.println(obj2.toString());
          System.out.println(obj3.toString());
          System.out.println(obj4.toString());
       }
    }
```

- **Mirant l'exemple anterior, sobre obj3, com podem conèixer el dia del mes de la data corresponent?**
    - Al crear l'obj3 no s'ha especificat el tipus Date, per tant haurem de dir-li al compilador que l'objecte retornat és de tipus Date:
        - System.out.println((Date)obj3.getX2().getDate());
- **Quan van aparèixer els tipus genèrics?**
    - Amb Java5.
- **Quins problemes provocava usar la classe Object en comptes dels tipus genèrics?**
    - En dissenyar estructures contenidores d’objectes (piles, cues, llistes, arbres…) no hi havia una manera senzilla de delimitar els tipus dels objectes a inserir i, si no s’anava amb compte, en una mateixa estructura contenidora hi podia haver objectes dispars.
    - Sovint calia fer conversions *cast* de la classe Object a la classe corresponent, amb perill d’equivocacions per part del programador que no es detecten fins a l’execució del programa, com s’ha comprovat al final del darrer exemple.
- **Quina sintaxi utilitzem per implementar mètodes que admetin per paràmetres objectes de classes genèriques¿**

```java
    <modificadorAccés> [final|abstract] nomMètode ( NomClasse<?,?...> [,...])
    {...}
```

- **Exemple de classe dissenyada amb tipus genèrics:**

```java
    import java.util.Date;
     
    public class MetodeAmbClasseGenerica {
       public static void metode (ExempleClasseGenerica<?,?> obj) {
          System.out.println(obj);
       }
     
       public static void main (String args[]) {
          ExempleClasseGenerica <Integer, Float> obj1 = 
             new ExempleClasseGenerica <Integer,Float> (new Integer(20), new Float(42.45));
          ExempleClasseGenerica <Double, Date> obj2 = 
             new ExempleClasseGenerica <Double,Date> (new Double(4.32), new Date());
          metode(obj1);
          metode(obj2);
       }
    }
```

- **Com podem restringir els tipus específics amb els que es creïn els objectes d'una classe genèrica? tipus genèric restringit**
    - En instanciar la classe genèrica s'ha de proporcionar una classe que sigui subclasse d'una classe X, la sintaxi seria:

```java
    [public] [final|abstract] NomClasse <T1 extends X, T2 extends Y...> {
    ...
    }
```

- **Exemple de classe genèrica amb un tipus genèric restringit i amb mètodes que reben, per paràmetre, objectes de la classe genèrica:**
    - Es tracta del disseny d’una classe que gestiona taules de valors numèrics i proporciona mètodes per calcular la mitjana dels valors emmagatzemats en la taula, la dimensió de les taules i per comparar les mitjanes i les dimensions de dues taules de valors numèrics.
    - La taula ha de ser genèrica perquè pugui gestionar els diversos tipus de valors numèrics possibles (`Integer`, `Double`, `Float`…), i la volem restringir perquè les taules només siguin de valors numèrics.
    - Els mètodes de comparació necessiten rebre, com a paràmetre, un objecte de classe genèrica.

```java
    public class TaulaValorsNumerics <T extends Number> {
      private T t[];
     
      public TaulaValorsNumerics (T[] obj) { t = obj; }
     
      public double mitja () {
       double suma=0;
       int valorsNoNuls=0;
       for (int i=0; i<t.length; i++) 
        if (t[i]!=null) 
        {suma = suma + t[i].doubleValue();
         valorsNoNuls++;
        }
     
       if (valorsNoNuls==0) return 0;
       else return suma / valorsNoNuls;
      }
     
      public int dimensio () { return t.length; }
     
      public boolean mateixaMitja (TaulaValorsNumerics <?> obj) {
        return mitja() == obj.mitja();
      }
     
      public boolean mateixaDimensio (TaulaValorsNumerics <?> obj) {
       return dimensio() == obj.dimensio();
      }
     
      public String toString() {
       String s="{";
       for (int i=0; i<t.length; i++)
        if (s.equals("{")) s = s + t[i];
        else s = s + ", " + t[i];
       s = s + "}";
       return s;
      }
     
      public static void main (String args[]) {
       Integer ti[] = {1, 2, null, 3, 4, null, 5};
       Double td[] = {1.1, 2.2, 3.3, null, 4.4, 5.5, 6.6};
       String ts[] = { "Cad1", "Cad2" };
       TaulaValorsNumerics<Integer> tvn1= new TaulaValorsNumerics<Integer> (ti);
       TaulaValorsNumerics<Double> tvn2= new TaulaValorsNumerics<Double> (td);
     
    // Les següents instruccions comentades no són compilables, per ser tipus genèric T restringit
    // TaulaValorsNumerics tvn3 = new TaulaValorsNumerics (ts);
    // TaulaValorsNumerics<String> tvn3 = new TaulaValorsNumerics<String> (ts);          
     
       System.out.println("tvn1: "+tvn1);
       System.out.println("Mitja: "+tvn1.mitja());
       System.out.println("Dimensió: "+tvn1.dimensio());
       System.out.println("tvn2: "+tvn2);
       System.out.println("Mitja: "+tvn2.mitja());
       System.out.println("Dimensió: "+tvn2.dimensio());
       System.out.println("tvn1 i tvn2 tenen la mateixa mitja?" + tvn1.mateixaMitja(tvn2));
       System.out.println("tvn1 i tvn2 tenen la mateixa dimensió?" + tvn1.mateixaDimensio(tvn2));
      }
    }
```

* * *

## 1.2.2. Interfícies

- **Què són les interfícies?**
    - Són tipus abstractes de dades (TAD) que defineixen la funcionalitat de les col·leccions i funcionalitats de suport.
- **Quins 2 tipus d'interficies cal distingir en el framework de col·leccions?**
    - 1r tipus: Interfícies que constitueixen el cor del *framework* i defineixen els diferents tipus de col·leccions:
        - `Collection`, `Set`, `List`, `Queue`, `SortedSet`, `Map` i `SortedMap`, conegudes normalment com *interfícies del JCF*.
    - 2n tipus: Interfícies de suport:
        - `Iterator`, `ListIterator`, `Comparable` i `Comparator`.
- **Per quines 2 jerarquies estan organitzades les Interfícies que constitueixen el cor del framework?**
    - 1a jerarquia: Agrupa les col·leccions amb accés per posició (seqüencial i directe) i que té la interfície Collection per arrel.
    - 2a jerarquia: Defineix les col·leccions amb accés per clau i que té la interfície Map per arrel.
- **Interfícies del framework de col·leccions de Java amb la jerarquia que hi ha entre elles:**

![754613513e91874bb412fd6409ee9598.png](../_resources/754613513e91874bb412fd6409ee9598.png)

- **Quina és la interfície Collection&lt;E&gt;?**
    - És la interfície pare de la jerarquia de col·leccions amb accés per posició (seqüencial i directe).
- **Quins 3 tipus de col·leccions comprèn la interfície Collection&lt;E&gt;?**
    - 1a col·lecció:
        - Col·leccions que permeten elements duplicats i col·leccions que no els permeten.
    - 2a col·lecció:
        - Col·leccions ordenades i col·leccions desordenades.
    - 3a col·lecció:
        - Col·leccions que permeten el valor `null` i col·leccions que no el permeten.
- **Quina és la definició de la interfície Collection&lt;E&gt;?**

```java
    public interface Collection<E> extends Iterable<E> {
    // Basic operations
    int size();
    boolean isEmpty();
    boolean contains(Object element);
    boolean add(E element);//optional
    boolean remove(Object element);//optional
    Iterator<E> iterator();
     
    // Bulk operations
    boolean containsAll(Collection<?> c);
    boolean addAll(Collection<? extends E> c);//optional
    boolean removeAll(Collection<?> c);//optional
    boolean retainAll(Collection<?> c);//optional
    void clear(); //optional
     
    // Array operations
    Object[] toArray();
    <T> T[] toArray(T[] a);
    }
```

- **Què vol dir el comentari optional acompanyant els mètodes de la definició anterior?**
    - Indica que el mètode pot no estar disponible en alguna de les implementacions de la interfície.
    - Això pot passar si un mètode de la interfície no té sentit en una implementació concreta.
    - La implementació ha de definir el mètode, però en ser cridat provoca una excepció *UnsupportedOperationException*.
- **Per què Java no proporciona cap classe que implementi directament la interfície Collection&lt;E&gt;?**
    - Perquè implementa interfícies derivades d'aquesta.
- **Quin mètode podem fer servir per recòrrer els elements d'una col·lecció?**
    - El mètode iterator().
- **Què retorna el mètode iterator()?**
    - Una referència a la interfície Iterator.

### INTERFÍCIES "ITERATOR" I "LISTITERATOR"

- **Què permeten les interfícies de suport Iterator i ListIterator utilitzades per diversos mètodes de les classes que implementen la interfície Collection o les seves subinterfícies?**
    - Permeten recórrer els elements d'una col·lecció.
- **Quina és la definició de la interfície Iterator?**

```java
    public interface Iterator<E>{
      boolean hasNext();
      E next();
      void remove();// optional
    }
```

- **Què permet la referència que retorna el mètode iterator() de la interfície Collection?**
    - Recórrer la col·lecció amb els mètodes next() i hastNext().
    - Eliminar l'element actual amb el mètode remove() sempre que la col·lecció permeti l'eliminació dels seus elements.
- ** Què permet la interfície ListIterator?**
    - Recórrer els objectes que implementen la interfície `List` (subinterfície de `Collection`) en ambdues direccions (endavant i endarrere) i efectuar algunes modificacions mentre s’efectua el recorregut.
- **Quins mètodes defineix la interfície ListIterator?**

```java
    public interface ListIterator<E> extends Iterator<E>{
      boolean hasNext();
      E next();
      boolean hasPrevious();
      E previous();
      int nextIndex();
      int previousIndex();
      void remove();
      void set(E e);
      void add(E e);
    }
```

- **Quins mètodes permeten el recorregut pels elements de la col·lecció (llista)?**
    - next()
    - previous()
- **En una llista amb n elements, com es numeren els elements?**
    - de 0 a n-1
- **Quins valors vàlids té l'índex iterador?**
    - de 0 a n
- **Què retorna el mètode previousIndex()?**
    - x-1
- **Què retorna el mètode nextIndex()?**
    - x
- **Si l'índex és 0, què retorna previousIndex()?**
    - -1
- **Si l'índex és n, què retorna nextIndex()?**
    - el resultat del mètode size()

### INTERFÍCIES COMPARABLE I COMPARATOR

- **Per a què estan orientades les interfícies de suport Comparable i Comparator?**
    - Estan orientades a mantenir una relació d'ordre en les classes del framework de col·leccions que implementen interfícies que faciliten ordenació (List, SortedSet i SortedMap).
- **De quin únic mètode consta la interfície Comparable?**

```java
    public interface Comparable<T> {
      int compareTo(T o);
    }
```

- **Què fa el mètode compareTo() de la interfície Comparable?**
    
    - Compara l’objecte sobre el qual s’aplica el mètode amb l’objecte rebut per paràmetre i retorna un enter negatiu, zero o positiu en funció de si l’objecte sobre el qual s’aplica el mètode és menor, igual o major que l’objecte rebut per paràmetre.
- **Què succeeix si les dos objectes usats al mètode compareTo() de la interfície Comparable no són comparables?**
    
    - El mètode genera una excepció de tipus ClassCastException.
- **Quines classes del llenguatge Java implementen la interfície Comparable?**
    
    - Moltes, per exemple: `String, Character, Date, Byte, Short, Integer,Long, Float, Double, BigDecimal, BigInteger…`.
    - Per tant totes aquestes classes proporcionen una implementació del mètode compareTo().
- **Amb què hauria de ser compatible tota implementació del mètode compareTo()?**
    
    - Amb el mètode equals().
- **Què ha de retornar el mètode compareTo() si el mètode equals() retorna true?**
    
- **Què tenen les classes que implementen la interfície Comparable?**
    
    - Es diu que tenen un ordre natural.
- **Amb quins mètodes es poden ordenar les col·leccions de classes que implementen la interfície Comparable?**
    
    - static Collections.sort()
    - Arrays.sort()

### EXEMPLE IMPLEMENTS COMPARABLE

- **Exemple programa per comparar dni de persones y per ordenar larray d'objectes persona:**

```java
public class Persona implements Comparable {

    private String dni;
    private String nom;
    private int edat;

    public Persona(){

    };

    public String getDni() {
        return dni;
    }

    public void setDni(String dni) {
        this.dni = dni;
    }

    public Persona(String dni, String nom, int edat) {
        this.dni = dni;
        this.nom = nom;
        this.edat = edat;
    }

    @Override
    public final int compareTo(Object personaParametre) {
        if (personaParametre instanceof Persona) {
            String dniPersonaParametre = ((Persona) personaParametre).dni;

            int resultatCompareTo = dni.compareTo(dniPersonaParametre);

            return resultatCompareTo;
        }
        throw new ClassCastException();  // Instrucció que genera una excepció
    }
}
```

```java
public class Alumne extends Persona {

    private char cicle;

    public Alumne(String dni, String nom, int edat, char cicle) {
        super(dni, nom, edat);
        this.cicle = cicle;
    }
}
```

```java
import java.util.Arrays;

public class ProvaPersona {

    public static void main(String args[]) {
        Persona arrayPersones[] = new Persona[6];
        arrayPersones[0] = new Alumne("99999999","Anna",20, '?');
        arrayPersones[1] = new Alumne("00000000","Pep",33,'m');
        arrayPersones[2] = new Alumne("22222222","Maria",40,'s');
        arrayPersones[3] = new Alumne("66666666","Àngel",22, '?');
        arrayPersones[4] = new Alumne("22222222","Joanna",25,'M');
        arrayPersones[5] = new Alumne("55555555","Teresa",30,'S');


        //Exemple compareTo() Comparable false
        //Si l'objecte sobre el qual s'aplica el mètode és menor
        //a l'objecte passat per paràmetre, aleshores -1

        //Si l'objecte sobre el qual s'aplica el mètode és igual
        //a l'objecte passat per paràmetre, aleshores 0

        //Si l'objecte sobre el qual s'aplica el mètode és major
        //a l'objecte passat per paràmetre, aleshores +1

        //Exemple1: dni de l'objecte sobre el qual s'aplica el mètode 99999999
        //dni de l'objecte passat per paràmetre: 00000000
        int resultatComparacioDnis = arrayPersones[0].compareTo(arrayPersones[1]);
        System.out.println("1r cas: dni " + arrayPersones[0].getDni() + " compareTo() dni " + arrayPersones[1].getDni());
        System.out.println("1r cas :" + resultatComparacioDnis);

        //Exemple2: dnis iguals
        resultatComparacioDnis = arrayPersones[2].compareTo(arrayPersones[4]);
        System.out.println("2n cas: dni " + arrayPersones[2].getDni() + " compareTo() dni " + arrayPersones[4].getDni());
        System.out.println("Iguals :" + resultatComparacioDnis);

        //Exemple3: dni de l'objecte sobre el qual s'aplica el mètode 00000000
        //dni de l'objecte passat per paràmetre: 99999999
        resultatComparacioDnis = arrayPersones[1].compareTo(arrayPersones[0]);
        System.out.println("3r cas: dni " + arrayPersones[1].getDni() + " compareTo() dni " + arrayPersones[0].getDni());
        System.out.println("3r cas :" + resultatComparacioDnis);




        //Exemple ordenació Comparable
        System.out.println("Contingut inicial de la taula:");
        for (int i=0; i<arrayPersones.length; i++) {
            System.out.println("   "+arrayPersones[i]);
        }
        Arrays.sort(arrayPersones);

        System.out.println("Contingut de la taula després d'haver estat ordenada:");
        for (int i=0; i<arrayPersones.length; i++) {
            System.out.println("Después de ordenar: "+arrayPersones[i]);
        }
    }
}
```

```java
//RESPOSTA 
1r cas: dni 99999999 compareTo() dni 00000000
1r cas :9
2n cas: dni 22222222 compareTo() dni 22222222
Iguals :0
3r cas: dni 00000000 compareTo() dni 99999999
3r cas :-9
Contingut inicial de la taula:
   Alumne@4cb2c100
   Alumne@6fb554cc
   Alumne@614c5515
   Alumne@77b52d12
   Alumne@2d554825
   Alumne@68837a77
Contingut de la taula després d'haver estat ordenada:
Después de ordenar: Alumne@6fb554cc
Después de ordenar: Alumne@614c5515
Después de ordenar: Alumne@2d554825
Después de ordenar: Alumne@68837a77
Después de ordenar: Alumne@77b52d12
Después de ordenar: Alumne@4cb2c100
```

### EXEMPLE IMPLEMENTS COMPARATOR

- **Què permet la interfície Comparator?**
    - Permet ordenar conjunts d'objectes que pertanyen a classes diferents.
- **Com podem establir l'ordre per poder ordenar objectes de classes diferents?**
    - El programador ha de subministrar un objecte d'una classe que implementi la interfície Comparator:

```java
    public interface Comparator<T> {
      int compare(T o1, T o2);
      boolean equals(Object obj);
    }
```

- **Quin és l'objectiu del mètode equals() que es troba dins la interface Comparator&lt;T&gt;?**
    - Poder comparar objectes Comparator.
- **Quin és l'objectiu del mètode compare() que es troba dins la interface Comparator&lt;T&gt;?**
    - Poder comparar 2 objectes de diferents classes i obtenir:
        - enter negatiu: si l'objecte rebut per primer paràmetre és menor a l'objecte rebut per segon paràmetre.
        - zero: si l'objecte rebut per primer paràmetre és igual a l'objecte rebut per segon paràmetre.
        - enter positiu: si l'objecte rebut per primer paràmetre és major a l'objecte rebut per segon paràmetre.
- **Exemple: programa per ordenar una taula deixant en primer lloc els elements Date, seguits dels elements Double, després els elements Persona i finalment els elements Short. També volem que entre el grup d'elements d'un mateix tipus (per exemple entre el grup d'elements de tipus Date) actui l'ordre natural definit en aquest tipus (definit per la implementació del mètode compareTo() de la interfície Comparable -> les dates menors han de quedar abans que les majors):**

```java
public class Persona implements Comparable{
    private String dni;
    private String nom;
    private int edat;

    public Persona(){

    };

    public String getDni() {
        return dni;
    }

    public void setDni(String dni) {
        this.dni = dni;
    }

    public Persona(String dni, String nom, int edat) {
        this.dni = dni;
        this.nom = nom;
        this.edat = edat;
    }

    @Override
    public final int compareTo(Object personaParametre) {
        if (personaParametre instanceof Persona) {
            String dniPersonaParametre = ((Persona) personaParametre).dni;

            int resultatCompareTo = dni.compareTo(dniPersonaParametre);

            return resultatCompareTo;
        }
        throw new ClassCastException();  // Instrucció que genera una excepció
    }
}
```

```java
public class Alumne extends Persona {

    private char cicle;

    public Alumne(String dni, String nom, int edat, char cicle) {
        super(dni, nom, edat);
        this.cicle = cicle;
    }
}
```

```java
import java.util.Comparator;
import java.util.Date;

public class MyComparator implements Comparator<Object> {

    //El mètode compare() ens permet comparar objectes de diferents classes i obtenir:
    //enter negatiu: si l'objecte rebut per primer paràmetre és menor a l'objecte rebut per segon paràmetre.
    //zero: si l'objecte rebut per primer paràmetre és igual a l'objecte rebut per segon paràmetre.
    //enter positiu: si l'objecte rebut per primer paràmetre és major a l'objecte rebut per segon paràmetre.
    public int compare (Object o1, Object o2) {
        if (o1 instanceof Date) {
            if (o2 instanceof Date) {
                return ((Date)o1).compareTo((Date)o2);
            } else {
                return -1;
            }
        } else if (o1 instanceof Double) {
            if (o2 instanceof Date) {
                return 1;
            } else if (o2 instanceof Double) {
                return ((Double)o1).compareTo((Double)o2);
            } else {
                return -1;
            }
        } else if (o1 instanceof Persona) {
            if (o2 instanceof Date || o2 instanceof Double) {
                return 1;
            } else if (o2 instanceof Persona) {
                return ((Persona)o1).compareTo((Persona)o2);
            } else {
                return -1;
            }
        } else if (o1 instanceof Short) {
            if (o2 instanceof Short) {
                return ((Short)o1).compareTo((Short)o2);
            } else {
                return 1;
            }
        } else {
            throw new ClassCastException();  // Instrucció que genera una excepció
        }
    }
}
```

```java
java.util.Arrays;
import java.util.Date;

public class ProvaComparator {

    public static void main (String args[]) {

        Object arrayObjectes[] = new Object[6];
        arrayObjectes[0] = new Alumne("99999999","Anna",20, '?');
        arrayObjectes[1] = new Date();
        arrayObjectes[2] = new Alumne("22222222","Maria",40,'s');
        arrayObjectes[3] = new Double(33.33);
        arrayObjectes[4] = new Short((short)22);
        arrayObjectes[5] = new Date(109,0,1);

        System.out.println("Contingut inicial de la taula:");
        for (int i = 0; i < arrayObjectes.length; i++)
            System.out.println("   " + arrayObjectes[i].getClass().getName()
                    + " - " + arrayObjectes[i]);

        Arrays.sort(arrayObjectes , new MyComparator());

        System.out.println("Contingut de la taula després d'haver estat ordenada:");
        for (int i=0; i < arrayObjectes.length; i++)
            System.out.println("   " + arrayObjectes[i].getClass().getName()
                    + " - " + arrayObjectes[i]);
    }
}
```

```java
//RESPOSTA
Contingut inicial de la taula:
   Alumne - Alumne@5315b42e
   java.util.Date - Mon Apr 17 11:10:16 CEST 2023
   Alumne - Alumne@5d5eef3d
   java.lang.Double - 33.33
   java.lang.Short - 22
   java.util.Date - Thu Jan 01 00:00:00 CET 2009
Contingut de la taula després d'haver estat ordenada:
   java.util.Date - Thu Jan 01 00:00:00 CET 2009
   java.util.Date - Mon Apr 17 11:10:16 CEST 2023
   java.lang.Double - 33.33
   Alumne - Alumne@5d5eef3d
   Alumne - Alumne@5315b42e
   java.lang.Short - 22
```

### INTERFÍCIES "SET" I "SORTEDSET"

- **Per a què és destinada la interfície Set&lt;E&gt;?**
    - Per a col·leccions que no mantenen cap ordre d'inserció i que no poden tenir 2 o més objectes iguals.
    - Correspon al concepte matemàtic de conjunt.
- **Quins mètodes es defineixen a la interfície Set&lt;E&gt;?**
    - Els mateixos mètodes definits a la interfície Collection&lt;E&gt;.
- **Per què necessiten les implementacions de la interfície Set&lt;E&gt; el mètode equals()?**
    - Per veure si dos objectes del tipus de la col·lecció són iguals i, per tant, no permetre'n la coexistència dins la col·lecció.
- **Quan retorna true la crida set.equals(Object obj)?**
    - si obj també és una instància que implementa la interfície Set +
    - si els dos objectes "set" i "obj" tenen el mateix nombre d'elements +
    - si tots els elements d'"obj" estan continguts en set
- **Aleshores, set.equals(Object obj) pot ser true encara que "set" i "obj" siguin de classes diferents?**
    - Sí.
- **Quines 3 operacions algebraiques permeten realitzar els mètodes de la interfície Set?**
    - Unió:
        - `s1.addAll(s2)` permet convertir s1 en la unió d’“s1” i “s2”.
    - Intersecció:
        - `s1.retainAll(s2)` permet convertir “s1” en la intersecció d’“s1” i “s2”.
    - Diferència:
        - `s1.removeAll(s2)` permet convertir “s1” en la diferència d’“s1” i “s2”.
- **Com podem saber si "s2" està contingut en s1?**
    - Amb el mètode containsAll():
        - `s1.containsAll(s2)`
- **Per què serveixen els mètodes que afegeix la interfície SortedSet derivada de Set?**
    - Per permetre gestionar conjunts ordenats.
- **Quina és la definició de la interfície SortedSet&lt;E&gt;?**

```java
    public interface SortedSet<E> extends Set<E> {
      // Range-view
      SortedSet<E> subSet(E fromElement, E toElement);
      SortedSet<E> headSet(E toElement);
      SortedSet<E> tailSet(E fromElement);
     
      // Endpoints
      E first();
      E last();
     
      // Comparator access
      Comparator<? super E> comparator();
    }
```

- **Com es defineix la relació d'ordre a aplicar sobre els elements d'un objecte col·lecció que implementi la interfície SortedSet?**
    - Es defineix en el moment de la seva construcció, indicant una referència a un objecte que implementi la interfície Comparator.
- **Què passa si no indiquem cap referència a un objecte que implementi la interfície Comparator al moment de construir un objecte que implementa la interfície SortedSet?**
    - Els elements de l'objecte creat es comparen amb l'ordre natural.
- **Què retorna el mètode comparator()?**
    - Retorna una referència a l’objecte `Comparator` que defineix l’ordre dels elements del mètode, i retorna `null` si es tracta de l’ordre natural.
- **Quins són els 3 mètodes que gestionen els elements d'un objecte SortedSet segons l'ordre establert en l'objecte?**
    - iterator()
    - toArray()
    - toString()

### INTERFÍCIE "LIST"

- **Per a quin tipus de col·leccions es destina la interfície Lisc&lt;E&gt;?**
    - Per a col·leccions que mantenen l'ordre d'inserció i que poden tenir elements repetits.

```java
    public interface List<E> extends Collection<E> {
      // Positional access
      E get(int index);
      E set(int index, E element);    //optional
      void add(int index, E element); //optional
      E remove(int index);            //optional
      boolean addAll(int index, Collection<? extends E> c); //optional
     
      // Search
      int indexOf(Object o);
      int lastIndexOf(Object o);
     
      // Iteration
      ListIterator<E> listIterator();
      ListIterator<E> listIterator(int index);
     
      // Range-view
      List<E> subList(int from, int to);
    }
```

- **Quan retorna true la crida list.equals(Object obj)?**
    - Si "obj" també és una instància que implementa la interfície List +
    - si els dos objectes tenen el mateix nombre d'elements +
    - els dos objectes contenen elements iguals i en el mateix ordre.
- **El resultat de list.equals(Object obj) pot ser true malgrat que "list" i "obj" siguin de classes diferents però implementen la interfície List?**
    - Sí.
- **Què fa el mètode add(E o) definit en la interfície Collection?**
    - Afegeix l'element "o" pel final de la llista.
- **Què fa el mètode remove(Object o) definit en la interfície Collection=**
    - Elimina la primera aparició de l'objecte indicat.

### INTERFÍCIE "QUEUE"

- Per a què es destina la interfície Queue&lt;E&gt;?
    - Per gestionar col·leccions que guarden múltiples elements abans de ser processats. Per aquest motiu, afegeix els següents mètodes als definit a la interfície Collection:

```java
    public interface Queue<E> extends Collection<E> {
      E element();
      boolean offer(E e);
      E peek();
      E poll();
      E remove();
    }
```

- **Quines 2 formes prenen els mètodes típics en la gestió de cues (encuar, desencuar i inici) en la interfície Queue, segons la reacció davant una fallada en l'operació?**
    - Mètodes que retornen una excepció.
    - Mètodes que retornen un valor especial (null o false, segons l'operació).
- **Classificació dels mètodes de gestió de cues:**

![714566fc343e4e86a1ec97060ffdaeb5.png](../_resources/714566fc343e4e86a1ec97060ffdaeb5.png)

### INTERFÍCIES "MAP" I "SORTEDMAP"

- Per a què es destina la interfície Map&lt;E&gt;?
    - Es destina a gestionar agrupacions d’elements als quals s’accedeix mitjançant una clau, la qual ha de ser única per als diferents elements de l’agrupació.
- Quina és la definició de la interfície Map&lt;E&gt;?

```java
    public interface Map<K,V> {
     
      // Basic operations
      V put(K key, V value);   //optional
      V get(Object key);
      V remove(Object key);    //optional
      boolean containsKey(Object key);
      boolean containsValue(Object value);
      int size();
      boolean isEmpty();
     
      // Bulk operations
      void putAll(Map<? extends K, ? extends V> m);  // optional
      void clear();                                  // optional
     
      // Collection Views
      public Set<K> keySet();
      public Collection<V> values();
      public Set<Map.Entry<K,V>> entrySet();
     
      // Interface for entrySet elements
      public interface Entry {
        K getKey();
        V getValue();
        V setValue(V value);
      }
    }
```

- Què retorna el mètode entrySet()?
    - Retorna una visió del `Map` com a `Set`.
    - Els elements d’aquest Set són referències a la interfície `Map.Entry` que és una interfície interna de `Map` que permet modificar i eliminar elements del `Map`, però no afegir-hi nous elements.
- Què permet el mètode get(key)?
    - Permet obtenir l’element a partir de la clau.
- Què permet el mètode keySet()?
    - Retorna una visió de les claus com a `Set`.
- Què retorna el mètode values()?
    - Retorna una visió dels elements del `Map` com a `Collection` (perquè hi pot haver elements repetits i com a `Set` això no seria factible).
- Què permet el mètode put()?
    - Permet afegir una parella clau/element.
- Què permet el mètode putAll(map)?
    - Permet afegir-hi totes les parelles d’un `Map` passat per paràmetre (les parelles amb clau nova s’afegeixen i, en les parelles amb clau ja existent en el Map, els elements nous substitueixen els elements existents).
- Què permet el mètode remove(key)?
    - Permet eliminar una parella clau/element a partir de la clau.
- Quan retorna true la crida map.equals(Object obj)?
    - Si "obj" també és una instància que implementa la interfície `Map` +
    - els dos objectes representen el mateix mapatge o, dit amb altres paraules, si l’expressió següent retorna true:
        - map.entrySet().equals(((Map) obj).entrySet())
- Per tant, pot ser el resultat de map.equals(Object obj) true encara que "map" i "obj" siguin de classes diferents però implementin a la interfície Map?
    - Sí.
- Què permet la interfície SortedMap?
    - És una interfície `Map` que permet mantenir ordenades les seves parelles en ordre ascendent segons el valor de la clau, seguint l’ordre natural o la relació d’ordre proporcionada per un objecte que implementi la interfície `Comparator` proporcionada en el moment de creació de la instància.
- Quina és la definició de la interfície SortedMap?

```java
    public interface SortedMap<K, V> extends Map<K, V> {
      // Range-view
      SortedMap<K, V> subMap(K fromKey, K toKey);
      SortedMap<K, V> headMap(K toKey);
      SortedMap<K, V> tailMap(K fromKey);
      // Endpoints
      K firstKey();
      K lastKey();
      // Comparator access
      Comparator<? super K> comparator();
    }
```