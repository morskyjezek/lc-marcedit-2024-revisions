---
title: Working with MARC files
teaching: 20
exercises: 1
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain the difference between mrc and mrk MARC file formats
- Successfully break and open a file of MARC records in the MarcEditor
- Explain character encoding and its importance
- Understand how to read a MARC record in the MarcEditor

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What is a MARC binary file?
- What does it mean to break and make a MARC file and how do I open a file of MARC records in MARCedit?
- Why is encoding important?
- How does the MarcEditor display MARC records?

::::::::::::::::::::::::::::::::::::::::::::::::::

The MaRC format, or Machine Readable Cataloging format, is and old file type. 
The base structure of these files was developed in the 1960s and 1970s, and it was
originally structured to be stored on magnetic tape data storage. Today, the files
are generally stored in a binary bitstream, which is not easily read without significant
effort to "decode" the file. These files are called "binary" files (even though
in the case of the MARC format, most of the characters can be read as they were 
intended to be displayed, if the encoding format is known). These files are also
frequently output by databases, and may have different file extensions. The table
below summarizes the main file types you may encounter.

## MARC file types

MarcEdit recognizes the following MARC file types:

Table: MaRC File Types

| File type | File extension | Usage |
| -------- | :-: | ------------------------------------ |
| Binary MARC file | `mrc` | File format typically used in an  ILS or LSP. Other file extensions provided by vendors (ex. marc, dat, bin) are equivalent. Binary is format consisting of a series of sequential bytes, each of which is eight bits in length. |
| MARCEdit Mnemonic file | `mrk` | File format used by MarcEdit that is a human readable version of the binary file. |
| MARC UTF-8 Text File | `mrk8` | Legacy file format for MARC mnemonic files saved with UTF8 encoding. |
| MARCXML file | `xml` | A MARC file expressed in the eXtensible Markup format or a text-based format for representing structured information. |

To work with a MARC file in the MARCEditor your file needs to be in MARC mnemonic format. If you have a binary file, then that file needs to be converted to the mnemonic format.


### MARCEdit's MaRC Conversion Tools

To work with MARC binary data files, or to convert between metadata formats for library bibliographic data recognized by MarcEdit, click on the MARC Tools icon that has the crossed hammer and spanner in the upper left hand corner of the main menu. The available features are:

- `MarcBreaker`: This "breaks" the MARC binary file into a readable (mnemonic) format that can be edited in the MarcEditor.
- `MarcMaker`: This takes the readable (mnemonic) format MARC data file and creates the MARC binary file.
- `MARC21 to MARC21XML`: This converts a MARC21 file to MARC21XML.
- `MARC21XML to MARC21`: This converts a MARC21XML file to a MARC21 binary file.
- `MARC to JSON`: This converts a MARC21 file to a JSON file.
- `JSON to MARC`: This converts a JSON file to a MARC21 file.
- `JSON to XML`: This converts a JSON file to XML.
- `XML to JSON`: This converts an XML file to JSON.

The conversions from one encoding standard to another, as in MARC21 to MARC21XML, rely on eXtensible stylesheet transformations, or XSLT. MarcEdit comes with several default stylesheets based on those maintained by the Library of Congress. If you are familiar with XSLT, you can also create your own.

:::::::::::::::::::::::::::::::::::::::::  callout

## Character Encoding

