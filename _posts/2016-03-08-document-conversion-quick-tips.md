---
layout: post
title: Some Quick Ideas for Document Conversion
---

I just love using LaTeX. It takes a while to learn, but once used to it, it's just so much quicker to fire up a console and write something down into a clean text-only interface. That being said, 90% of the documents I get from others at my job are MS Word files, either .doc or .docx. Some colleagues even prefer I send them those files instead of plain text files or PDFs, so I just do them the favour. However, opening up LibreOffice just to write down one page of barely formatted text just seems so nonsensical. You can see how the difference in preference between others and me can be very annoying, so here are some automated ways of dealing with this.

Software required for these scripts:
* LibreOffice
* pandoc

## 1. Using my PDF viewer to quickly look at office files

Starting LibreOffice just to view a single file annoys me, as it takes a bit of time and also distracts while reading, as it gives me too much interface I don't need at the time. So I've written a script that will just convert the file on the fly into a PDF and start Atril, my PDF viewer, to show it. This uses LibreOFfice in headless mode to convert the file, which for some reason won't work when you have any instance of normal LibreOffice open. Coincidentally, it even won't give you an error message, so keep that in mind when testing: close all instances of LibreOFfice first!

{% highlight js %}
#!/bin/bash

soffice --headless --convert-to pdf:"writer_pdf_Export" "$1" && 
atril "${1%%.*}".pdf &&
rm "${1%%.*}".pdf
{% endhighlight %}

This script will

1. Convert any file LibreOffice can read into PDF
2. Open that PDF in Atril (substitute this command with your PDF reader of choice)
The magic regular expression there tells Atril to open a file with the same basname as the original file, but with .pdf as the extension.
3. Delete the PDF file once you close the window of the PDF viewer, but leave the original file intact.

All I need to do then is save the script (I chose the name **viewaspdf**), make this script executable, 

{% highlight js %}
chmod +x viewaspdf
{% endhighlight %}

and put into a directory where my system will see it as an executable (**~/.bin** or **/usr/local/bin**), as well as tell my file manager (in my case Thunar) to always open PDFs with this programme.

But wait, you'll say, how did I know that the soffice command takes the value

{% highlight js %}
pdf:"writer_pdf_Export"
{% endhighlight %}

to convert documents to PDF? I just looked it up on <a href="https://cgit.freedesktop.org/libreoffice/core/tree/filter/source/config/fragments/filters"> this page</a> (also bookmark it, we'll need it later). Just click on the desired format and note the value under **<node oor:name** that is in "".

## 2. Quickly read that MS Word file on your command line

I have to cringe every time I get a simple text document not as plain text, but as an MS Word file. Ugh! But thanks to open source software, I can just write a viewer for the command line.

{% highlight js %}
#!/bin/bash

if [ $# -eq 0 ]
  then
    echo "\n\nNo filename supplied... \n\n"
  else
    soffice --headless --convert-to txt:"Text" "$1" &&
    less "${1%%.*}".txt &&
    rm "${1%%.*}".txt
fi

exit
{% endhighlight %}

This will

1. See whether a file is supplied with a simple if loop (which is handy if you're on a console and the filename doesn't exist). It will warn you if there is no file.
2. Otherwise it will convert the file to plain text (with the filter information provided by the link above again) 
3. view it with less (or you can provide an editor like nano, vim,...)
4. Once you exit less, it will just delete the text file.

I call the script **docless**.

## 3. Convert a LaTeX file to MS Word

I just hate it when I use LaTeX to write something and the person proofreading it won't accept a PDF since they are used to inserting comments into a .doc file. Well, this method sadly won't make .doc files with perfect layout and all that, but it will at least give the person the entire content without you having to manually copy/paste the whole thing into LibreOffice or something. This script requires **pandoc**.

#!/bin/bash
{% highlight js %}
printf "\n\n Converting LaTeX document to M$ Word... \n\n"

if [ $# -eq 0 ]
  then
    echo "\n\nNo filename supplied... \n\n"
  else
    pandoc -s $1 -o temp-latex2doc.odt
    soffice --headless --convert-to docx:"MS Word 2007 XML" temp-latex2doc.odt
    mv temp-latex2doc.docx "${1%%.*}".docx
    rm temp-latex2doc.odt
    printf "\nDone!\n\n"
fi

exit
{% endhighlight %}

This will

1. use pandoc to convert the LaTeX script into an odt (LibreOffice) file
2. use LibreOffice to convert the odt file to MS Word
3. remove the temporary odt file

This really isn't all that great for LaTeX code with complex layouts, but it's great for simple essays or text-heavy stuff.

I hope this has been useful for some of you. Let me know if you'd like more articles like these.

