# Technical Documentation for SpellChecker
Written by James Canterbury

---

### Introduction
This file describes how to use the spell checker provided. The spell checker is written in Java language and contains four different files each with a specific purpose. The spell checker is a rudimentary spell checker and when given a word it will say it is a valid word or if it is incorrect it will suggest alternate words.

---
### Description of equipment and List of Materials
Things you will need to run this program
<ul>
<li>The four files found in this folder needed to make the program function properly </li>
<li>a way to compile the files using a Java compiler</li>
<li>a way to run the compiled files</li>
</ul>

---
### Code example
```
// Read in the entire dictionary...
// sk is a scanner object which reads in the dictionary and then user input
// x is a data structure used to store the words in the dictionary
while (sk.hasNext()) {
	String word = sk.next();
	x.insert(word);      
}
System.out.println("Dicitonary loaded...");

sk = new Scanner(System.in);

// Keep suggesting alternatives as long as the user makes an input.
while (sk.hasNext()) {
	String word = sk.next();
	if (x.find(word))
		System.out.println(word + " is correct.");
	else {
		char[] alphabet = "abcdefghijklmnopqrstuvwxyz".toCharArray();
		System.out.println("Suggesting alternatives ...");
		for (int i = 0; i < word.length(); i++) {
			StringBuffer a = new StringBuffer(word);
			for (int j = 0; j < 26; j++) {
				char c = alphabet[j];
				a.setCharAt(i, c);
				if (x.find(a.toString()))
					System.out.println(a.toString());
			}   
		}
	}
}
```
---
### Installation instructions

Download the files in the folder then place them in a good spot you can find them when you need to compile them

---
### Example(s) of your code (if applicable)
This is the StringNode class which is used by StringSet below to store each word
```
public class StringNode {

  private String key;
  private StringNode next;

  public StringNode(String _key, StringNode _next) {
    key = _key;
    next = _next;
  }

  public String getKey() {
    return key;
  }

  public void setKey(String _key) {
    key = _key;
  }

  public StringNode getNext() {
    return next;
  }

  public void setNext(StringNode _next) {
    next = _next;
  }

}
```

This is the StringSet class which is used to store each word and provides the following methods:
<ul>
<li>Insert</li>
<li>Find</li>
<li>Print</li>
</ul>

```
/**
 * This is a string set data structure, that is implemented as a Hash Table.
 * This data structure supports operations insert, find and print - that insert a new
 * String, finds a String key and prints the contents of the data structure resp.
 */
public class StringSet {

  StringNode [] table;	// Hash table - collisions resolved through chaining.
  int numelements;	// Number of elements actually stored in the structure.
  int size;					// Allocated memory (size of the hash table).
  int x = 7;

  /**
   * Constructor: initilaizes numelements, size and initial table size.
   */
  public StringSet() {
    numelements = 0;
    size = 100;
    table = new StringNode[size];
  }

  /*
   * inserts a new key into the set. Inserts it at the head of the linked list given by its hash value.
   */
  public void insert(String key) {
      if (numelements == size) {
      //TODO: need to expand the hash table and rehash its contents.
      int old_size = size;
      StringNode [] old = new StringNode[old_size];
      for (int i = 0; i < old_size; i++) {
          for (StringNode curr = table[i]; curr != null; curr = curr.getNext()) {
              int b = hash(curr.getKey());
              old[b] = new StringNode(curr.getKey(), old[b]);
          }
      }
      size = size * 2;
      table = new StringNode[size];
      for (int i = 0; i < old_size; i++)
          for (StringNode curr = old[i]; curr != null; curr = curr.getNext())
          {
              int a = hash(curr.getKey());
              table[a] = new StringNode(curr.getKey(), table[a]);
          }
    }      
    //TODO: Code for actual insert.
    int s = hash(key);
    table[s] = new StringNode(key, table[s]);
    numelements++;
  }

  /*
   * finds if a String key is present in the data structure. Returns true if found, else false.
   */
  public boolean find(String key) {
    int s = hash(key);
    for (StringNode curr = table[s]; curr != null; curr = curr.getNext())
    {
        if (curr.getKey().equals(key))
        {
            return true;
        }
    }
    return false;
  }

  /*
   * Prints the contents of the hash table.
   */
  public void print() {
    for (int i = 0; i < size; i++) {
        for (StringNode curr = table[i]; curr != null; curr = curr.getNext())
            System.out.println(curr.getKey());
    }
  }

  /*
   * The hash function that returns the index into the hash table for a string k.
   */
  private int hash(String k) {
    int h = 0;
    // TODO: Compute a polynomial hash function for the String k. Make sure that the hash value h returned is a proper index
    // in the hash table, ie. in the range [0...capacity-1].
    for (int i = 0; i < k.length(); i++)
    {
        h = (h * x + k.charAt(i)) % size;
    }
    return h;
  }
}

```
---
### FAQs

Question: How many characters does the spell checker change to find alternate words?
Answer: 1 character, The spellchecker starts at the first letter of the word given by the user and changes that letter to each letter in the alphabet and checks to see if it is a valid word. The spell checker does not change the length of the input word to provide an alternative.

Question: Why does the dictionary contain special characters?
Answer: These should be ignored and input should not contain special characters or capital letters. User input should contain only lowercase letters.

---
### Troubleshooting/Where to Get Support
Make sure you have read the section of this document that is labeled *Instructions for Use*.

If you need help with getting the program to work you can email the writer at canterburyjr@appstate.edu.

---
### How to Contribute
If you wish to add extra functionality or anything of the sort you may modify the files and send changes to the writer at canterburyjr@appstate.edu.

---
### Licensing

Not sure what is supposed to go here

---
### Instructions for Use

How to run the program
<ul>
<li>Download the four files needed into a directory</li>
<li>Compile the .java files</li>
<li>Run the program by java SpellChecker</li>
<li>Next you must enter a word that is all lower case and has no special characters</li>
<li>After you press enter it will either say the word is correct or it will say it is incorrect and suggest alternatives</li>
<li>You can keep entering in words or you can stop the program by doing ctrl + c</li>
</ul>

---
