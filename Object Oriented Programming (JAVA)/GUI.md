# JAVA NOTES: GUI 
# ΠΕΡΙΕΧΟΜΕΝΑ
1. [Γραφικά Συστατικά](#γραφικά-συστατικά)
    - [JList](#jlist)
    - [JButton](#jbutton)
    - [JTextArea](#jtextarea)
    - [JTextField](#jtextfield)
2. [Layout Managers](#layout-managers)
3. [Listeners](#listeners)

## Για την υλοποίηση ενός απλού παραθύρου:

```java
import javax.swing.Jframe;

public class MainFrame extends JFrame {
    
    public MainFrame() {
        this.setSize(200, 200);
        this.setTitle("WINDOW TITLE");
        this.setVisible(true);
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}
```

<i>ΑΝ ΔΕΝ ΘΕΛΟΥΜΕ ΝΑ ΤΕΡΜΑΤΙΖΕΤΕ ΤΟ ΠΡΟΓΡΑΜΜΑ ΜΟΛΙΣ ΠΑΤΗΘΕΙ ΤΟ “Χ” ΣΤΟ ΠΑΡΑΘΥΡΟ, ΑΛΛΑ ΘΈΛΟΥΜΕ ΑΠΛΑ ΝΑ ΕΞΑΦΑΝΙΖΕΤΑΙ ΤΟ ΠΑΡΑΘΥΡΟ:</i><br>

```java
this.setDefaultCloseOperation(JFrame HIDE_ON_CLOSE);
```

## Τοποθέτηση Γραφικών Συστατικών
Για την τοποθέτηση γραφικών συστατικών ακολουθούμε την εξής διαδικασία:

1. Κατασκευάζουμε ένα panel και τα γραφικά συστατικά που χρειαζόμαστε
2. Τοποθετούμε τα Γ.Σ. στο panel
3. Τοποθετούμε το panel στον υποδοχέα

<b>Παράδειγμα:</b> <br>

```java
import javax.swing.*;

public class MainFrame extends JFrame {
    public MainFrame(){
        // Κατασκευή Panel και Γραφικών Συστατικών
        this.button = new JButton();
        this.panel = new JPanel();
        // Τοποθέτηση Γ.Σ. στο Panel
        this.panel.add(this.button);
        // Τοποθέτηση Panel στον υποδοχέα
    }
}
```

## Γραφικά Συστατικά
### JList
Για την δημιουργία ενός γραφικού συστατικού JList: <br>
1. Κατασκευάζουμε ένα αντικείμενο JList
2. Κατασκευάζουμε ένα ListModel για το αντικείμενο JList
3. Τοποθετούμε τα στοιχεία που θέλουμε να εμφανίσει η JList στο ListModel
4. Τοποθετούμε το ListModel ως μοντέλο στην JList
5. Τοποθετούμε το αντικείμενο JList στο Panel

```java
public class myFrame extends JFrame {
    private JPanel panel;
    private JList list;

    public myFrame() {
        this.panel = new JPanel();

        // 1. Κατασκευάζουμε ένα αντικείμενο JList
        this.list = new JList();
        // 2. Κατασκευάζουμε ένα ListModel για το αντικείμενο JList
        DefaultListModel model = new DefaultListModel();
        // 3. Τοποθετούμε τα στοιχεία στο ListModel
        for(Item item: ListOfItems) {
            model.addElement(item);
        }
        // 4. Τοποθετούμε το ListModel ως μοντέλο στην JList
        this.list.setModel(model);
        // 5. Τοποθετούμε το αντικείμενο JList στο Panel
        this.panel.add(list);
    }
}
```

### JButton
Για την δημιουργία ενός Γ.Σ. JButton:
```java
public myFrame() {
    this.panel = new JPanel();
    
    // 1. Κατασκευάζουμε ένα JButton
    this.button = new JButton("Click Me Man!");
    // 2. Το τοποθετούμε στο panel
    this.panel.add(this.button);
}
```

### JTextarea
Για την δημιουργία JTextArea:
```java
public myFrame() {
    this.panel = new JPanel();
    
    // 1. Κατασκευάζουμε ένα JTextarea
    this.textArea = new JTextarea(ROWS, COLUMNS);
    // 2. Το τοποθετούμε στο panel
    this.panel.add(this.textArea);
}
```
Για να <B>προσθέσουμε</b> κείμενο:
```java
this.textArea.append("KEIMENO MPLA MPLA");
```
Αν θέλουμε <i>ο χρήστης να <b>μην μπορει να επεξεργαστεί</b> το κείμενο</i>:
```java
this.textArea.setEditable(false);   // Το κείμενο δεν επεξεργάζεται
this.textArea.setEditable(true);   // Το κείμενο επεξεργάζεται
```

### JTextField
Για την δημιουργία JTexField:
```java
public myFrame() {
    this.panel = new JPanel();
    
    // 1. Κατασκευάζουμε ένα JTextarea
    this.textField = new JTexField("Enter Email: ", size); 
    // 2. Το τοποθετούμε στο panel
    this.panel.add(this.textField);
}
```
Αν θέλουμε <i>ο χρήστης να <b>μην μπορει να επεξεργαστεί</b> το κείμενο</i>:

```java
this.textField.setEditable(false);   // Το κείμενο δεν επεξεργάζεται
this.textField.setEditable(true);   // Το κείμενο επεξεργάζεται
```

### JFileChooser
```java
// Code to make object
fileChooser = new JFileChooser();
// Code to show File Chooser and get the selected file
int returnValue = fileChooser.showOpenDialog(parentPanel);

if(returnValue == JFileChooser.OPEN_DIALOG){    // open Btn Clicked (user selected file)
    File file = fileChooser.getSelectedFile();
    .
    .
    .
}

```

## Layout Managers
### Border Layout
![image](https://user-images.githubusercontent.com/77233507/187683661-e4bb69c9-8e45-470d-bf1e-6c47dee54828.png)
1. Κατασκευή panel (ή γνωστοποίηση του με:  Container pane = myframe.getContentPane())
2. Κατασκευή γραφικών συστατικών
3. Τοποθέτηση των γραφικών συστατικών στο panel δίνοντας την θέση που θέλω να μπουν:
```java
panel.add(button, BorderLayout.CENTER)
```
<b>Διαθέσιμες Θέσεις:</b> <br>
```java
BorderLayout.PAGE_START
BorderLayout.LINE_START
BorderLayout.CENTER
BorderLayout.LINE_END
BorderLayout.PAGE_END
```

## Listeners
2 Τρόποι. <br>
Είτε:
```java
btn.addActionListener(new ActionListener() {
	public void actionPerformed(ActionEvent e) {
		System.out.println("YOU CLICKED A BUTTON");
	}
});
```
Είτε με κατασκευή κλάσης μέσα στην κλάσση την γραφικής διασύνδεσης
```java
class myActionListener implements ActionListener {
    public void actionPerformed(ActionEvent e) {
		if(e.getSource == buttonOne) {
            System.out.println("YOU CLICKED BUTTON No1");
        }
        else if(e.getSource == buttonTwo) {
            System.out.println("YOU CLICKED BUTTON No2");
        }
	}
}
```
