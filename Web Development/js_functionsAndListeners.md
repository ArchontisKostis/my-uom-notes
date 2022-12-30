# Χρησιμες Συναρτησεις και Event Listeners
## Περιεχόμενα
1. [Επικύρωση Ασφάλειας Στοιχείων](#επικύρωση-ασφάλειας-στοιχείων)
2. [Επικύρωση Ονόματος](#επικύρωση-ονόματος)
3. [Επικύρωση E-Mail](#επικύρωση-e-mail)
4. [Επικύρωση URL](#επικύρωση-url)
5. [Εισαγωγή Listeners](#εισαγωγή-listeners)


## Επικύρωση Ασφάλειας Στοιχείων
```javascript
// Validate Input Function
function validateInput($data){
    $data = trim($data);
    $data = stripslashes($data);
    $data = htmlspecialchars($data);
    return $data;
}
```

## Επικύρωση Ονόματος
```javascript
// Validate Name
function name_is_valid($name) {
    if (!preg_match("/^[a-zA-Z ]*$/",$name)) { 
        return "Only letters and white space allowed";
    }
}
```

## Επικύρωση E-Mail
```javascript
function mail_is_valid($email) {
    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) { 
        return "Invalid E-Mail"; 
    } 
}
```


## Επικύρωση URL
```javascript
function URL_is_valid($url) {
    if (!preg_match("/\b(?:(?:https?|ftp):\/\/|www\.)[-a-z0-9+&@#\/%?=~_|!:,.;]*[-a-z0-9+&@#\/%=~_|]/i",$url)) { 
        return "Invalid URL"; 
    }
}
```

## Εισαγωγή Listeners
```javascript
var button = document.getElementById('my-button');

button.addEventListener('click', function (evt) {
    this.innerHTML = "You Clicked Me!";
}, false);

// Η τρίτη (boolean) παράμετρος σχετίζεται με τη φάση πυροδότησης (true/false → capture/bubble)
```