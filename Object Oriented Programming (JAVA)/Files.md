# JAVA NOTES: AΡΧΕΙΑ
## ΠΕΡΙΕΧΟΜΕΝΑ
- [Αρχεία Κειμένου](#αρχεία-κειμένου)
    1. [Εγγραφή σε Αρχείο](#1-εγγραφή-σε-αρχεία)
        - [ΟΔΗΓΙΕΣ](#οδηγιες-ακ-εγγραφη)
        - [ΚΩΔΙΚΑΣ](#τελικος-κωδικας-ακ-εγγραφη)
    2. [Διάβασμα από Αρχείο](#2-διάβασμα-απο-αρχεία)
        - [ΟΔΗΓΙΕΣ](#οδηγιες-ακ-αναγνωση)
        - [ΚΩΔΙΚΑΣ](#τελικος-κωδικας-ακ-αναγνωση)
- [Διαδικά Αρχεία](#διαδικά-αρχεία)
    1. [Εγγραφή σε Αρχείο](#1-εγγραφή-σε-διαδικά-αρχεία)
        - [ΟΔΗΓΙΕΣ](#οδηγιες-δα-εγγραφη)
        - [ΚΩΔΙΚΑΣ](#τελικος-κωδικας-δα-εγγραφη)
    2. [Διάβασμα από Αρχείο](#1-ανάγνωση-από-διαδικά-αρχεία)
        - [ΟΔΗΓΙΕΣ](#οδηγιες-δα-αναγνωση)
        - [ΚΩΔΙΚΑΣ](#τελικος-κωδικας-δα-αναγνωση)


# Αρχεία Κειμένου
### 1. Εγγραφή σε Αρχεία
Η αποθήκευση δεδομένων σε αρχείο γίνεται σε τρία βήματα:
1. Άνοιγμα του αρχείου
2. Εγγραφή των δεδομένων
3. Κλείσιμο του αρχείου

**Οποιοδήποτε από αυτά τα βήματα μπορεί να παράγει εξαιρέσεις! Για αυτό τα τοποθετούμε σε ένα ```try/catch``` block.**

## ΟΔΗΓΙΕΣ (Α.Κ. ΕΓΓΡΑΦΗ)
#### Βήμα 1o: άνοιγμα αρχείου
Δημιουργούμε ένα αντικείμενο FileWriter, που ο κατασκευαστής δέχεται το όνομα του αρχείου.
```java
FileWriter writer = new FileWriter("…όνομα αρχείου…");
```
Αν το αρχείο **δεν υπάρχει** ήδη, ***δημιουργείται***. <br><br>
Αν **το αρχείο υπάρχει** και ***θέλουμε να γίνει εγγραφή μετά από όσα υπάρχουν ήδη στο αρχείο***, τότε χρησιμοποιούμε τον παρακάτω κατασκευαστή:
```java
// ΓΙΑ ΝΑ ΠΡΟΣΘΕΣΟΥΜΕ ΕΓΓΡΑΦΕΣ ΣΤΟ ΑΡΧΕΙΟ
// ΒΑΖΟΥΜΕ ΤΟ 2ο ΟΡΙΣΜΑ (append) true
public FileWriter(String filename, boolean append)
```
Το όνομα του αρχείου μπορεί να έχει τη μορφή αλφαριθμητικού ή
ενός αντικειμένου File:
```java
File f = new File("…όνομα αρχείου…");
```

#### Βήμα 2o: άνοιγμα αρχείου
Όταν ένα αρχείο ανοίξει επιτυχώς, τότε μπορεί να χρησιμοποιηθεί η μέθοδος ```write``` του εγγραφέα για την αποθήκευση χαρακτήρων — συχνά με μορφή αλφαριθμητικών — στο αρχείο:
```java
writer.write("…τμήμα κειμένου…");
```

### Βήμα 3o: κλείσιμο αρχείου
Όταν τελειώσει η εγγραφή της εξόδου, **πρέπει** να κλείσουμε
κανονικά το αρχείο:
```java
writer.close();
```
Αυτό **εξασφαλίζει ότι όλα τα δεδομένα έχουν πράγματι γραφεί** στο
εξωτερικό σύστημα αρχείων, και έχει συχνά ως αποτέλεσμα την
αποδέσμευση κάποιων εσωτερικών ή εξωτερικών πόρων.

## ΤΕΛΙΚΟΣ ΚΩΔΙΚΑΣ (Α.Κ. ΕΓΓΡΑΦΗ)
```java
// Η Λίστα RoomsList περιέχει Strings
// Ο παρακάτω κώδικας φτιάχνει ένα αρχείο με τα περιεχόμενα της
// λίστας RoomList (1 σε κάθε γραμμή)
try {
    // Ανοιγμα Αρχείου
    File myFile = new File("filename.txt");
    FileWriter writer = new FileWriter(myFile);
    // Εγγραφή στο αρχείο
    for(String text: RoomList) {
        writer.write(text);
        writer.write(System.lineSeparator()); //to change line
    }
    // Κλεισιμο αρχείου
    writer.close();
} 
catch(IOException e) {
    e.printStackTrace();
    // H κάτι άλλο
}
```

### 2. Διάβασμα απο  Αρχεία
## ΟΔΗΓΙΕΣ (Α.Κ. ΑΝΑΓΝΩΣΗ)
Για το διάβασμα απο ένα αρχείο κειμένου ακολουθούμε την εξής διαδικασία:
1. Κατασκευάζουμε ένα αντικείμενο ```File```
    ```java
    File myFile = new File("names.txt");
    ```
2. Κατασκευάζουμε ένα αντικείμενο `FileReader` με το `File` που κατασκευάσαμε πριν ώς όρισμα.
    ```java
    FileReader fileReader = new FileReader(myFile);
    ```
3. Κατασκευάζουμε ένα αντικείμενο `BufferedReader` και περικλίουμε το αντικείμενο `FileReader`
    ```java
    BufferedReader reader = new BufferedReader(fileReader);
    ```
4. Εκτελούμε τις ενέργειες που θέλουμε
    ```java
	String fileLine = reader.readLine();    // Read 1st Line
	while(fileLine != null) {	// fileLine == null means the file ended
		// Κάποια Ενέργεια π.χ. :
		System.out.println(fileLine);
		// ΝΕΑ ΓΡΑΜΜΗ
		fileLine = reader.readLine();
	}
    ```
5. **ΚΛΕΙΝΟΥΜΕ ΤΟ ΑΡΧΕΙΟ**
```java
reader.close();
```

### ΤΕΛΙΚΟΣ ΚΩΔΙΚΑΣ (Α.Κ. ΑΝΑΓΝΩΣΗ)
```java
// READ FROM FILEs
try {
	// Create File & Readers
	File myFile = new File("names.txt");
	FileReader fileReader = new FileReader(myFile);
	BufferedReader reader = new BufferedReader(fileReader);
	
	// Parse each lines file
	String fileLine = reader.readLine();
	while(fileLine != null) {	// fileLine == null means the file ended
		// Κάποια Ενέργεια π.χ. :
		System.out.println(fileLine);
		// ΝΕΑ ΓΡΑΜΜΗ
		fileLine = reader.readLine();
	}
    // Close The File
	reader.close();
	
} 
catch (FileNotFoundException e) {
	e.printStackTrace();
} 
catch (IOException e) {
	e.printStackTrace();
}
```

# Διαδικά Αρχεία
### 1. Εγγραφή σε Διαδικά  Αρχεία
## ΟΔΗΓΙΕΣ (Δ.Α ΕΓΓΡΑΦΗ)
**Για να μπορέσουμε να αποθηκεύσουμε ένα αντικείμενο σε _διαδικό αρχείο_ η Κλάση του αντικείμένου αυτού *ΠΡΕΠΕΙ ΝΑ ΥΛΟΠΟΙΕΙ ΤΗΝ ΔΙΑΣΥΝΔΕΣΗ `Serializable`***
1. Κατασκευάζουμε ένα αντικείμενο `File`
    ```java
    File myFile = new File("names.txt");
    ```
2. Κατασκευάζουμε ένα αντικείμενο `FileOutputStream` με όρισμα το αντικείμενο `File` που φτιάξαμε.
3. Κατασκευάζουμε ένα αντικέιμενο `ObjectOutputStream` με όρισμα το αντικέιμενο `FileOutputStream`
4. Αποθηκεύουμε τα αντικείμενα που θέλουμε
    ```java
    objectOutStream.writeObject(anObject);
    ```
5. ΚΛΕΙΝΟΥΜΕ **ΚΑΙ ΤΑ ΔΥΟ** ΑΝΤΙΚΕΙΜΕΝΑ `OutputStream`
    ```java
    fileOutStream.close();
    objectOutStream.close();
    ```

Η ΚΛΑΣΗ ΤΟΥ ΑΝΤΙΚΕΙΜΕΝΟΥ ΠΡΕΠΕΙ ΝΑ ΕΧΕΙ ΔΗΛΩΘΕΙ ΕΤΣΙ:
```java
public class MyClassName implements Serializable {
    // Properties
    .
    .
    // Methods
}
```

## ΤΕΛΙΚΟΣ ΚΩΔΙΚΑΣ (Δ.Α. ΕΓΓΡΑΦΗ)
```java
try {
		// 1. Create File
		File file = new File("employees.arch");
		
		// 2. Create FileOutputStream
		FileOutputStream fileOutStream = new FileOutputStream(file);
		
		// 3. Create ObjectOutputStream
		ObjectOutputStream objectStream = new ObjectOutputStream(fileOutStream);
		
		// 4. Write an Object to the file
		objectStream.writeObject(anObject);
		
		// 5. Close File
		fileOutStream.close();
		objectStream.close();
		
		System.out.println("OK");
	} catch (FileNotFoundException exc) {
		exc.printStackTrace();
	} catch (IOException exc) {
		exc.printStackTrace();
	}
```

### 1. Ανάγνωση από Διαδικά Αρχεία
## ΟΔΗΓΙΕΣ (Δ.Α ΑΝΑΓΝΩΣΗ)
1. Κατασκευάζουμε ένα αντικείμενο `File` με όρισμα το αρχείο που θέλουμε να διαβάσουμε
    ```java
    File myFile = new File("names.txt");
    ```
2. Κατασκευάζουμε ένα αντικείμενο `FileInputStream` με όρισμα το αντικείμενο `File` που φτιάξαμε.
3. Κατασκευάζουμε ένα αντικέιμενο `ObjectInputStream` με όρισμα το αντικέιμενο `FileInputStream`
4. Διαβάζουμε από το αρχείο με την μέθοδο `readObject` 
    ```java
    MyClass myObject = (MyClass) objectInStream.readObject();
    ```
    Επειδή η μέθοδος `readObject` _επιστρέφει αντικείμενα τύπου `Object`_ **ΠΡΕΠΕΙ ΝΑ ΓΙΝΕΙ ΡΗΤΗ ΜΕΤΑΤΡΟΠΗ ΤΥΠΟΥ** (μεσω `(MyClass) objectInStream.readObject()`)

### ΤΕΛΙΚΟΣ ΚΩΔΙΚΑΣ (Δ.Α ΑΝΑΓΝΩΣΗ)
```java
try {
	// 1. Create File
	File file = new File("employees.arch");
	
	// 2. Create FileInputStream
	FileInputStream fileInStream = new FileInputStream(file);
	
	// 3. Create ObjectInputStream
	ObjectInputStream objectInStream = new ObjectInputStream(fileInStream);
	
	// 4. Get the object(s) from the file
	// Η μέθοδος readObject() επιστρέφει αντικείμενα
	// της υπερκλάσσης Object άρα κάνουμε ριτή μετατροπή
	// τύπου -->  (MyClass) objectInStream.readObject();
	e = (Employee) objectInStream.readObject();
	
	System.out.println("OK");
	System.out.println(e.getName());
}
catch (IOException exc) {
	exc.printStackTrace();
} 
catch (ClassNotFoundException e1) {
	// TODO Auto-generated catch block
	e1.printStackTrace();
}
```