To ensure the integrity of your data you need to select the correct character encoding for your dataset. MarcEdit does not automatically detect character encoding, however, UTF8 is set as the default encoding scheme. You can update the encoding scheme when using the MarcBreaker, or you can update the default in Preferences → MarEditor → Default Encoding. For more information on character encoding and translating from one encoding to another, see [The MarcEdit Field Guide](https://marcedit.reeset.net/learning_marcedit/9-2/dealing-with-character-encodings-in-marcedit/)


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Break a MARC Binary File

Use MarcEdit's "Mark Breaker" to transform the binary MARC data file (`.dat`) into 
the MARC mnemonic "human readable"" format (`.mrk`). 
Expand the elements below for the step-by-step guide.

::: solution

## Transform a MARC binary file for use in the MarcEditor

1. Launch MarcEdit. 
1. In the main window click on the "MARC Tools" icon.
2. In the MARC Tools window, Select Operation → MARCBreaker.
3. In the field, Select Data to Process, click the file folder image to the right of the Open box to browse for the sample MARC data file (.mrc). Double click the found file to select it.
4. Next, you will need save your file in the MARC mnemonic format (.mrk) by clicking the file folder to the right of the Save As box. Select the location and name you would like to give your new file.
5. Under Character encoding select UTF8 as default character encoding.
6. Click execute.
7. Once you click execute the newly created .mrk file will be available to open in the MarcEditor. Under Results at the bottom of the window you will see a count of the records in your file. Click Edit Records to open the .mrk file in the MarcEditor.

**Note:** When you break a binary file and create a new `.mrk` file for editing in the MarcEditor, you are making a copy of your data in a new file format. As a result, any edits you make to the `.mrk` file in the MarcEditor will not automatically be reflected in the original file. We will cover saving and compiling (using the MarcMaker) to create an updated file later on.
::: 

::::::::::::::::::::::::::::::::::::::::::::::::::

## MARC Record layout in the MarcEditor

You should now see the MARC records from the file displaying in the MarcEditor:

![](fig/marc_sample_data.png){alt='MarcEditor screen with file open'}

The MarcEditor displays the records in what is called the 'Mnemonic MARC Text File' format (file extension \*.mrk). Each line in the file represents a field in a MARC record:

```
=245  14$aThe Lord of the Rings /$c J.R.R. Tolkien.
```

This example breaks down as follows:

<table>
  <tr>   <td><code>=</code>   </td>   <td>Each line/field starts with the '=' sign.
   </td>
  </tr>
  <tr>   <td><code>245</code>   </td>   <td>The '=' is followed immediately by the three character MARC field code.
   </td>
  </tr>
  <tr>   <td><code>[two spaces]</code>   </td>   <td>The MARC field is always followed by two spaces.
   </td>
  </tr>
  <tr>   <td><code>14</code>   </td>   <td>The field indicators follow the spaces if the field has indicators. When an indicator is not coded a <code>\\</code> is used. For the control or fixed fields where no indicators are used, the field content starts directly after the spaces.
   </td>
  </tr>
  <tr>   <td><code>\$aThe Lord of the Rings /\$c J.R.R. Tolkien.</code>   </td>   <td>The field content contains the subfields (indicated using the <code>\$</code> symbol) and the text. Because the subfields use the <code>\$</code> symbol, any real occurrences of the dollar symbol (e.g. for currency) is shown as <code>[dollar]</code> instead. Unlike in some cataloguing applications, there are no spaces between subfield codes and the subfield text.
   </td>
  </tr>
</table>

Records in the MarcEditor display are separated by a blank line.

:::::::::::::::::::::::::::::::::::::::::  callout

## MARC syntax in the MarcEditor

Understanding the layout of MARC data in the MarcEditor is key to using the program's tools successfully. For instance, in some tools it is important to specify a field's indicators directly preceeding the first subfield. Throughout this workshop we will highlight how different tools rely on this syntax to apply edits. 


::::::::::::::::::::::::::::::::::::::::::::::::::

The MarcEditor divides a file of MARC records into 'pages' of 100 records. You can scroll up and down the page of MARC records using the scroll bar as usual, but to see the next 100 records you need to use the Next/Previous page controls which are at the bottom left of the screen. The MarcEditor can handle very large files of MARC records, because it never tries to load all the records at the same time.

## Setting MarcEditor Preferences

You can adjust the number of records displayed per 'page' through the MarcEditor preferences which can be accessed through the Edit → Preferences menu option from the MarcEditor, or through the 'Settings' icon on the opening screen of MarcEdit.

Within the MarcEditor preferences you can adjust the font and font size within the MarcEditor. You can also set your character encoding defaults. If you navigate to File Associations within the Preferences window, you can select Associate (`*.mrc`) files with the MarcBreaker and Associate (`*.mrk`) files with the MarcEditor. Setting these file associations will make it easy to break `.mrc` files and edit `.mrk` files.

If you change your preferences for the MarcEditor, the tool used to work with MARC data, you can always go back to the default settings.

:::::::::::::::::::::::::::::::::::::::  checklist

## Reset settings for the MarcEditor in Preferences

1. Click Edit → Preferences
2. Select "MarcEditor" in the Preferences window in the left hand pane
3. In the right hand pane, select Set Defaults for either font or font size
4. Click Ok
  

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- MARC files may be encoded in a variety of formats and text encodings
- MarcEdit can work with many of these differing formats
- The MARC Tools Icon allows you to convert data from one file format to another
- The MarcEditor works with a MarcEdit specific mnemonic format of MARC records (.mrk)
- It is necessary to break a MARC binary file to work with that MARC data in the MarcEditor. The extension of these readable MARC files is `.mrk` rather than `.mrc`
- Understanding the format and syntax of the MARC mnemonic format is key to working with MarcEdit

::::::::::::::::::::::::::::::::::::::::::::::::::


