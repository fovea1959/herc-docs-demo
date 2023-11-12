####################################
Appendix A - Documentation Standards
####################################

The Hercules documents are written in reStructuredText.

This appendix details the reStructuredText standards to be adhered to when creating or editing documentation, in order to achieve a consistent presentation of documenation across many contributors, and over time.

reStructuredText (RST) is a lightweight plaintext markup language, which is simple and human-readable in its raw form.
It allows for easy conversion to other formats, such as PDF, HTML or EPUB.
Read more on reStructuredText `here <https://en.wikipedia.org/wiki/ReStructuredText>`_ .

This document is not intended to be a guide on RST - a basic familiarity with RST should be gained prior to working on documentation.

*****************
Sections
*****************

One of the first and most basic standards any documenter will need to know is that of Sections, used to establish a heirarchy, and build a table of contents.
There is no definitive standard in place, however we will adopt the below standards, commonly used with Python documentation.

.. note::
The number of punctuation characters should match the length of the section name.

Standards
=========

**Top level 'part'**
::
  ######
  Part 1
  ######
Surround the name by over- and underlining using `#` symbols.

**2nd level 'chapter'**
::
  *********
  Chapter 1
  *********
Surround the name by over- and underlining using `*` symbols.

**3rd level 'section'**
::
  Section 1
  =========
Underlining using `=` symbols.

**4th level 'subsection'**
::
  Subsection 1
  ------------
Underlining using `-` symbols.

**5th level 'subsection'**
::
  Subsection 1
  ^^^^^^^^^^^^
Underlining using `^` symbols.

Examples
========

The first example:
::
  ######################
  Hercules Document Name
  ######################

  ****************
  1st Chapter Name
  ****************
  
  Section 1
  =========
  
  1st Subsection
  --------------
  
  2nd Subsection
  --------------
  
  1st subsubsection
  ^^^^^^^^^^^^^^^^^
  
  Section 2
  =========

...would result in the following structure in the left hand TOC panel of the generated HTML:

.. image:: /doc_resources/images/appendix_a_tocsamp.png


*****************
Images
*****************

Occassionaly it is neccessary to include images in the documentation, such as screenshots.
When this is required, the below standards should be applied.

Standards
=========

* Any images files to be included in the documents should be placed in the /doc_resources/images/ folder.
* image files should be named as follows:

Examples
========
/doc_resources/images/configuration_scnshot1.jpg
/doc_resources/images/configuration_exampleb.jpg
