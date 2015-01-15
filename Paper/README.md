# Paper Source Code

## Building the document

This thesis was written in LaTeX to be processed by pdflatex to produce a .pdf file directly.  The LaTeX source was mostly tested with the MikTeX ditribution of LaTeX, but the sourced should be buildable with TeXlive as well.  The command for building the pdf file is:

`/Path/To/pdflatex(.exe) outline.tex`

After the first pass on outline.tex and if the bibliographic references change, the BibTeX references should be built using the following command:

`/Path/To/bibtex(.exe) outline.aux`

Up to two more passes of running pdflatex may be needed to resolve all references in the final document.  Subsequently, if no changes are made that would change the table of contents, figure numbers, bibliographic refereces, etc., only one pass of pdflatex may be necessary to include changes in the final document.

## Organization

Main source document: outline.tex

The main document includes additional .tex source documents using the `\input{Relative/Path/To/*file*.tex}`  The relative path base directory is the directory of the main source document. Beware that if you include any files in other source documents (figures, other tex documents, etc.), the relative path base directory is the same as the main source document, not the called document.

Figures produced by GNU Octave are included with the `\input{*filename*.tex}` command, and because those files include a .pdf figure, those are left is the same directory as the main source document. Other figures are included in the ./figures directory and are included using the `\includegraphics{./figures/*file*}` command.  It is not necessary to inlude the file extension for pdf figures when processing the source with pdflatex.  pdflatex will automatically include the pdf file that begins with `*file*`.  Processing the source with latex will automatically include the eps file that begins with `*file*`

Most of the text of the paper is included is separate .tex files under the *sections* directory.  Remember that figures and files included in those files are referenced using the main source document's directory as the base directory.

## GNU Octave output

Graphs were developed using GNU Octave with GNUPlot not FLTK as the plotting backend.  The TeX output was produced using the following command in Octave:

`print(*figure handle*,*filename.tex*,'-dtex')`

(The device '-dpdflatex' was not used because it only works with the FLTK graphics toolkit)

The result is a TeX file that can be included in the LaTeX document along with a .eps that the .tex file references.  pdflatex cannot include .eps figures, so the utility epstopdf was used to convert the .eps file produced by Octave in to a .pdf figure.  The following command will accomplish the conversion:

`/Path/To/epstopdf(.exe) *filename*.eps`

## Helpful commands when editing .tex files in Notepad++

It is useful to create shortcuts in [Notepad++](http://notepad-plus-plus.org/) to process tex files while editing the documents.  The following commands were adapted from [Troy Henderson](http://www.tlhiv.org/ma497/software/):

Run pdfLaTeX:
`cmd /c cd /d "$(CURRENT_DIRECTORY)" && X:\Path\to\pdflatex.exe -shell-escape "$(FILE_NAME)" && pause`

Run BibTeX:
`cmd /c cd /d "$(CURRENT_DIRECTORY)" && X:\Path\to\bibtex.exe "$(NAME_PART).aux" && pause`

Open pdf in SumatraPDF:
`"X:\Path\to\SumatraPDF.exe" "$(CURRENT_DIRECTORY)\$(NAME_PART).pdf"`


