# Σημειώσεις PHP
## ΠΕΡΙΕΧΟΜΕΝΑ
1. [Φόρμες](#φόρμες)
    1. [Λήψη Δεδομένων από Φόρμα](#λήψη-δεδομένων-από-φόρμα)
    2. [Ελεγχος για Υποχρεωτικα Πεδία](#ελεγχος-για-υποχρεωτικα-πεδία)
    3. [Ελεγχος για Υποχρεωτικα Πεδία](#ελεγχος-για-υποχρεωτικα-πεδία)
    4. [Επικύρωση Στοιχείων Φόρμας](#επικύρωση-στοιχείων-φόρμας)
        - [Όνομα](#ονόμα)
        - [E-Mail](#e-mail)
        - [URL](#url)
    5. [Διατήρηση τιμών σε φόρμα μετά την υποβολή](#διατήρηση-τιμών-σε-φόρμα-μετά-την-υποβολή)
2. [Διασύνδεση με Βάσεις Δεδομένων](#mysql)
    1. [Σύνδεση σε βάση SQL](#σύνδεση-σε-βάση-sql)
    2. [Δημιουργία Βάσης](#δημιουργία-βάσης)
    3. [Δημιουργία Πίνακα](#δημιουργία-πίνακα)
    4. [Εισαγωγή Τιμών σε Πίνακα](#εισαγωγή-τιμών-σε-πίνακα)
    5. [Εμφάνιση Τιμών από Πίνακα](#εμφάνιση-τιμών-από-πίνακα)

## Φόρμες
### Λήψη Δεδομένων από Φόρμα
```php
<?php
    // Define Variables and Set them to Empty Values
    $name = "";
    
    // Valdate Input Function
    function validateInput($data){
        $data = trim($data);
        $data = stripslashes($data);
        $data = htmlspecialchars($data);
        return $data;
    }

    // Check if User Submited the form
    if($_SERVER["REQUEST_METHOD"] == "POST"){
        $name = validateInput($_POST["name"]);
    }
?>

<html>
    <head></head>
    <body>
        <form method="POST" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>">
        Name: <input type="text" name="name">
        <button type="submit">
        </form>
    </body>
</html>

<?php
    echo $name;
?>
```

### Ελεγχος για Υποχρεωτικα Πεδία
```php
$name = "";
$nameErr = "";

if($_SERVER["REQUEST_METHOD"] == "POST") {
    // check that input is not empty
    if(empty($_POST["name"])) {
        $nameErr = "Name is a required field";
    }
    else {
        $name = validateInput($_POST["name"]);
    }
}
```

### Επικύρωση Στοιχείων Φόρμας
#### Ονόμα
Ο παρακάτω κώδικας δείχνει έναν απλό τρόπο για να ελέγξετε αν το πεδίο όνομα 
περιέχει μόνο γράμματα και κενά. Εάν η τιμή του πεδίου ονόματος δεν είναι έγκυρη, 
τότε αποθηκεύστε ένα μήνυμα λάθους: 

```php
$name = test_input($_POST["name"]); 
if (!preg_match("/^[a-zA-Z ]*$/",$name)) { 
    $nameErr = "Only letters and white space allowed"; 
} 
```
#### E-mail
Στον παρακάτω κώδικα, εάν η διεύθυνση ηλεκτρονικού ταχυδρομείου δεν είναι 
καλοσχηματισμένη, τότε αποθηκεύεται ένα μήνυμα λάθους:
```php
$email = test_input($_POST["email"]); 
if (!filter_var($email, FILTER_VALIDATE_EMAIL)) { 
    $emailErr = "Invalid email format"; 
} 
```

#### URL
Ο παρακάτω κώδικας δείχνει ένα τρόπο για να ελέγξετε αν μια σύνταξη διεύθυνσης URL 
είναι έγκυρη (αυτή η κανονική έκφραση επιτρέπει επίσης παύλες στο URL). Εάν η 
σύνταξη διεύθυνσης URL δεν είναι έγκυρη, τότε να αποθηκεύσετε ένα μήνυμα λάθους:
```php
$website = test_input($_POST["website"]);
$regex = ""/\b(?:(?:https?|ftp):\/\/|www\.)[-a-z0-9+&@#\/%?=~_|!:,.;]*[-a-z0-
9+&@#\/%=~_|]/i";

if (!preg_match($regex,$website)) { 
    $websiteErr = "Invalid URL"; 
}
```

### Διατήρηση τιμών σε φόρμα μετά την υποβολή
```php
<form method="POST" action='<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>'>
    Name: 
    <input type="text" name="name" value="<?php echo $name;?>"> 

    E-mail: 
    <input type="text" name="email" value="<?php echo $email;?>">

    Website: 
    <input type="text" name="website" value="<?php echo $website;?>"> 

    Comment: 
    <textarea name="comment" rows="5" cols="40">
        <?php echo $comment;?>
    </textarea> 

    Gender: 
    <input type="radio" name="gender" <?php if (isset($gender) && $gender=="female") echo "checked";?> value="female">Female 
    <input type="radio" name="gender" <?php if (isset($gender) && $gender=="male") echo "checked";?> value="male">Male

    <button type="submit">SUBMIT</button>
</form>
```

## MySQL
### Σύνδεση σε βάση SQL
### MySQLi (OOP)
```php
<?php
    // Server Details
    $servername = "localhost";
    $username = "root";
    $password = "";

    // Create Connection to DB
    $connection = new mysqli($servername, $username, $password);

    // Check Connection to DB
    if($connection->connect_error){
        die("Connection Failed: ".$connection->connect_error);
    }
?>
```

### PDO (OOP)
```php
<?php
    // Server Details
    $servername = "localhost";
    $username = "root";
    $password = "";

    // Connect to DB
    try{
        $connection = new PDO("mysql:host;dbname=test;$username, $password");
        $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        echo "Connected"
    }
    catch (PDOException $e){
        echo "Connection failed: " . $e->getMessage();
    }
?>
```
<br><br>

### Δημιουργία Βάσης
### MySQLi (OOP)
```php
<?php
    // DB Details
    $servername = "localhost"; 
    $username = "root"; 
    $password = ""; 

    // Create Connection
    $conn = new mysqli($servername, $username, $password);
    // Check Connection
    if ($conn->connect_error) { 
        die("Connection failed: " . $conn->connect_error); 
    } 

    // Create a new DB
    $myQuery = "CREATE DATABASE myDB";
    if($conn->query($sql) === TRUE){
        echo "Database created";
    }
    else{
        echo "Error creating database: " . $conn->error;
    }

    // CLOSE CONNECTION
    $conn->close();
?>
```

### Δημιουργία Πίνακα
```php
<?php
    // Create new Table
    $myQuery = "
        CREATE TABLE IF NOT EXISTS Persons(
            id INT(10) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
            P_name VARCHAR(50) NOT NULL,
            website VARCHAR(30) NOT NULL
    )";

    // Execute Query
    if($conn->query($myQuery) === TRUE){
        echo "<br>Table Created <br>";
    }
    else {
        echo "<br>Error creating table: <br>" . $conn->error."<br>"; 
    }
    // CLOSE CONNECTION (USE ONLY WHEN DONE)
    $conn->close();
?>
```

### Εισαγωγή Τιμών σε Πίνακα
```php
<?php
    $name = 'Archo'; $email = 'archo@ntis.gr';
    // Insert to DB
    $myQuery = "
            INSERT INTO Persons(id, P_name, website)
            VALUES(0, '$name', '$email');
    ";

    // Execute Query
    if($conn->query($myQuery) === TRUE){
        echo "New record created successfully"; 
    } else { 
        echo "Error: " . $myQuery . "<br>" . $conn->error; 
    }
    // CLOSE CONNECTION (USE ONLY WHEN DONE)
    $conn->close();
?>
```

### Εμφάνιση Τιμών από Πίνακα
```php
<?php
    // Show Table data
    $myQuery = "SELECT * FROM Persons";
    $result = $conn->query($myQuery);

    if ($result->num_rows > 0) {    // True if the query has results to show 
        // output data of each row 
        while($row = $result->fetch_assoc()) { 
            echo " <br>
                ID: " . $row["id"].
                " | Name: " . $row["P_name"]." "
                . $row["website"]. "<br>"; 
        } 
    } 
    else { 
        echo "0 results"; 
    }
?>
```

<h1>
<b>ΜΟΛΙΣ ΤΕΛΕΙΩΣΟΥΜΕ ΜΕ ΤΗΝ ΒΑΣΗ ΠΑΝΤΑ ΚΛΕΙΝΟΥΜΕ ΤΟ CONNECTION</b>
</h1> <br><br>

```php
<?php
    // CLOSE CONNECTION (USE ONLY WHEN DONE)
    $conn->close();
?>
```


