HomeInventory.java:
//HomeInventory.java 
package homeinventory;
import javax.swing.*;
import javax.swing.filechooser.*; 
import java.awt.*;
import java.awt.event.*;
import java.beans.*;
import com.toedter.calendar.*; 
import java.awt.geom.*;
import java.io.*;
import java.util.*;
import java.text.*;
import java.awt.print.*;
public class HomeInventory extends JFrame {
JToolBar inventoryToolBar = new JToolBar();
JButton newButton = new JButton(new ImageIcon("new.gif"));
JButton deleteButton = new JButton(new ImageIcon("delete.gif")); 
JButton saveButton = new JButton(new ImageIcon("save.gif"));
 JButton previousButton = new JButton(new ImageIcon("previous.gif"));
 JButton nextButton = new JButton(new ImageIcon("next.gif")); 
JButton printButton = new JButton(new ImageIcon("print.gif"));
 JButton exitButton = new JButton();
JLabel itemLabel = new JLabel();
JTextField itemTextField = new JTextField();
JLabel locationLabel = new JLabel();
JComboBox locationComboBox = new JComboBox(); JCheckBox markedCheckBox = new JCheckBox(); JLabel serialLabel = new JLabel();
JTextField serialTextField = new JTextField();
JLabel priceLabel = new JLabel();
JTextField priceTextField = new JTextField();
JLabel dateLabel = new JLabel();
JDateChooser dateDateChooser = new JDateChooser(); JLabel storeLabel = new JLabel();
JTextField storeTextField = new JTextField();
JLabel noteLabel = new JLabel();
JTextField noteTextField = new JTextField();
JLabel photoLabel = new JLabel();
static JTextArea photoTextArea = new JTextArea(); JButton photoButton = new JButton();
JPanel searchPanel = new JPanel();
JButton[] searchButton = new JButton[26];
PhotoPanel photoPanel = new PhotoPanel();
static final int maximumEntries = 300;
static int numberEntries;
static InventoryItem[] myInventory = new InventoryItem[maximumEntries]; 
int currentEntry;
static final int entriesPerPage = 2;
static int lastPage;
public static void main(String args[]) {
new HomeInventory().show(); }
public HomeInventory()
{
// frame constructor
setTitle("Home Inventory Manager"); setResizable(false);
se tDe faultClose Ope ration(JFrame .DO_NOTHING_ON_CLOSE);
 addWindowListener(new WindowAdapter()
{
public void windowClosing(WindowEvent evt) {
exitForm(evt); }
});
getContentPane().setLayout(new GridBagLayout()); 
GridBagConstraints gridConstraints;
inve ntoryToolBar.setFloatable (false );
inve ntoryToolBar.setBackground(Color.BLUE);
inve ntoryToolBar.setOrientation(SwingConstants.VERTICAL);
 gridConstraints = new GridBagConstraints();
 gridConstraints.gridx = 0;
gridConstraints.gridy = 0;
gridConstraints.gridheight = 8;
gridConstraints.fill = GridBagConstraints.VERTICAL;
getContentPane().add(inventoryToolBar, gridConstraints);
inventoryToolBar.addSe parator();
Dimension bSize = new Dimension(70, 50);
 newButton.setText("New"); 
sizeButton(newButton, bSize);
 newButton.setToolTipText("Add New Item");
newButton.setHorizontalTextPosition(SwingConstants.CENTER);
newButton.setVerticalTextPosition(SwingConstants.BOTTOM);
newButton.setFocusable (false );
inventoryToolBar.add(newButton);
newButton.addActionListener(new ActionListener() {
public void actionPerformed(ActionEvent e) {
newButtonActionPerformed(e ); }
});
deleteButton.setText("Delete"); 
sizeButton(deleteButton, bSize); 
deleteButton.setToolTipText("Delete Current Item");
deleteButton.setHorizontalTextPosition(SwingConstants.CENTER);
deleteButton.setVerticalTextPosition(SwingConstants.BOTTOM); 
deleteButton.setFocusable(false);
inventoryToolBar.add(deleteButton); 
deleteButton.addActionListener(new ActionListener()
{
public void actionPerformed(ActionEvent e) {
deleteButtonActionPerformed(e ); }
});
saveButton.setText("Save"); 
sizeButton(saveButton, bSize); 
saveButton.setToolTipText("Save Current Item");
saveButton.setHorizontalTextPosition(SwingConstants.CENTER);
save Button.setVerticalTextPosition(SwingConstants.BOTTOM); 
saveButton.setFocusable(false);
inventoryToolBar.add(save Button); 
saveButton.addActionListener(new ActionListener()
{
public void actionPerformed(ActionEvent e) {
saveButtonActionPerformed(e ); }
});
inventoryToolBar.addSeparator();
previousButton.setText("Previous"); 
sizeButton(previousButton, bSize); 
previousButton.setToolTipText("Display Previous Item");
previousButton.setHorizontalTextPosition(SwingConstants.CENTER);
previousButton.setVerticalTextPosition(SwingConstants.BOTTOM); 
previousButton.setFocusable (false );
inventoryToolBar.add(previousButton); 
previousButton.addActionListener(new ActionListener()
{
public void actionPerformed(ActionEvent e) {
previousButtonActionPerformed(e ); }
});
nextButton.setText("Next"); 
sizeButton(nextButton, bSize); 
nextButton.setToolTipText("Display Next Item");
nextButton.setHorizontalTextPosition(SwingConstants.CENTER);
nextButton.setVerticalTextPosition(SwingConstants.BOTTOM); 
nextButton.setFocusable (false );
inventoryToolBar.add(nextButton); 
nextButton.addActionListener(new ActionListener()
{
public void actionPerformed(ActionEvent e) {
nextButtonActionPerformed(e ); }
});
inve ntoryToolBar.addSe parator();
printButton.se tTe xt("Print"); sizeButton(printButton, bSize); printButton.setToolTipText("Print Inventory List");
printButton.se tHoriz ontalTe xtPosition(SwingConstants.CENTER);
printButton.se tVe rticalTe xtPosition(SwingConstants.BOTTOM); printButton.se tFocusable (false );
inve ntoryToolBar.add(printButton); printButton.addActionListener(new ActionListener()
{
public void actionPerformed(ActionEvent e) {
printButtonActionPe rforme d(e ); }
});
exitButton.setText("Exit"); sizeButton(exitButton, bSize); exitButton.setToolTipText("Exit Program"); e xitButton.se tFocusable (false );
inve ntoryToolBar.add(e xitButton); exitButton.addActionListener(new ActionListener() {
public void actionPerformed(ActionEvent e) {
e xitButtonActionPe rforme d(e ); }
});
itemLabel.setText("Inventory Item"); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 1; gridConstraints.gridy = 0;
gridConstraints.insets = new Insets(10, 10, 0, 10); gridConstraints.anchor = GridBagConstraints.EAST; getContentPane().add(itemLabel, gridConstraints);
itemTextField.setPreferredSize(new Dimension(400, 25)); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 2;
gridConstraints.gridy = 0;
gridConstraints.gridwidth = 5;
gridConstraints.insets = new Insets(10, 0, 0, 10); gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(itemTextField, gridConstraints); itemTextField.addActionListener(new ActionListener () {
public void actionPerformed(ActionEvent e) {
ite mTe xtFie ldActionPe rforme d(e ); }
});
locationLabe l.se tTe xt("Location");
gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 1;
gridConstraints.gridy = 1;
gridConstraints.insets = new Insets(10, 10, 0, 10); gridConstraints.anchor = GridBagConstraints.EAST; getContentPane().add(locationLabel, gridConstraints);
locationComboBox.setPreferredSize(new Dimension(270, 25)); locationComboBox.setFont(new Font("Arial", Font.PLAIN, 12)); locationComboBox.se tEditable (true );
locationComboBox.se tBackground(Color.WHITE); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 2;
gridConstraints.gridy = 1; gridConstraints.gridwidth = 3; gridConstraints.insets = new Insets(10, 0, 0, 10);
gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(locationComboBox, gridConstraints); locationComboBox.addActionListener(new ActionListener () {
public void actionPerformed(ActionEvent e) {
locationComboBoxActionPe rforme d(e ); }
});
marke dChe ckBox.se tTe xt("Marke d?");
marke dChe ckBox.se tFocusable (false );
gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 5;
gridConstraints.gridy = 1;
gridConstraints.insets = new Insets(10, 10, 0, 0); gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(markedCheckBox, gridConstraints);
serialLabel.setText("Serial Number"); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 1;
gridConstraints.gridy = 2;
gridConstraints.insets = new Insets(10, 10, 0, 10); gridConstraints.anchor = GridBagConstraints.EAST; getContentPane().add(serialLabel, gridConstraints);
serialTextField.setPreferredSize(new Dimension(270, 25)); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 2;
gridConstraints.gridy = 2;
gridConstraints.gridwidth = 3;
gridConstraints.insets = new Insets(10, 0, 0, 10); gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(serialTextField, gridConstraints); serialTextField.addActionListener(new ActionListener () {
public void actionPerformed(ActionEvent e) {
se rialTe xtFie ldActionPe rforme d(e ); }
});
priceLabel.setText("Purchase Price");
gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 1;
gridConstraints.gridy = 3;
gridConstraints.insets = new Insets(10, 10, 0, 10); gridConstraints.anchor = GridBagConstraints.EAST; getContentPane().add(priceLabel, gridConstraints); priceTextField.setPreferredSize(new Dimension(160, 25)); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 2;
gridConstraints.gridy = 3;
gridConstraints.gridwidth = 2;
gridConstraints.insets = new Insets(10, 0, 0, 10); gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(priceTextField, gridConstraints); priceTextField.addActionListener(new ActionListener () {
public void actionPerformed(ActionEvent e) {
price Te xtFie ldActionPe rforme d(e ); }
});
dateLabel.setText("Date Purchased"); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 4;
gridConstraints.gridy = 3;
gridConstraints.insets = new Insets(10, 10, 0, 0); gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(dateLabel, gridConstraints);
dateDateChooser.setPreferredSize(new Dimension(120, 25)); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 5;
gridConstraints.gridy = 3;
gridConstraints.gridwidth = 2;
gridConstraints.insets = new Insets(10, 0, 0, 10);
gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(dateDateChooser, gridConstraints); dateDateChooser.addPropertyChangeListener(new PropertyChangeListener() {
public void propertyChange(PropertyChangeEvent e) {
date Date Choose rPrope rtyChange (e ); }
});
storeLabel.setText("Store/Website"); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 1;
gridConstraints.gridy = 4;
gridConstraints.insets = new Insets(10, 10, 0, 10); gridConstraints.anchor = GridBagConstraints.EAST; getContentPane().add(storeLabel, gridConstraints);
storeTextField.setPreferredSize(new Dimension(400, 25)); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 2;
gridConstraints.gridy = 4;
gridConstraints.gridwidth = 5;
gridConstraints.insets = new Insets(10, 0, 0, 10); gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(storeTextField, gridConstraints); storeTextField.addActionListener(new ActionListener () {
public void actionPerformed(ActionEvent e) {
store Te xtFie ldActionPe rforme d(e ); }
noteLabel.setText("Note");
gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 1;
gridConstraints.gridy = 5;
gridConstraints.insets = new Insets(10, 10, 0, 10); gridConstraints.anchor = GridBagConstraints.EAST; getContentPane().add(noteLabel, gridConstraints);
noteTextField.setPreferredSize(new Dimension(400, 25)); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 2;
gridConstraints.gridy = 5;
gridConstraints.gridwidth = 5;
gridConstraints.insets = new Insets(10, 0, 0, 10); gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(noteTextField, gridConstraints); noteTextField.addActionListener(new ActionListener () {
public void actionPerformed(ActionEvent e) {
note Te xtFie ldActionPe rforme d(e ); }
});
photoLabe l.se tTe xt("Photo");
gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 1;
gridConstraints.gridy = 6;
gridConstraints.insets = new Insets(10, 10, 0, 10); gridConstraints.anchor = GridBagConstraints.EAST; getContentPane().add(photoLabel, gridConstraints);
});
photoTextArea.setPreferredSize(new Dimension(350, 35));
photoTextArea.setFont(new Font("Arial", Font.PLAIN, 12)); photoTe xtAre a.se tEditable (false );
photoTe xtAre a.se tLine Wrap(true );
photoTe xtAre a.se tWrapStyle Word(true ); photoTextArea.setBackground(new Color(255, 255, 192));
photoTe xtAre a.se tBorde r(Borde rFactory.cre ate Line Borde r(Color.BLACK)); photoTe xtAre a.se tFocusable (false );
gridConstraints = new GridBagConstraints();
gridConstraints.gridx = 2;
gridConstraints.gridy = 6;
gridConstraints.gridwidth = 4;
gridConstraints.insets = new Insets(10, 0, 0, 10); gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(photoTextArea, gridConstraints);
photoButton.se tTe xt("...");
gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 6;
gridConstraints.gridy = 6;
gridConstraints.insets = new Insets(10, 0, 0, 10); gridConstraints.anchor = GridBagConstraints.WEST; getContentPane().add(photoButton, gridConstraints); photoButton.addActionListener(new ActionListener () {
public void actionPerformed(ActionEvent e) {
photoButtonActionPe rforme d(e ); }
});
searchPanel.setPreferredSize(new Dimension(240, 160));
searchPanel.setBorder(BorderFactory.createTitledBorder("Item Search")); searchPanel.setLayout(new GridBagLayout());
gridConstraints = new GridBagConstraints();
gridConstraints.gridx = 1;
gridConstraints.gridy = 7;
gridConstraints.gridwidth = 3;
gridConstraints.insets = new Insets(10, 0, 10, 0); gridConstraints.anchor = GridBagConstraints.CENTER; getContentPane().add(searchPanel, gridConstraints);
int x = 0, y = 0;
// create and position 26 buttons for (int i = 0; i < 26; i++)
{
// create new button
searchButton[i] = new JButton();
// set text property searchButton[i].setText(String.valueOf((char) (65 + i))); searchButton[i].setFont(new Font("Arial", Font.BOLD, 12)); searchButton[i].setMargin(new Insets(-10, -10, -10, -10)); sizeButton(searchButton[i], new Dimension(37, 27));
se archButton[i].se tBackground(Color.YELLOW);
se archButton[i].se tFocusable (false );
gridConstraints = new GridBagConstraints(); gridConstraints.gridx = x;
gridConstraints.gridy = y;
searchPanel.add(searchButton[i], gridConstraints);
// add method
searchButton[i].addActionListener(new ActionListener ()
{
public void actionPerformed(ActionEvent e) {
se archButtonActionPe rforme d(e ); }
});
x++;
// six buttons per row if (x % 6 == 0)
{
x = 0;
y++; }
photoPanel.setPreferredSize(new Dimension(240, 160)); gridConstraints = new GridBagConstraints(); gridConstraints.gridx = 4;
gridConstraints.gridy = 7;
gridConstraints.gridwidth = 3;
gridConstraints.insets = new Insets(10, 0, 10, 10); gridConstraints.anchor = GridBagConstraints.CENTER; getContentPane().add(photoPanel, gridConstraints);
pack();
Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();
setBounds((int) (0.5 * (screenSize.width - getWidth())), (int) (0.5 * (screenSize.height - getHeight())), getWidth(), getHeight());
int n;
// open file for entries try
{
BufferedReader inputFile = new BufferedReader(new FileReader("inventory.txt"));
numberEntries =
Inte ge r.value Of(inputFile .re adLine ()).intValue ();
if (numberEntries != 0) {
for (int i = 0; i < numberEntries; i++) {
myInventory[i] = new InventoryItem(); myInventory[i].description = inputFile.readLine(); myInventory[i].location = inputFile.readLine(); myInventory[i].serialNumber = inputFile.readLine(); myInventory[i].marked =
Boole an.value Of(inputFile .re adLine ()).boole anValue (); myInventory[i].purchasePrice =
inputFile .re adLine ();
myInventory[i].purchaseDate = inputFile.readLine();
myInventory[i].purchaseLocation = inputFile .re adLine ();
myInventory[i].note = inputFile.readLine();
myInventory[i].photoFile = inputFile.readLine(); }
}
// read in combo box elements
n = Integer.valueOf(inputFile.readLine()).intValue(); if (n != 0)
{
for (int i = 0; i < n; i++)
{
locationComboBox.addIte m(inputFile .re adLine ());
} }
inputFile .close (); currentEntry = 1; showEntry(curre ntEntry);
}
catch (Exception ex) {
numberEntries = 0;
currentEntry = 0; }
if (numberEntries == 0) {
ne wButton.se tEnable d(false ); deleteButton.setEnabled(false); ne xtButton.se tEnable d(false );
pre viousButton.se tEnable d(false ); printButton.se tEnable d(false );
} }
private void exitForm(WindowEvent evt) {
if (JOptionPane.showConfirmDialog(null, "Any unsaved changes will be lost.\nAre you sure you want to exit?", "Exit Program", JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE) == JOptionPane.NO_OPTION)
re t urn;
// write entries back to file try
{
PrintWriter outputFile = new PrintWriter(new BufferedWriter(new File Write r("inve ntory.txt")));
outputFile .println(numbe rEntrie s); if (numberEntries != 0)
{
for (int i = 0; i < numberEntries; i++) {
outputFile .println(myInve ntory[i].de scription); outputFile .println(myInve ntory[i].location); outputFile .println(myInve ntory[i].se rialNumbe r); outputFile .println(myInve ntory[i].marke d); outputFile .println(myInve ntory[i].purchase Price ); outputFile .println(myInve ntory[i].purchase Date );
outputFile .println(myInve ntory[i].purchase Location); outputFile .println(myInve ntory[i].note );
outputFile .println(myInve ntory[i].photoFile ); }
}
// write combo box entries
outputFile .println(locationComboBox.ge tIte mCount()); if (locationComboBox.getItemCount() != 0)
{
for (int i = 0; i < locationComboBox.getItemCount(); i++) outputFile .println(locationComboBox.ge tIte mAt(i));
}
outputFile .close (); }
catch (Exception ex) {
}
System.exit(0); }
private void newButtonActionPerformed(ActionEvent e) {
checkSave();
blankValue s(); }
private void deleteButtonActionPerformed(ActionEvent e) {
if (JOptionPane.showConfirmDialog(null, "Are you sure you want to delete this item?", "Delete Inventory Item", JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE) == JOptionPane.NO_OPTION)
re t urn;
de le te Entry(curre ntEntry); if (numberEntries == 0)
{
currentEntry = 0;
blankValue s(); }
else {
curre ntEntry--;
if (currentEntry == 0)
currentEntry = 1; showEntry(curre ntEntry);
} }
private void saveButtonActionPerformed(ActionEvent e) {
// check for description
ite mTe xtFie ld.se tTe xt(ite mTe xtFie ld.ge tTe xt().trim()); if (itemTextField.getText().equals(""))
{
JOptionPane.showConfirmDialog(null, "Must have item description.", "Error", JOptionPane.DEFAULT_OPTION, JOptionPane.ERROR_MESSAGE);
ite mTe xtFie ld.re que stFocus();
re t urn; }
if (newButton.isEnabled()) {
// delete edit entry then resave
de le te Entry(curre ntEntry); }
// capitalize first letter
String s = itemTextField.getText();
itemTextField.setText(s.substring(0, 1).toUpperCase() + s.substring(1)); numbe rEntrie s++;
// determine new current entry location based on description currentEntry = 1;
if (numberEntries != 1)
{
do {
if
(itemTextField.getText().compareTo(myInventory[currentEntry - 1].description) < 0)
bre ak;
curre ntEntry++;
}
while (currentEntry < numberEntries); }
// move all entries below new value down one position unless at end if (currentEntry != numberEntries)
{
for (int i = numberEntries; i >= currentEntry + 1; i--) {
myInventory[i - 1] = myInventory[i - 2];
myInventory[i - 2] = new InventoryItem(); }
}
myInventory[currentEntry - 1] = new InventoryItem();
myInventory[currentEntry - 1].description = itemTextField.getText();
myInventory[currentEntry - 1].location =
locationComboBox.ge tSe le cte dIte m().toString();
myInventory[currentEntry - 1].marked = markedCheckBox.isSelected();
myInventory[currentEntry - 1].serialNumber = serialTextField.getText();
myInventory[currentEntry - 1].purchasePrice = priceTextField.getText();
myInventory[currentEntry - 1].purchaseDate = date ToString(date Date Choose r.ge tDate ());
myInventory[currentEntry - 1].purchaseLocation = storeTextField.getText(); myInventory[currentEntry - 1].photoFile = photoTextArea.getText(); myInventory[currentEntry - 1].note = noteTextField.getText(); showEntry(curre ntEntry);
if (numberEntries < maximumEntries) ne wButton.se tEnable d(true );
else
ne wButton.se tEnable d(false );
de le te Button.se tEnable d(true );
printButton.se tEnable d(true ); }
private void previousButtonActionPerformed(ActionEvent e) {
checkSave();
curre ntEntry--; showEntry(curre ntEntry);
}
private void nextButtonActionPerformed(ActionEvent e) {
checkSave();
curre ntEntry++; showEntry(curre ntEntry);
}
private void printButtonActionPerformed(ActionEvent e) {
lastPage = (int) (1 + (numberEntries - 1) / entriesPerPage); PrinterJob inventoryPrinterJob = PrinterJob.getPrinterJob(); inventoryPrinterJob.setPrintable(new InventoryDocument()); if (inventoryPrinterJob.printDialog())
{
try
{
inve ntoryPrinte rJob.print();
}
catch (PrinterException ex) {
JOptionPane.showConfirmDialog(null, ex.getMessage(), "Print Error", JOptionPane.DEFAULT_OPTION, JOptionPane.ERROR_MESSAGE);
} }
}
private void exitButtonActionPerformed(ActionEvent e) {
e xitForm(null); }
private void photoButtonActionPerformed(ActionEvent e) {
JFileChooser openChooser = new JFileChooser();
ope nChoose r.se tDialogType (JFile Choose r.OPEN_DIALOG);
openChooser.setDialogTitle("Open Photo File");
openChooser.addChoosableFileFilter(new FileNameExtensionFilter("Photo Files", "jpg"));
if (openChooser.showOpenDialog(this) == JFileChooser.APPROVE_OPTION) showPhoto(ope nChoose r.ge tSe le cte dFile ().toString());
}
private void searchButtonActionPerformed(ActionEvent e) {
int i;
if (numberEntries == 0)
re t urn;
// search for item letter
String letterClicked = e.getActionCommand(); i = 0;
do
{
if (myInventory[i].description.substring(0, 1).equals(letterClicked)) {
currentEntry = i + 1; showEntry(curre ntEntry); re t urn;
}
i++; }
while (i < numberEntries);
JOptionPane.showConfirmDialog(null, "No " + letterClicked + " inventory items.", "None Found", JOptionPane.DEFAULT_OPTION,
JOptionPane .INFORMATION_MESSAGE);
}
private void itemTextFieldActionPerformed(ActionEvent e) {
locationComboBox.re que stFocus(); }
private void locationComboBoxActionPerformed(ActionEvent e) {
// If in list - exit method
if (locationComboBox.getItemCount() != 0) {
for (int i = 0; i < locationComboBox.getItemCount(); i++) {
if (locationComboBox.getSelectedItem().toString().equals(locationComboBox.ge tIte mAt(i).toString())) {
se rialTe xtFie ld.re que stFocus();
re t urn; }
} }
// If not found, add to list box
locationComboBox.addIte m(locationComboBox.ge tSe le cte dIte m()); se rialTe xtFie ld.re que stFocus();
}
private void serialTextFieldActionPerformed(ActionEvent e) {
price Te xtFie ld.re que stFocus(); }
private void priceTextFieldActionPerformed(ActionEvent e) {
date Date Choose r.re que stFocus(); }
private void dateDateChooserPropertyChange(PropertyChangeEvent e) {
store Te xtFie ld.re que stFocus(); }
private void storeTextFieldActionPerformed(ActionEvent e) {
note Te xtFie ld.re que stFocus(); }
private void noteTextFieldActionPerformed(ActionEvent e) {
photoButton.re que stFocus(); }
private void sizeButton(JButton b, Dimension d) {
b.setPreferredSize(d); b.se tMinimumSiz e (d); b.se tMaximumSiz e (d);
}
private void showEntry(int j) {
// display entry j (1 to numberEntries)
itemTextField.setText(myInventory[j - 1].description); locationComboBox.setSelectedItem(myInventory[j - 1].location); markedCheckBox.setSelected(myInventory[j - 1].marked); serialTextField.setText(myInventory[j - 1].serialNumber); priceTextField.setText(myInventory[j - 1].purchasePrice); dateDateChooser.setDate(stringToDate(myInventory[j - 1].purchaseDate)); storeTextField.setText(myInventory[j - 1].purchaseLocation); noteTextField.setText(myInventory[j - 1].note);
showPhoto(myInventory[j - 1].photoFile);
ne xtButton.se tEnable d(true );
pre viousButton.se tEnable d(true );
if (j == 1)
pre viousButton.se tEnable d(false ); if (j == numberEntries)
ne xtButton.se tEnable d(false ); ite mTe xtFie ld.re que stFocus();
}
private Date stringToDate(String s) {
int m = Integer.valueOf(s.substring(0, 2)).intValue() - 1; int d = Integer.valueOf(s.substring(3, 5)).intValue();
int y = Integer.valueOf(s.substring(6)).intValue() - 1900; return(new Date(y, m, d));
}
private String dateToString(Date dd)
{
String yString = String.valueOf(dd.getYear() + 1900); int m = dd.getMonth() + 1;
String mString = new DecimalFormat("00").format(m); int d = dd.getDate();
String dString = new DecimalFormat("00").format(d); return(mString + "/" + dString + "/" + yString);
}
private void showPhoto(String photoFile) {
if (!photoFile.equals("")) {
try {
photoTe xtAre a.se tTe xt(photoFile ); }
catch (Exception ex) {
photoTextArea.setText(""); }
} else {
photoTextArea.setText(""); }
photoPane l.re paint(); }
private void blankValues() {
// blank input screen
ne wButton.se tEnable d(false ); deleteButton.setEnabled(false); save Button.se tEnable d(true );
pre viousButton.se tEnable d(false );
ne xtButton.se tEnable d(false ); printButton.se tEnable d(false );
ite mTe xtFie ld.se tTe xt(""); locationComboBox.se tSe le cte dIte m(""); markedCheckBox.setSelected(false);
se rialTe xtFie ld.se tTe xt("");
price Te xtFie ld.se tTe xt(""); dateDateChooser.setDate(new Date()); storeTextField.setText(""); noteTextField.setText(""); photoTextArea.setText("");
photoPane l.re paint();
ite mTe xtFie ld.re que stFocus();
}
private void deleteEntry(int j) {
// delete entry j
if (j != numberEntries) {
// move all entries under j up one level for (int i = j; i < numberEntries; i++)
{
myInventory[i - 1] = new InventoryItem();
myInventory[i - 1] = myInventory[i]; }
}
numbe rEntrie s--; }
private void checkSave() {
boolean edited = false;
if (!myInventory[currentEntry - 1].description.equals(itemTextField.getText()))
edited = true;
else if (!myInventory[currentEntry -1].location.equals(locationComboBox.getSelectedItem().toStrin g())) edited = true;
else if (myInventory[currentEntry - 1].marked != markedCheckBox.isSelected()) edited = true;
else if (!myInventory[currentEntry - 1].serialNumber.equals(serialTextField.getText())) edited = true;
else if (!myInventory[currentEntry - 1].purchasePrice.equals(priceTextField.getText())) edited = true;
else if (!myInventory[currentEntry -
1].purchase Date .e quals(date ToString(date Date Choose r.ge tDate ())))
edited = true;
else if (!myInventory[currentEntry -
1].purchase Location.e quals(store Te xtFie ld.ge tTe xt()))
edited = true;
else if (!myInventory[currentEntry - 1].note.equals(noteTextField.getText()))
edited = true;
else if (!myInventory[currentEntry - 1].photoFile.equals(photoTextArea.getText()))
edited = true; if (edited)
{
if (JOptionPane.showConfirmDialog(null, "You have edited this item. Do you want to save the changes?", "Save Item", JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE) == JOptionPane.YES_OPTION)
save Button.doClick(); }
} }
class PhotoPanel extends JPanel {
public void paintComponent(Graphics g) {
Graphics2D g2D = (Graphics2D) g; supe r.paintCompone nt(g2D);
// draw border
g2D.se tPaint(Color.BLACK);
g2D.draw(new Rectangle2D.Double(0, 0, getWidth() - 1, getHeight() - 1));
// show photo
Image photoImage = new
Image Icon(Home Inve ntory.photoTe xtAre a.ge tTe xt()).ge tImage ();
int w = getWidth();
int h = getHeight();
double rWidth = (double) getWidth() / (double) photoImage.getWidth(null); double rHeight = (double) getHeight() / (double) photoImage.getHeight(null); if (rWidth > rHeight)
{
// leave height at display height, change width by amount height is changed
w = (int) (photoImage.getWidth(null) * rHeight); }
else {
// leave width at display width, change height by amount width is changed
h = (int) (photoImage.getHeight(null) * rWidth); }
// center in panel
g2D.drawImage(photoImage, (int) (0.5 * (getWidth() - w)), (int) (0.5 * (getHeight() - h)), w, h, null);
g2D.dispose (); }
}
class InventoryDocument implements Printable {
public int print(Graphics g, PageFormat pf, int pageIndex) {
Graphics2D g2D = (Graphics2D) g;
if ((pageIndex + 1) > HomeInventory.lastPage) {
return NO_SUCH_PAGE; }
int i, iEnd;
// here you decide what goes on each page and draw it
// header
g2D.setFont(new Font("Arial", Font.BOLD, 14));
g2D.drawString("Home Inventory Items - Page " + String.valueOf(pageIndex + 1), (int) pf.getImageableX(), (int) (pf.getImageableY() + 25));
// get starting y
int dy = (int) g2D.getFont().getStringBounds("S", g2D.getFontRenderContext()).getHeight();
int y = (int) (pf.getImageableY() + 4 * dy);
iEnd = HomeInventory.entriesPerPage * (pageIndex + 1); if (iEnd > HomeInventory.numberEntries)
iEnd = HomeInventory.numberEntries;
for (i = 0 + HomeInventory.entriesPerPage * pageIndex; i < iEnd; i++) {
// dividing line
Line2D.Double dividingLine = new
Line2D.Double(pf.getImageableX(), y, pf.getImageableX() + pf.getImageableWidth(), y);
g2D.draw(dividingLine );
y += dy;
g2D.setFont(new Font("Arial", Font.BOLD, 12));
g2D.drawString(HomeInventory.myInventory[i].description, (int) pf.getImageableX(), y); y += dy;
g2D.setFont(new Font("Arial", Font.PLAIN, 12));
g2D.drawString("Location: " + HomeInventory.myInventory[i].location, (int) (pf.getImageableX() + 25), y);
y += dy;
if (HomeInventory.myInventory[i].marked)
g2D.drawString("Item is marked with identifying information.", (int) (pf.getImageableX() + 25), y);
else
g2D.drawString("Item is NOT marked with identifying information.", (int) (pf.getImageableX() + 25), y);
y += dy;
g2D.drawString("Serial Number: " + HomeInventory.myInventory[i].serialNumber, (int) (pf.getImageableX() + 25), y);
y += dy;
g2D.drawString("Price: $" + HomeInventory.myInventory[i].purchasePrice + ",Purchased on: " + HomeInventory.myInventory[i].purchaseDate, (int) (pf.getImageableX() + 25), y);
y += dy;
g2D.drawString("Purchased at: " + HomeInventory.myInventory[i].purchaseLocation, (int) (pf.getImageableX() + 25), y);
y += dy;
g2D.drawString("Note: " + HomeInventory.myInventory[i].note, (int) (pf.getImageableX() + 25), y);
y += dy; try
{
// maintain original width/height ratio
Image inventoryImage = new
Image Icon(Home Inve ntory.myInve ntory[i].photoFile ).ge tImage ();
double ratio = (double) (inventoryImage.getWidth(null)) / (double) inve ntoryImage .ge tHe ight(null);
g2D.drawImage(inventoryImage, (int) (pf.getImageableX() + 25), y, (int) (100 * ratio), 100, null);
}
catch (Exception ex) {
// have place to go in case image file doesn't open }
y += 2 * dy + 100; }
return PAGE_EXISTS; }
}






//InventoryItem.java:
package homeinventory; public class InventoryItem {
public String description; public String location; public boolean marked;
public String serialNumber; public String purchasePrice; public String purchaseDate; public String purchaseLocation; public String note;
public String photoFile; }