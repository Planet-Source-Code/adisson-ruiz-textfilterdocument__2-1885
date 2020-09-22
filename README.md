<div align="center">

## TextFilterDocument


</div>

### Description

Control the input in a textfield. Limit the number of characters allowed in the textbox and block unwanted characters.PLEASE RATE IT.
 
### More Info
 
Use the static constants to define your filter.

//A maximum input of 5 characters of ANY type.

TextFilterDocument d = new TextFilterDocument(TextFilterDocument.ANY,5);

//Accept any charater excluding the following.

String invalidChars = "\\'><?*&%#$%^";

d.setCharToExclude(invalidChars );

JTextField t = new JTextField(5);

t.setDocument(d);


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Adisson Ruiz](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/adisson-ruiz.md)
**Level**          |Advanced
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |Java \(JDK 1\.1\)
**Category**       |[Input/ Output](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/input-output__2-84.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/adisson-ruiz-textfilterdocument__2-1885/archive/master.zip)





### Source Code

```
package utilities.Gui.Text;
import javax.swing.text.*;
import java.awt.*;
public class TextFilterDocument extends PlainDocument
{
 /**For Numbers**/
 private static final String NUMBERS = "0123456789";
 private static final String NUMBERS_WITH_DECIMAL = "0123456789.";
 private static final String LETTERS = "aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ";
 private static final String LETTERS_WITH_SPACE = "aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ ";
 private int FilterType = 0;
 private String validChars = null;
 private String excludeChars = null;
 private boolean hasLimit = false;
 private int Limit = 0;
 private boolean hasExcludeChars = false;
 public static final int ANY = 0;
 public static final int NUMBERS_ONLY = 1;
 public static final int NUMBERS_ONLY_WITH_DECIMAL = 2;
 public static final int LETTERS_ONLY = 3;
 public static final int LETTERS_ONLY_WITH_SPACE = 4;
 private static final int SPECIFIED = 5;
 /**TextFilterDocument, constructor**/
 public TextFilterDocument()
 {
 this(ANY);
 }
 public TextFilterDocument(int FilterType)
 {
 super();
 this.FilterType = FilterType;
 }
 public TextFilterDocument(String validChars)
 {
 super();
 this.validChars = validChars;
 this.FilterType = SPECIFIED;
 }
 public TextFilterDocument(String validChars,int limit)
 {
 this(SPECIFIED,limit);
 this.validChars = validChars;
 }
 public TextFilterDocument(int FilterType,int limit)
 {
 super();
 this.FilterType = FilterType;
 this.Limit = limit;
 hasLimit = true;
 }
 public void setCharToExclude(String excludeChars)
 {
 if (excludeChars.length() > 0)
 {
  hasExcludeChars = true;
  this.excludeChars = excludeChars;
 }
 else
  hasExcludeChars = false;
 }
 /**
 * A String is being inserted into the document.
 * Ensure that all characters are valid.
 * @param offset&#8212;Where the new string goes.
 * @param string&#8212;The String to be inserted after check.
 * @param attributeSet&#8212;Attributes for the new string.
 **/
 public void insertString( int offset, String string,AttributeSet attributeSet )throws BadLocationException
 {
 boolean invalid = false;
 if(string == null )
  return;
 if (hasLimit && Limit == offset)
  invalid = true;
 else if (hasExcludeChars)
 {
  for( int i = 0; i < string.length(); i++ )
		 if(excludeChars.indexOf(string.valueOf(string.charAt(i))) >= 0 )
		  invalid = true;
 }
 else if (FilterType == NUMBERS_ONLY)
 {
		 for( int i = 0; i < string.length(); i++ )
		 if(NUMBERS.indexOf( string.valueOf(string.charAt(i))) == -1 )
		  invalid = true;
 }
 else if (FilterType == NUMBERS_ONLY_WITH_DECIMAL)
 {
		 for( int i = 0; i < string.length(); i++ )
		 if(NUMBERS_WITH_DECIMAL.indexOf( string.valueOf(string.charAt(i))) == -1 )
		  invalid = true;
 }
 else if (FilterType == LETTERS_ONLY)
 {
		 for( int i = 0; i < string.length(); i++ )
		 if( LETTERS.indexOf( string.valueOf(string.charAt(i))) == -1 )
		  invalid = true;
 }
 else if (FilterType == LETTERS_ONLY_WITH_SPACE)
 {
		 for( int i = 0; i < string.length(); i++ )
		 if( LETTERS_WITH_SPACE.indexOf( string.valueOf(string.charAt(i))) == -1 )
		  invalid = true;
 }
 else if (FilterType == SPECIFIED)
 {
		 for( int i = 0; i < string.length(); i++ )
		 if( validChars.indexOf( string.valueOf(string.charAt(i))) == -1 )
		  invalid = true;
 }
 if (invalid)
 {
  // Not a valid string, don't insert the string and beep
		 Toolkit.getDefaultToolkit().beep();
		 return;
 }
 else
  super.insertString( offset, string, attributeSet );
 }
}
```

