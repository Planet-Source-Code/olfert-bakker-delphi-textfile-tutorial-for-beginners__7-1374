<div align="center">

## Delphi TextFile tutorial for beginners


</div>

### Description

This article is for those Delphi beginners out there who wish to learn a little bit about the basics of Delphi TextFile Management. I remember having lots of trouble with it when I was new to Delphi, so I figured I might as well help the 'freshmen' getting this done!
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Olfert Bakker](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/olfert-bakker.md)
**Level**          |Beginner
**User Rating**    |3.0 (15 globes from 5 users)
**Compatibility**  |Delphi 7, Delphi 6, Delphi 5
**Category**       |[Files/ File Controls/ Input/ Output](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files-file-controls-input-output__7-3.md)
**World**          |[Delphi](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/delphi.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/olfert-bakker-delphi-textfile-tutorial-for-beginners__7-1374/archive/master.zip)





### Source Code

```
Right. Well, as I explained in the purpose section, this file is meant for beginners who want to learn about text file management and routines, so, if you're an experienced Delphi programmer, you might just want to skip this tutorial, for you'll probably know this by heart.
In Delphi, there are many ways of handling files of several types. Among those are, of course, default types, such as .txt and .ini files, however it is also possible to create your own file types. Because Delphi is based upon the old Pascal language, there are many different standart functions and procedures related to file manipulation and handling, so it's rather easy to get confused. In this tutorial, I'll explain the default ways for handling simple textfiles (.txt), using the various Delhi 5(or higher) methods. I will not, however, do a lot of explaining about file types and specific type-handling. (Of course, if you'd like me to write an article on that too, feel free to mail me and I'll see what I can do for you...)
Before you start this tutorial, I am assuming that you have a basic knowledge of Borland Delphi 5 or higher and that you know how to use Delphi.
First a little info on file handling in general:
Files are, of course, nothing more than a lot of binary data, stored on a physical drive (usually).
Files can be treated like any other object, except that files are always external, and cannot be included in you programs' code. Files can be created, modified and deleted through code at run time.
First you will need a file, so let's write a program that creates a file. For this program all you need is a Form, an Edit Box and a button. You might want to call the button 'Save' or something, with the button's 'Caption' property, and the default text of the editbox you might want to change to 'C:\test.txt' or alike.
Assuming the form = form1, the editbox is Edit1 and the button is button1, you'll have to use the following code:
procedure TForm1.Button1Click(Sender: TObject);
var
  F: TextFile; //Declare a file variable
  S: String;  //Declare a string variable
begin
  S := Edit1.Text;
  AssignFile(F, S);
  Rewrite(F);
  CloseFile(F);
end;
This code simply assigns (the standard Delphi procedure AssignFile) file F, a texfile, located at path S, a string controlled by the editbox, and creates (the standard Delphi procedure Rewrite, which can be used to either create a new file F, or to overwrite an existing file F) a file. Then it frees the instance of the TextFile variable F, by using the standart Delphi procedure CloseFile, which closes a file and frees any instances of it at runtime. You have now created an empty file whith the name C:\test.txt (or another name, depending on the path you entered in the editbox).
Upon opening the file, you'll see that there is no text in the file. We can put text in the file with the standard Delphi procedure WriteLN (this procedure is for TextFile type files ONLY! Do not use it if you're using a different filetype, or you'll get an I/O error.), which enables you to write a line of text, stored in a string type variable, to the file. Limitations of the string type apply, so our line can only contain 255 characters. The WriteLN procedure, obviously, envokes a manipulation of our file. This means that the file must be open for manipulation before we can use the WriteLN procedure, so we'll put it between the Rewrite procedure and the CloseFile procedure, like this:
  Rewrite(F);
  WriteLN(F, S);
  CloseFile(F);
If we run the code now, and open the file in a text-editor afterwards, the file will contain a single line: I'ts own name and path. of course, if we have to open the file in a separate editor, our creation would be rather a useless program, so let's add one button and one editbox, button2 and edit2 (Let's name the button 'Load' and leave the edit's text blank.), and use the following code for the buttons OnClick event:
procedure TForm1.Button2Click(Sender: TObject);
var
  F: TextFile;
  S: String;
begin
  AssignFile(F, Edit1.Text);
  Reset(F);
  ReadLN(F, S);
  CloseFile(F);
  Edit2.Text := S;
end;
Now, upon running the program, if we press the 'Save' button first and then press the 'Load' Button, you'll see that the second editbox will contain the same information as the first one.
This is because you have just reopened the file (with the standard Delphi procedure Reset, which opens a an assigned file F and places the pointer at the beginning of the file) and read the first line (with the standard Delphi procedure ReadLN, which reads the a line in a TextFile F, beginning at the pointer and ending at the EOLN (End Of LiNe) mark). Then we put this line S into the editbox Edit2.
Now, you might not always want to begin a new file, so, to add text to an existing file, you can use the standard Delphi procedure Append, which opens an assigned file F and places the pointer at the beginning of an new line at the end of the file (EOF), like this:
  Append(F);
Now, if you use the WriteLN procedure, you’ll be able to add lines to the file as you please. Using iterations, it should be easy now to create normal, unformatted textfiles and manipulating them.
Basically, this pretty much covers the default functions of Delphi for file manipulation in TextFiles. I’ll be writing a tutorial on typed and untyped files soon, but I’m pretty busy at the moment, so it may be a while before it appears. I hope this helped you out a bit.
If you have any comments, mail them to inet@mcblade.fol.nl.
```

