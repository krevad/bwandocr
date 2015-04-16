# B/W and OCR it
This Automator app will strip the colors from a scanned PDF and then OCR it with PDFPen.
The converison to black and white will remove some unwanted artifacts from the scanning such as dust and wrinkles while greatly reduce file size.

**Note!** This script will replace the original file. Use it with duplicates until you are confident with how it works.

## Prerequisites
* A recent version of Mac OS X.
* PDFpen or PDFpenPro by [Smile Software](http://www.smilesoftware.com/PDFpen/). PDFPen uses the OmniPage OCR engine which is pretty good, often much better than the free software that came with your scanner. 

## Create the Automator application
Launch Automator, choose to create an *Application*.

The application consists of two actions:

1. Apply Quartz Filter to PDF Documents
2. Run AppleScript

Add these actions right away.

### Apply Quartz Filter to PDF Documents
Use the *Black & White* filter.

### Run AppleScript
If you use PDFpenPro, you need to edit the *tell application*-command below. 

Cut and paste this code snippet into the action's code area:
```
on run {input, parameters}	tell application "PDFpen"		open input		set theDoc to document 1		tell theDoc			if needs ocr of theDoc then				ocr theDoc				repeat while performing ocr of theDoc					delay 1				end repeat				delay 1				close with saving			end if		end tell	end tell	return inputend run
```

## Use
Save your new application and drop your PDF:s on its icon.

## Inspiration

[Padraic Renaghan's *pdfpenocr.scpt*](https://gist.github.com/prenagha/1355037)
