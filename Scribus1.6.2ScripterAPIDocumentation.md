## Document related Commands 

closeDoc(...)

closeDoc() 

Closes the current document without prompting to save.

May throw [NoDocOpenError](#NoDocOpenError) if there is no document to close 

docChanged(...)

docChanged(bool) 

Enable/disable save icon in the Scribus icon bar and the Save menu item. It's useful to call this procedure when you're changing the document, because Scribus won't automatically notice when you change the document using a script. 

getDocName(...)

getDocName() -> string 

Returns the name of current file 

getUnit(...)

getUnit() -> integer (Scribus unit constant) 

Returns the measurement units of the document. The returned value will be one of the UNIT_* constants: UNIT_INCHES, UNIT_MILLIMETERS, UNIT_PICAS, UNIT_POINTS.

Typically you may use this command so that you can change the measurement units to something else, for which you are creating or modifying objects based some particular units, like points, after which you want to return to whatever the original units were.

original = getUnit()

*do some operations...then later*

setUnit(original) 

haveDoc(...)

haveDoc() -> bool 

Returns true if there is a document open. Since this returns a boolean, typically this will be used in a conditional clause:

if haveDoc():

so that you can deal with the situation where no document exists with an else: clause. 

loadStylesFromFile(...)

loadStylesFromFile("filename") 

Loads paragraph styles from the Scribus document at "filename" into the current document. 

masterPageNames(...)

masterPageNames() 

Returns a list of the names of all master pages in the document. 

newDoc(...)

newDoc(size, margins, orientation, firstPageNumber, unit, facingPages, firstSideLeft) -> bool 

WARNING: Obsolete procedure! Use [newDocument](#-newDocument) instead. Also note that this commands requires 7 parameters, whereas the preferred newDocument() command requires 8.

Creates a new document and returns true if successful. The parameters have the following meaning:

- size = A tuple (width, height) describing the size of the document. You can use predefined constants named PAPER_<paper_type> e.g. PAPER_A4 etc. 
- margins = A tuple (left, right, top, bottom) describing the document margins 
- orientation = the page orientation - constants PORTRAIT, LANDSCAPE 
- firstPageNumber = is the number of the first page in the document used for page numbering. While you'll usually want 1, it's useful to have higher numbers if you're creating a document in several parts. 
- unit: this value sets the measurement units used by the document. Use a predefined constant for this, one of: UNIT_INCHES, UNIT_MILLIMETERS, UNIT_PICAS, UNIT_POINTS. 
- facingPages = FACINGPAGES, NOFACINGPAGES 
- firstSideLeft = FIRSTPAGELEFT, FIRSTPAGERIGHT 

The values for width, height and the margins are expressed in the given unit for the document. PAPER_* constants are a series of tuples specific to the document size, with the values corresponding to points. Therefore, if you are creating a document and using UNIT_MILLIMETERS for example, DO NOT USE the PAPER_* constants. A workaround can be to use the PAPER_* constant along with UNIT_POINTS, then follow the command with another command, setUnit(UNIT_MILLIMETERS).

example: [newDoc](#-newDoc)(PAPER_A4, (10, 10, 20, 20), LANDSCAPE, 1, UNIT_POINTS, FACINGPAGES, FIRSTPAGERIGHT) 

newDocument(...)

newDocument(size, margins, orientation, firstPageNumber, unit, pagesType, firstPageOrder, numPages) -> bool 

Note that this commands requires 8 parameters, whereas the obsolete newDoc() command required 7. The additional parameter indicates how many pages to create.

Creates a new document and returns true if successful. The parameters have the following meaning: 

- size = A tuple (width, height) describing the size of the document. You can use predefined constants named PAPER_<paper_type> e.g. PAPER_A4 etc.
- margins = A tuple (left, right, top, bottom) describing the document margins
- orientation = the page orientation - constants PORTRAIT, LANDSCAPE
- firstPageNumer = is the number of the first page in the document used for pagenumbering. While you'll usually want 1, it's useful to have higher numbers if you're creating a document in several parts.
- unit: this value sets the measurement units used by the document. Use a predefined constant for this, one of: UNIT_INCHES, UNIT_MILLIMETERS, UNIT_PICAS, UNIT_POINTS.
- pagesType = One of the predefined constants PAGE_n. PAGE_1 is single page, PAGE_2 is for double sided documents, PAGE_3 is for 3 pages fold and PAGE_4 is 4-fold.
- firstPageOrder = What is position of first page in the document. Indexed from 0 (0 = first).
- numPage = Number of pages to be created.

The values for width, height and the margins are expressed in the given unit for the document. PAPER_* constants are a series of tuples specific to the document size, with the values corresponding to points. Therefore, if you are creating a document and using UNIT_MILLIMETERS for example, DO NOT USE the PAPER_* constants.

For A and B paper formats there are now new constants to use with UNIT_MILLIMETERS, named for example, PAPER_A4_MM, or PAPER_B6_MM.

Examples:

newDocument(PAPER_A4, (10, 10, 20, 20), LANDSCAPE, 7, UNIT_POINTS, PAGE_4, 3, 1)

newDocument(PAPER_A4_MM, (10, 10, 20, 20), LANDSCAPE, 7, UNIT_MILLIMETERS, PAGE_4, 3, 1)

May raise ScribusError if is firstPageOrder bigger than allowed by pagesType. 

openDoc(...)

openDoc("name") 

Opens the document "name".

May raise ScribusError if the document could not be opened. 

placeEPS(...)

placeEPS("filename", x, y) 

Places the EPS "filename" onto the current page, x and y specify the coordinate of the topleft corner of the EPS placed on the page.

If loading was successful, the selection contains the imported EPS. 

placeODG(...)

placeODG("filename", x, y) 

Places the ODG "filename" onto the current page, x and y specify the coordinate of the topleft corner of the ODG placed on the page.

If loading was successful, the selection contains the imported ODG. 

placeSVG(...)

placeSVG("filename", x, y) 

Places the SVG "filename" onto the current page, x and y specify the coordinate of the topleft corner of the SVG placed on the page.

If loading was successful, the selection contains the imported SVG. 

placeSXD(...)

placeSXD("filename", x, y) 

Places the SXD "filename" onto the current page, x and y specify the coordinate of the topleft corner of the SXD placed on the page.

If loading was successful, the selection contains the imported SXD. 

placeVectorFile(...)

placeVectorFile("filename", x, y) 

Places the vector graphics "filename" onto the current page, x and y specify the coordinate of the topleft corner of the graphic placed on the page.

If loading was successful, the selection contains the imported graphic. 

revertDoc(...)

revertDoc() 

Revert the current document to its last saved state. 

saveDoc(...)

saveDoc() 

Saves the current document with its current name, returns true if successful. If the document has not already been saved, this may bring up an interactive save file dialog. If the save fails, there is currently no way to tell. 

saveDocAs(...)

saveDocAs("name") 

Saves the current document under the new name "name" (which may be a full or relative path).

May raise ScribusError if the save fails. 

setBaseLine(...)

setBaseLine(grid, offset) 

Sets the base line settings of the document, grid spacing(grid), grid offset(offset). Values are given in the measurement units of the document - see UNIT_<type> constants. 

setBleeds(...)

setBleeds(lr, rr, tr, br) 

Sets the bleeds of the document. Left(lr), Right(rr), Top(tr) and Bottom(br) bleeds are given in the measurement units of the document - see UNIT_<type> constants. 

setDocType(...)

setDocType(facingPages, firstPageLeft) 

Sets the document type. To get facing pages set the first parameter to FACINGPAGES, to switch facingPages off use NOFACINGPAGES instead. If you want to be the first page a left side set the second parameter to FIRSTPAGELEFT, for a right page use FIRSTPAGERIGHT. 

setInfo(...)

setInfo("author", "info", "description") -> bool 

Sets the document information. "Author", "Info", "Description" are strings. 

setMargins(...)

setMargins(lr, rr, tr, br) 

Sets the margins of the document, Left(lr), Right(rr), Top(tr) and Bottom(br) margins are given in the measurement units of the document - see UNIT_<type> constants. 

setUnit(...)

setUnit(type) 

Changes the measurement unit of the document. Possible values for "unit" are defined as constants UNIT_<type>.

May raise ValueError if an invalid unit is passed.

As noted above, typically you may use this command so that you can change the measurement units to something else, for which you are creating or modifying objects based some particular units, like points, after which you want to return to whatever the original units were.

original = getUnit()

*do some operations...then later*

setUnit(original) 

scrollDocument(...)

scrollDocument(x,y) 

Scroll the document in main GUI window by x and y. 

zoomDocument(...)

zoomDocument(double) 

Zoom the document in main GUI window. Actions have whole number values like 20.0, 100.0, etc. Zoom to Fit uses -100 as a marker. 

## Page related Commands 

applyMasterPage(...)

applyMasterPage(masterPageName, pageNr) 

Applies the named master page to the indicated page. Some examples of usage are on the wiki.. 

closeMasterPage(...)

closeMasterPage() 

Closes the currently active master page, if any, and returns editing to normal. Begin editing with [editMasterPage()](#-editMasterPage). 

createMasterPage(...)

createMasterPage(pageName) 

Creates a new master page named pageName. Begin editing with [editMasterPage()](#-editMasterPage). 

currentPage(...)

currentPage() -> integer 

Returns the number of the current working page. Page numbers are counted from 1 upwards, no matter what the displayed first page number of your document is.

If you want to enter into a text frame the special character for the current page number, it is decimal 30 or hex 0x1e. For example, either of the following would be equivalent:

scribus.setText('Page ' + chr(30), textframe)

scribus.setText('Page \x1e', textframe)

See also pageCount() 

deleteMasterPage(...)

deleteMasterPage(pageName) 

Delete the named master page. 

deletePage(...)

deletePage(nr) 

Deletes the given page. Does nothing if the document contains only one page. Page numbers are counted from 1 upwards, no matter what the displayed first page number is.

May raise IndexError if the page number is out of range 

editMasterPage(...)

editMasterPage(pageName) 

Enables master page editing and opens the named master page for editing. Finish editing with [closeMasterPage()](#-closeMasterPage). 

getAllObjects(...)

getAllObjects([type, page, "layer"]) -> list 

Returns a list containing the names of all objects of specified type and located on specified page and/or layer.

This function accepts several optional keyword arguments: 

- type (optional): integer corresponding to item type, by default all items will be returned. You can use one of the ITEMTYPE_* constants.
- page (optional): index of page on which returned objects are located, by default the current page. The page index starts at 0 and goes to the total number of pages - 1.
- "layer" (optional): name of layer on which returned objects are located, by default the function returns items located on all layers.

May throw ValueError if page index or layer name is invalid. 

getHGuides(...)

getHGuides() -> list 

Returns a list containing positions of the horizontal guides. Values are in the document's current units - see UNIT_<type> constants. 

getMasterPage(...)

getMasterPage(nr) -> string 

Returns the name of master page applied to page "nr".

May raise IndexError if the page number is out of range. 

getPageType(...)

getPageType() -> integer 

Returns the type of the Page, 0 means left Page, 1 is a middle Page and 2 is a right Page 

getPageItems(...)

getPageItems() -> list 

Returns a list of tuples with items on the current page. The tuple is: (name, objectType, order) E.g. [('Text1', 4, 0), ('Image1', 2, 1)] means that object named 'Text1' is a text frame (type 4) and is the first at the page... 

getPageMargins(...)

getPageMargins() 

Returns the document page margins as a (top, left, right, bottom) tuple in the document's current units. See UNIT_<type> constants and [getPageSize](#-getPageSize)(). 

getPageNMargins(...)

getPageNMargins(nr) 

Returns a tuple with a particular page's margins measured in the document's current units. See UNIT_<type> constants and [getPageSize](#-getPageSize)(). 

getPageSize(...)

getPageSize() -> tuple 

Returns a tuple with document page dimensions measured in the document's current units. See UNIT_<type> constants and [getPageMargins](#-getPageMargins)() 

getPageNSize(...)

getPageNSize(nr) -> tuple 

Returns a tuple with a particular page's size measured in the document's current units. See UNIT_<type> constants and [getPageMargins](#-getPageMargins)() 

getVGuides(...)

getVGuides() 

See [getHGuides](#-getHGuides). 

gotoPage(...)

gotoPage(nr) 

Moves to the page "nr" (that is, makes the current page "nr"). Note that gotoPage doesn't (currently) change the page the user's view is displaying, it just sets the page that script commands will operates on.

May raise IndexError if the page number is out of range. 

importPage(...)

importPage("fromDoc", (pageList), [create, importWhere, importWherePage]) 

Imports a set of pages (given as a tuple) from an existing document (the file name must be given). This function maps the "Page->Import" dropdown menu function.

The function accepts following arguments: 

- fromDoc: string; the filename of the document to import pages from
- pageList: tuple; page numbers of pages to import
- create: number; 0 to replace existing pages, 1 (default) to insert new pages
- importWhere: number; used if create==1; 0 to create pages before importWherePage, 1 to create pages after importWherePage, 2 (default) to create pages at the end of the document
- importWherePage: number; used if create==1 and importWhere==0|1; zero-based page number (of the current document) before or after which to import the pages 

newPage(...)

newPage(where [,"masterpage"]) 

Creates a new page. If "where" is -1 the new Page is appended to the document, otherwise the new page is inserted before "where". Page numbers are counted from 1 upwards, no matter what the displayed first page number of your document is. The optional parameter "masterpage" specifies the name of the master page for the new page.

May raise IndexError if the page number is out of range 

pageCount(...)

pageCount() -> integer 

Returns the number of pages in the document.

There is also a special character for page count, in decimal 23, and in hex 0x17. You might combine this with the special character for current page in a text frame (on a Master Page for example) as follows. Either of these is equivalent:

scribus.setText('Page ' + chr(30) + ' of ' + chr(23), textframe)

scribus.setText('Page \x1e of \x17', textframe) 

redrawAll(...)

redrawAll() 

Redraws all pages. 

savePageAsEPS(...)

savePageAsEPS("name") 

Saves the current page as an EPS to the file "name".

May raise ScribusError if the save failed. 

setHGuides(...)

setHGuides(list) 

Sets horizontal guides. Input parameter must be a list of guide positions measured in the current document units - see UNIT_<type> constants.

Example:

setHGuides(getHGuides() + [200.0, 210.0]) # this will add new guides while saving existing guides

setHGuides([90,250]) # this will replace current guides entirely 

setRedraw(...)

setRedraw(bool) 

Disables page redraw when bool = False, otherwise redrawing is enabled. This change will persist even after the script exits, so make sure to call [setRedraw](#-setRedraw)(True) in a finally: clause at the top level of your script. 

setVGuides(...)

setVGuides() 

The usage is analogous to that of [setHGuides](#-setHGuides) for either adding to existing guides or replacing them. 

## Commands for Master Pages

*Please see the comments at the bottom of the page.*

masterPageNames(...)

masterPageNames() 

Returns a list of the names of all master pages in the document. 

applyMasterPage(...)

applyMasterPage(Master Page name, page nr) 

Applies the named master page to the indicated page. Some examples of usage are on the wiki.. 

closeMasterPage(...)

closeMasterPage() 

Closes the currently active master page, if any, and returns editing to normal. Begin editing with [editMasterPage()](#-editMasterPage). 

createMasterPage(...)

createMasterPage(pageName) 

Creates a new master page named pageName. Begin editing with [editMasterPage()](#-editMasterPage). 

deleteMasterPage(...)

deleteMasterPage(pageName) 

Delete the named master page. 

editMasterPage(...)

editMasterPage(pageName) 

Enables master page editing and opens the named master page for editing. Finish editing with [closeMasterPage()](#-closeMasterPage). 

It's important to consider how you may wish to approach working with Master Pages with Scripter. It's conceivable you may want to work with existing Master Pages, in which case you will need a list of them from masterPageNames(), after which you might present these to the user in a dialog so that one can be selected. It's more likely perhaps that you will be creating a Master Page, editing it, then applying it to one or more pages of the Document.

With this latter method, you would first use createMasterPage(), then editMasterPage(). At this point you would proceed as if you were editing any page of the Document you are working on. Once finished, you must then closeMasterPage() to continue. *Note that this command takes no arguments.* You may then wish some time later to applyMasterPage() in whatever fashion you choose, necessarily being careful to only choose valid page numbers – recall that pages are numbered starting with 1.

If you need to continue to edit the Document in some other fashion, it is important to realize that you must select a page to work with, using the gotoPage() command. 

## Creating and Destroying Objects 

createBezierLine(...)

createBezierLine(list, ["name"]) -> string 

Creates a new bezier curve and returns its name. The points for the bezier curve are stored in the list "list" in the following order: [x1, y1, kx1, ky1, x2, y2, kx2, ky2...xn. yn, kxn. kyn] In the points list, x and y mean the x and y coordinates of the point and kx and ky meaning the control point for the curve. The coordinates are given in the current measurement units of the document (see UNIT constants). "name" should be a unique identifier for the object because you need this name for further access to that object. If "name" is not given Scribus will create one for you.

May raise [NameExistsError](scripterapi.html#NameExistsError) if you explicitly pass a name that's already used. May raise ValueError if an insufficient number of points is passed or if the number of values passed don't group into points without leftovers. 

createEllipse(...)

createEllipse(x, y, width, height, ["name"]) -> string 

Creates a new ellipse on the current page and returns its name. The coordinates are given in the current measurement units of the document (see UNIT constants). "name" should be a unique identifier for the object because you need this name for further referencing of that object. If "name" is not given Scribus will create one for you.

May raise [NameExistsError](scripterapi.html#NameExistsError) if you explicitly pass a name that's already used. 

createImage(...)

createImage(x, y, width, height, ["name"]) -> string 

Creates a new picture frame on the current page and returns its name. The coordinates are given in the current measurement units of the document. "name" should be a unique identifier for the object because you need this name for further access to that object. If "name" is not given Scribus will create one for you.

May raise [NameExistsError](scripterapi.html#NameExistsError) if you explicitly pass a name that's already used. 

createLine(...)

createLine(x1, y1, x2, y2, ["name"]) -> string 

Creates a new line from the point(x1, y1) to the point(x2, y2) and returns its name. The coordinates are given in the current measurement unit of the document (see UNIT constants). "name" should be a unique identifier for the object because you need this name for further access to that object. If "name" is not given Scribus will create one for you.

May raise [NameExistsError](scripterapi.html#NameExistsError) if you explicitly pass a name that's already used. 

createPathText(...)

createPathText(x, y, "textbox", "beziercurve", ["name"]) -> string 

Creates a new pathText by merging the two objects "textbox" and "beziercurve" and returns its name. The coordinates are given in the current measurement unit of the document (see UNIT constants). "name" should be a unique identifier for the object because you need this name for further access to that object. If "name" is not given Scribus will create one for you.

May raise [NameExistsError](scripterapi.html#NameExistsError) if you explicitly pass a name that's already used. May raise [NotFoundError](scripterapi.html#NotFoundError) if one or both of the named base object don't exist. 

createPolyLine(...)

createPolyLine(list, ["name"]) -> string 

Creates a new polyline and returns its name. The points for the polyline are stored in the list "list" in the following order: [x1, y1, x2, y2...xn. yn]. The coordinates are given in the current measurement units of the document (see UNIT constants). "name" should be a unique identifier for the object because you need this name for further access to that object. If "name" is not given Scribus will create one for you.

May raise [NameExistsError](scripterapi.html#NameExistsError) if you explicitly pass a name that's already used. May raise ValueError if an insufficient number of points is passed or if the number of values passed don't group into points without leftovers. 

createPolygon(...)

createPolygon(list, ["name"]) -> string 

Creates a new polygon and returns its name. The points for the polygon are stored in the list "list" in the following order: [x1, y1, x2, y2...xn. yn]. At least three points are required. There is no need to repeat the first point to close the polygon. The polygon is automatically closed by connecting the first and the last point. The coordinates are given in the current measurement units of the document (see UNIT constants). "name" should be a unique identifier for the object because you need this name for further access to that object. If "name" is not given Scribus will create one for you.

May raise [NameExistsError](scripterapi.html#NameExistsError) if you explicitly pass a name that's already used. May raise ValueError if an insufficient number of points is passed or if the number of values passed don't group into points without leftovers. 

createRect(...)

createRect(x, y, width, height, ["name"]) -> string 

Creates a new rectangle on the current page and returns its name. The coordinates are given in the current measurement units of the document (see UNIT constants). "name" should be a unique identifier for the object because you need this name to reference that object in future. If "name" is not given Scribus will create one for you.

May raise [NameExistsError](scripterapi.html#NameExistsError) if you explicitly pass a name that's already used. 

createText(...)

createText(x, y, width, height, ["name"]) -> string 

Creates a new text frame on the actual page and returns its name. The coordinates are given in the actual measurement unit of the document (see UNIT constants). "name" should be a unique identifier for the object because you need this name for further referencing of that object. If "name" is not given Scribus will create one for you.

May raise [NameExistsError](scripterapi.html#NameExistsError) if you explicitly pass a name that's already used. 

deleteObject(...)

deleteObject(["name"]) 

Deletes the item with the name "name". If "name" is not given the currently selected item is deleted. 

objectExists(...)

objectExists(["name"]) -> bool 

Test if an object with specified name really exists in the document. The optional parameter is the object name. When no object name is given, returns True if there is something selected. 

## Selecting Objects 

deselectAll(...)

deselectAll() 

Deselects all objects in the whole document. 

getSelectedObject(...)

getSelectedObject([nr]) -> string 

Returns the name of the selected object. "nr" if given indicates the number of the selected object, e.g. 0 means the first selected object, 1 means the second selected Object and so on. 

moveSelectionToBack(...)

moveSelectionToBack() 

Moves the current selection to the back. 

moveSelectionToFront(...)

moveSelectionToFront() 

Moves the current selection to the front. 

selectionCount(...)

selectionCount() -> integer 

Returns the number of selected objects. 

selectObject(...)

selectObject("name") 

Adds the object with the given "name" to the current selection.

Lots of scripter function use the concept of "currently selected item" if an object name is not provided. In the case of multiple selections, the currently selected item is always the first item in the selection. As a consequence if you are planning to use object "name" as the currently selected item for following operations and current selection is not empty, you should call deselectAll() before calling this function.

If what you wish to do is to paste a copy of the object to another page, you must first copyObject(), then pasteObject(). See Manipulating Objects. 

## Setting Object Properties 

loadImage(...)

loadImage("filename" [, "name"]) 

Loads the picture "picture" into the image frame "name". If "name" is not given the currently selected item is used.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError) if the target frame is not an image frame 

outlineText(...)

outlineText(["name"]) 

Convert the text frame "name" to outlines. If "name" is not given the currently selected item is used. 

scaleImage(...)

scaleImage(x, y [, "name"]) 

Do not use this command since it no longer works. Use setImageScale instead. 

setCornerRadius(...)

setCornerRadius(radius, ["name"]) 

Sets the corner radius of the object "name". The radius is expressed in points regardless of page units, and must be an integer. If "name" is not given the currently selected item is used. 

May raise ValueError if the corner radius is negative. 

setCustomLineStyle(...)

setCustomLineStyle(styleName, ["name"]) 

Sets the custom line style of the object "name" to "styleName". Argument "styleName" is the name of line style as seen in Style Manager. If "name" is not given the currently selected item is used. 

setFillBlendmode(...)

setFillBlendmode(blendmode, ["name"]) 

Sets the fill blendmode of the object "name" to blendmode. If "name" is not given the currently selected item is used. 

setFillColor(...)

setFillColor("color", ["name"]) 

Sets the fill color of the object "name" to the color "color". "color" is the name of one of the defined colors. If "name" is not given the currently selected item is used. 

setFillShade(...)

setFillShade(shade, ["name"]) 

Sets the shading of the fill color of the object "name" to "shade". "shade" must be an integer value in the range from 0 (lightest) to 100 (full Color intensity). If "name" is not given the currently selected Item is used.

May raise ValueError if the fill shade is out of bounds. 

setFillTransparency(...)

setFillTransparency(transparency, ["name"]) 

Sets the fill transparency of the object "name". If "name" is not given the currently selected item is used.

In spite of this command's wording, the "transparency" value is actually a decimal corresponding to the opacity, so for example, 0.9 = 90% opacity, 0.2 = 20% opacity. 

setGradientFill(...)

setGradientFill(type, "color1", shade1, "color2", shade2, ["name"]) 

Sets the gradient fill of the object "name" to type. Color descriptions are the same as for [setFillColor](#-setFillColor)() and [setFillShade](#-setFillShade)(). See the constants for available types (FILL_<type>). 

setGradientStop(...)

setGradientStop("color", shade, opacity, ramppoint, ["name"]) 

Set or add a gradient stop to the gradient fill of the object \"name\" at position ramppoint. Color descriptions are the same as for [setFillColor](#-setFillColor)() and [setFillShade](#-setFillShade)(). setGradientFill() must have been called previously for the gradient fill to be visible. 

setImageScale(...)

setImageScale(x, y [, "name"]) 

Sets the scaling factors of the picture in the image frame "name". If "name" is not given the currently selected item is used. A number of 1 means 100 %. Scaling factors are equal to the values shown on properties palette.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError) if the target frame is not an image frame 

setImageOffset(...)

setImageOffset(x, y [, "name"]) 

Sets the position of the picture in the image frame "name". If "name" is not given the currently selected item is used. The specified offset values are equal to the values shown on properties palette when point unit is used.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError) if the target frame is not an image frame 

setItemName(...)

setItemName(newName, [, "name"]) 

Sets the name of the object "name" to "newName" and returns the name applied. If "name" is not given the currently selected item is used.

May raise [NotFoundError](scripterapi.html#NotFoundError) if the object doesn't exist. 

setLineBlendmode(...)

setLineBlendmode(blendmode, ["name"]) 

Sets the line blendmode of the object "name" to blendmode is the name of one of the defined colors. If "name" is not given the currently selected item is used. 

setLineCap(...)

setLineCap(captype, ["name"]) 

Sets the line cap style of the object "name" to the style "cap". If "name" is not given the currently selected item is used.

The value "cap" must be taken amongst predefined constants CAP_<type>: CAP_FLAT, CAP_ROUND, or CAP_SQUARE. 

setLineColor(...)

setLineColor("color", ["name"]) 

Sets the line color of the object "name" to the color "color". If "name" is not given the currently selected item is used. 

setLineJoin(...)

setLineJoin(join, ["name"]) 

Sets the line join style of the object "name" to the style "join". If "name" is not given the currently selected item is used.

The value "join" must be taken amongst predefined constants JOIN_<type>: JOIN_BEVEL, JOIN_MITTER or JOIN_ROUND. 

setLineShade(...)

setLineShade(shade, ["name"]) 

Sets the shading of the line color of the object "name" to "shade". "shade" must be an integer value in the range from 0 (lightest) to 100 (full color intensity). If "name" is not given the currently selected item is used.

May raise ValueError if the line shade is out of bounds. 

setLineStyle(...)

setLineStyle(style, ["name"]) 

Sets the line style of the object "name" to the style "style". If "name" is not given the currently selected item is used.

There are predefined constants for "style" - LINE_<style>. 

setLineTransparency(...)

setLineTransparency(transparency, ["name"]) 

Sets the line transparency of the object "name". If "name" is not given the currently selected item is used. In spite of this command's wording, the "transparency" value is actually a decimal corresponding to the opacity, so for example, 0.9 = 90% opacity, 0.2 = 20% opacity. 

setLineWidth(...)

setLineWidth(width, ["name"]) 

Sets line width of the object "name" to "width". "width" must be in the range from 0.0 to 12.0 inclusive, and is measured in points. If "name" is not given the currently selected item is used. 

May raise ValueError if the line width is out of bounds. 

setMultiLine(...)

setMultiLine("namedStyle", ["name"]) 

Sets the line style of the object "name" to the named style "namedStyle". If "name" is not given the currently selected item is used.

May raise [NotFoundError](scripterapi.html#NotFoundError) if the line style doesn't exist. 

setObjectAttributes(...)

setObjectAttributes(attributes, ["name"]) 

Sets attributes of the object "name". If "name" is not given the currently selected item is used.

attributes is a list of dictionary. Each dictionary must have those keys: Name, Type, Value, Parameter, Relationship, RelationshipTo, AutoAddTo. All values must be strings. 

traceText(...)

traceText(["name"]) 

Deprecated, use outlineText() instead. 

## Getting Object Properties 

getObjectType(...)

getObjectType(["name"]) -> string 

Get type of object "name" as a string. If "name" is not given the currently selected item is used. 

getCornerRadius(...)

getCornerRadius(["name"]) -> integer 

Returns the corner radius of the object "name". The radius is expressed in points. If "name" is not given the currently selected item is used. 

getCustomLineStyle(...)

getCustomLineStyle(["name"]) -> string 

Returns the style name of custom line style for the object. If object's "name" is not given the currently selected item is used. 

getFillBlendmode(...)

getFillBlendmode(["name"]) -> integer 

Returns the fill blendmode of the object "name". If "name" is not given the currently selected Item is used. 

getFillColor(...)

getFillColor(["name"]) -> string 

Returns the name of the fill color of the object "name". If "name" is not given the currently selected item is used. 

getFillShade(...)

getFillShade(["name"]) -> integer 

Returns the shading value of the fill color of the object "name". If "name" is not given the currently selected item is used. 

getFillTransparency(...)

getFillTransparency(["name"]) -> float 

Returns the fill transparency of the object "name". If "name" is not given the currently selected Item is used. 

getImageColorSpace(...)

getImageColorSpace(["name"]) -> integer (see CSPACE_* constants) 

Returns the color space of the image loaded in image frame "name" as one of following integer constants: 

- CSPACE_RGB 
- CSPACE_CMYK 
- CSPACE_GRAY 
- CSPACE_DUOTONE 
- CSPACE_MONOCHROME. 

Returns CSPACE_UNDEFINED if there is no image loaded in the frame.

If "name" is not given the currently selected item is used. 

getImageFile(...)

getImageFile(["name"]) -> string 

Returns the filename for the image in the image frame. If "name" is not given the currently selected item is used. 

getImageOffset(...)

getImageOffset(["name"]) -> (x,y) 

Returns a (x, y) tuple containing the offset values in point unit of the image frame "name". If "name" is not given the currently selected item is used. 

getImageScale(...)

getImageScale(["name"]) -> (x,y) 

Returns a (x, y) tuple containing the scaling values of the image frame "name". If "name" is not given the currently selected item is used. 

getItemPageNumber(...)

getItemPageNumber(["name"]) -> integer 

Returns the page number for the given page item. If "name" is not given the currently selected item is used. 

getLineBlendmode(...)

getLineBlendmode(["name"]) -> integer 

Returns the line blendmode of the object "name". If "name" is not given the currently selected Item is used. 

getLineCap(...)

getLineEnd(["name"]) -> integer (see constants) 

Returns the line cap style of the object "name". If "name" is not given the currently selected item is used. The cap types are: CAP_FLAT, CAP_ROUND, CAP_SQUARE 

getLineColor(...)

getLineColor(["name"]) -> string 

Returns the name of the line color of the object "name". If "name" is not given the currently selected item is used. 

getLineJoin(...)

getLineJoin(["name"]) -> integer (see contants) 

Returns the line join style of the object "name". If "name" is not given the currently selected item is used. The join types are: JOIN_BEVEL, JOIN_MITTER, JOIN_ROUND 

getLineShade(...)

getLineShade(["name"]) -> integer 

Returns the shading value of the line color of the object "name". If "name" is not given the currently selected item is used. 

getLineStyle(...)

getLineStyle(["name"]) -> integer (see constants) 

Returns the line style of the object "name". If "name" is not given the currently selected item is used. Line style constants are: LINE_DASH, LINE_DASHDOT, LINE_DASHDOTDOT, LINE_DOT, LINE_SOLID 

getLineTransparency(...)

getLineTransparency(["name"]) -> float 

Returns the line transparency of the object "name". If "name" is not given the currently selected Item is used. 

getLineWidth(...)

getLineWidth(["name"]) -> integer 

Returns the line width of the object "name". If "name" is not given the currently selected Item is used. 

getObjectAttributes(...)

getObjectAttributes(["name"]) -> list 

Returns a list containing all attributes of object "name". If "name" is not given the currently selected Item is used. 

getPosition(...)

getPosition(["name"]) -> (x,y) 

Returns a (x, y) tuple with the position of the object "name". If "name" is not given the currently selected item is used. The position is expressed in the actual measurement unit of the document - see UNIT_<type> for reference. 

getRotation(...)

getRotation(["name"]) -> integer 

Returns the rotation of the object "name". The value is expressed in degrees, and clockwise is positive. If "name" is not given the currently selected item is used. 

getSize(...)

getSize(["name"]) -> (width,height) 

Returns a (width, height) tuple with the size of the object "name". If "name" is not given the currently selected item is used. The size is expressed in the current measurement unit of the document - see UNIT_<type> for reference. 

## Manipulating Objects 

combinePolygons()

combinePolygons() 

Combines two or more selected polygons.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError). 

copyObject(...)

copyObject(["name"]) -> string 

Copies the specified object or first item of selection if "name" is not given.

Deprecated. Use copyObjects() instead. 

copyObjects(...)

copyObjects(names) 

Copies the specified objects or the current object selection if no item names are given.

The names of objects to copy can be provided as a string to copy a single object or as a list of strings to copy several objects at once. 

duplicateObject(...)

duplicateObject(["name"]) -> string 

Creates a duplicate of the specified object or of first item of selection if "name" is not given.

Returns name of new object.

Deprecated. Use duplicateObjects() instead. 

duplicateObjects(...)

duplicateObjects(names) -> list 

Creates a duplicate of the specified objects or of the current selection if no names are given.

The names of objects to duplicate can be provided as a string to duplicate a single object or as a list of strings to duplicate several objects at once.

Returns a list of the names of the newly created objects. 

getCharacterStyle(...)

getCharacterStyle(["name"]) 

Return name of character style applied to object named "name". If "name" is not given, the currently selected object is used.

If current object has a text selection, the name of style applied to start of selection is returned. Otherwise the name of the item default character style is returned.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError) if target frame is not a text frame. 

getParagraphStyle(...)

getParagraphStyle(["name"]) 

Return name of paragraph style applied to object named "name". If "name" is not given, the currently selected object is used.

If current object has a text selection, the name of style applied to start of selection is returned. Otherwise the name of the item default style is returned.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError) if target frame is not a text frame. 

getStyle(...)

getStyle(["name"]) 

Deprecated. Use getParagraphStyle() instead. 

getTextFlowMode(...)

getTextFlowMode(["name"]) -> integer 

Return the current text flow mode used by item "name" as an integer. If "name" is not given, the currently selected object is used.

The function will return one of the following value: 

- 0 : text flow around frame is disabled 
- 1 : text flow around frame shape 
- 2 : text flow around frame bounding box 
- 3 : text flow around frame contour line 
- 4 : text flow around image clip path 

groupObjects(...)

groupObjects(list) 

Groups the objects named in "list" together. "list" must contain the names of the objects to be grouped. If "list" is not given the currently selected items are used. 

isLocked(...)

isLocked(["name"]) -> bool 

Returns true if is the object "name" locked. If "name" is not given the currently selected item is used. 

lockObject(...)

lockObject(["name"]) -> bool 

Locks the object "name" if it's unlocked or unlock it if it's locked. If "name" is not given the currently selected item is used. Returns true if locked. 

moveObject(...)

moveObject(dx, dy [, "name"]) 

Moves the object "name" by dx and dy relative to its current position. The distances are expressed in the current measurement unit of the document (see UNIT constants). If "name" is not given the currently selected item is used. If the object "name" belongs to a group, the whole group is moved.

If what you wish to do is to move an object to a different page or layer, it may be more efficient to do the sequence *copyObject(...)*, followed by *pasteObject(...)*, and then finally *deleteObject(...)* to delete the original. 

moveObjectAbs(...)

moveObjectAbs(x, y [, "name"]) 

Moves the object "name" to a new location. The coordinates are expressed in the current measurement unit of the document (see UNIT constants). If "name" is not given the currently selected item is used. If the object "name" belongs to a group, the whole group is moved. 

pasteObject(...)

pasteObject() -> string 

Pastes an object from the clipboard. This will be used only or most sensibly following *copyObject(...)*, since otherwise there will likely be nothing in the clipboard to paste.

Returns the names of the newly created object in a comma separated string.

Deprecated. Use pasteObjects() instead. 

pasteObjects(...)

pasteObjects() -> list 

Pastes the content of clipboard to canvas. This will be used only or most sensibly following *copyObjects(...)*, since otherwise there will likely be nothing in the clipboard to paste.

Returns the names of the newly created object in a list. 

rotateObject(...)

rotateObject(rot [, "name"]) 

Rotates the object "name" by "rot" degrees relatively. The object is rotated by the vertex that is currently selected as the rotation point - by default, the top left vertext at zero rotation. Positive values mean counter clockwise rotation when the default rotation point is used. If "name" is not given the currently selected item is used. 

rotateObjectAbs(...)

rotateObjectAbs(rot [, "name"]) 

Sets the rotation of the object "name" to "rot". Positive values mean counter clockwise rotation. If "name" is not given the currently selected item is used. 

scaleGroup(...)

scaleGroup(factor [,"name"]) 

Scales the group the object "name" belongs to. Values greater than 1 enlarge the group, values smaller than 1 make the group smaller e.g a value of 0.5 scales the group to 50 % of its original size, a value of 1.5 scales the group to 150 % of its original size. The value for "factor" must be greater than 0. If "name" is not given the currently selected item is used.

May raise ValueError if an invalid scale factor is passed. 

setCharacterStyle(...)

setCharacterStyle("style" [, "name"]) 

Apply the named character "style" to the object named "name".

If object name is not provided, style is applied on current object selection.

If multiple objects are selected or if selected object has no text selection, style is applied on selected object(s). Otherwise style is applied to the current text selection.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError) if the target frame is not a text frame.

May raise [NotFoundError](scripterapi.html#NotFoundError) if specified style name does not exist in current document. 

setParagraphStyle(...)

setParagraphStyle("style" [, "name"]) 

Apply the named paragraph "style" to the object named "name".

If object name is not provided, style is applied on current object selection.

If multiple objects are selected or if selected object has no text selection, style is applied on selected object(s). Otherwise style is applied to the current text selection.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError) if the target frame is not a text frame.

May raise [NotFoundError](scripterapi.html#NotFoundError) if specified style name does not exist in current document. 

setScaleFrameToImage(...)

setScaleFrameToImage([name]) 

Set frame size on the selected or specified image frame to image size.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError). 

setScaleImageToFrame(...)

setScaleImageToFrame(scaletoframe, proportional=None, name=<selection>) 

Sets the scale to frame on the selected or specified image frame to `scaletoframe'. If `proportional' is specified, set fixed aspect ratio scaling to `proportional'. Both `scaletoframe' and `proportional' are boolean.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError). 

setStyle(...)

setStyle("style" [, "name"]) 

Deprecated. Use setParagraphStyle() instead. 

setTextFlowMode(...)

setTextFlowMode("name" [, state]) 

Enables/disables "Text Flows Around Frame" feature for object "name".

Called with parameters string name and optional int "state" (0 <= state <= 3). Setting "state" to 0 will disable text flow. Setting "state" to 1 will make text flow around object frame. Setting "state" to 2 will make text flow around bounding box. Setting "state" to 3 will make text flow around contour line. If "state" is not passed, text flow is toggled. 

sizeObject(...)

sizeObject(width, height [, "name"]) 

Resizes the object "name" to the given width and height. If "name" is not given the currently selected item is used. 

unGroupObjects(...)

unGroupObjects("name") 

Destructs the group the object "name" belongs to. If "name" is not given the currently selected item is used. 

textFlowMode(...)

textFlowMode("name" [, state]) 

Deprecated. Use setTextFlowMode() instead. 

## Creating and Manipulating Styles 

createCharStyle(...) 

createCharStyle(...) 

Creates a character style. This function takes the following keyword parameters: 

- "name" [required] -> name of the char style to create (first parameter) 
- "font" [optional] -> name of the font to use (second parameter) 
- fontsize [optional] -> font size to set (double) (third parameter) 
- "features" [optional] -> nearer typographic details can be defined by a string that might contain the following phrases comma-separated (without spaces!) (fourth parameter - a string): 
  - inherit 
  - bold 
  - italic 
  - underline 
  - underlinewords 
  - strike 
  - superscript 
  - subscript 
  - outline 
  - shadowed 
  - allcaps 
  - smallcaps 
- "fillcolor" [optional], fillshade [optional] -> specify fill options (5th parameter: string, 6th parameter: a float 1.0 = 100%) 
- "strokecolor" [optional], strokeshade [optional] -> specify stroke options (7th parameter: string, 8th parameter: a float 1.0 = 100%) 
- baselineoffset [optional] -> offset of the baseline (ninth parameter) 
- shadowxoffset [optional], shadowyoffset [optional] -> offset of the shadow if used (10th and 11th parameters) 
- outlinewidth [optional] -> width of the outline if used (12th parameter) 
- underlineoffset [optional], underlinewidth [optional] -> underline options if used (13th and 14th parameters) 
- strikethruoffset [optional], strikethruwidth [optional] -> strikethru options if used (15th and 16th parameters) 
- scaleh [optional], scalev [optional] -> scale of the chars (17th and 18th parameters - float values, 1.0 = 100%) 
- tracking [optional] -> tracking of the text (19th parameter - number with odd math, e.g. -50 = -5.0%) 
- "language" [optional] -> language code (20th parameter - a string en = English) 
- "fontfeatures" [optional] -> a string that contains a comma-separated list of OpenType font features (21th parameter - a string): 

- Ligatures: 
  - -liga: disable common ligatures 
  - -clig: disable contextual ligatures 
  - +dlig: enable discretionary ligatures 
  - +hlig: enable historical ligatures 
- Script Position: 
  - +subs: enable subscript 
  - +sups: enable superscript 
  - +ordn: enable ordinals 
- Capitals: 
  - +smcp: enable small capitals 
  - +c2sc: enable small capitals from capitals 
  - +pcap: enable petite capitals 
  - +c2pc: enable petite capitals from capitals 
  - +unic: enable unicase 
  - +titl: enable titling 
- Numerals: 
  - +lnum: enable lining figures 
  - +tnum: enable old style numerals 
- Numeral Width: 
  - +pnum: enable proportional figures 
  - +tnum: enable tabular figures 
- Numeral Fractions: 
  - +frac: enable diagonal fractions 
  - +afrc: enable stacked fractions 
- Numeral zero: 
  - +zero: enable slashed zero 
- Style sets: 

- +ss01: enable 1st style set 
- ... 
- +ss20: enable 20th style set 

Any style attribute not explicitly defined will have its value inherited from default character style. 

Due to the important number of arguments of this function, it is strongly advised to use Python keyword syntax when calling this function. For example if a style needs to alter only font size, do not use this syntax: 

- newStyle = createCharStyle("New Style", "Arial Regular", 12) 

but use this syntax instead: 

- newStyle = createCharStyle("New Style", fontsize=12) 

For some guidance on this showing in particular how to set tracking, see the wiki page [Text and Text Manipulation](https://wiki.scribus.net/canvas/Text_and_Text_Manipulation). 

createCustomLineStyle(...) 

createCustomLineStyle(styleName, style) 

Creates the custom line style 'styleName'. 

This function takes list of dictionary as parameter for "style". Each dictionary represent one subline within style. Dictionary can have those keys: 

- Color [optional] -> name of the color to use (string) 
- Dash [optional] -> type of line to use (integer) 
- LineEnd [optional] -> type of LineEnd to use (integer) 
- LineJoin [optional] -> type of LineJoin to use (integer) 
- Shade [optional] -> opacity of line (integer) 
- Width [optional] -> width of line (double) 

createParagraphStyle(...) 

createParagraphStyle(...) 

Creates a paragraph style. This function takes the following keyword parameters: 

- "name" [required] -> specifies the name of the paragraphstyle to create 
- linespacingmode [optional] -> specifies the linespacing mode; possible modes are: 
  - fixed linespacing: 0 
  - automatic linespacing: 1 
  - baseline grid linespacing: 2 
- linespacing [optional] -> specifies the linespacing if using fixed linespacing 
- alignment [optional] -> specifies the alignment of the paragraph 
  - left: 0 
  - center: 1 
  - right: 2 
  - justify: 3 
  - extend: 4 
- leftmargin [optional], rightmargin [optional] -> specify the margin 
- gapbefore [optional], gapafter [optional] -> specify the gaps to the heading and following paragraphs 
- firstindent [optional] -> the indent of the first line 
- hasdropcap [optional] -> specifies if there are caps (1 = yes, 0 = no) 
- dropcaplines [optional] -> height (in lines) of the caps if used 
- dropcapoffset [optional] -> offset of the caps if used 
- "charstyle" [optional] -> char style to use 
- "bullet" [optional] -> string to use as bullet 
- "tabs" [optional] -> a list of tab definitions 

- a tab is defined as a tuple with the following format (position,type,fillchar) 
- position [required] -> float value for the position 
- type [optional] -> left: 0 [default], right: 1, period: 2, comma: 3, center: 4 
- fillchar [optional] -> the char to fill the space; default is none 

If you wish to skip a number of settings, unfortunately, this command will not accept null values, i.e., a series of commas. You *must* put some integer value for each of the potential parameters. For example, imagine you wish to only specify a name for the Paragraph Style, and the Character Style. Your command should be something like: 

- scribus.createParagraphStyle("MyNewStyle", 0, 0, 0, 0, 0, 0, 0, 0, 0, "MyCharStyle")) 

On the other hand, if you only wanted to specify a name and linespacing mode, you can quit whenever after you finished with non-zero data: 

- scribus.createParagraphStyle("MyOtherNewStyle", 1) 

getAllStyles(...) 

getAllStyles() -> list 

Deprecated, use getParagraphStyles() instead. 

getCellStyles(...) 

getCellStyles() -> list 

Return a list of the names of all cell styles in the current document. 

getCharStyles(...) 

getCharStyles() -> list 

Return a list of the names of all character styles in the current document. 

getLineStyles(...) 

getLineStyles() -> list 

Return a list of the names of all line styles in the current document. 

getParagraphStyles(...) 

getParagraphStyles() -> list 

Return a list of the names of all paragraph styles in the current document. 

getTableStyles(...) 

getTableStyles() -> list 

Return a list of the names of all table styles in the current document. 

## Handling Text Frames 

dehyphenateText(...)

dehyphenateText(["name"]) -> bool 

Does dehyphenation on text frame "name". If "name" is not given the currently selected item is used.

May raise WrongFrameTypeError if the target frame is not a text frame 

deleteText(...)

deleteText(["name"]) 

Deletes any text in the text frame "name". If there is some text selected, only the selected text will be deleted. If "name" is not given the currently selected item is used. 

getAllText(...)

getAllText(["name"]) -> string 

Returns the text of the text frame "name" and of all text frames which are linked with this frame. If this textframe has some text selected, the selected text is returned. If "name" is not given the currently selected item is used. 

getColumnGap(...)

getColumnGap(["name"]) -> float 

Returns the column gap size of the text frame "name" expressed in points. If "name" is not given the currently selected item is used. 

getColumns(...)

getColumns(["name"]) -> integer 

Gets the number of columns of the text frame "name". If "name" is not given the currently selected item is used. 

getFirstLineOffset(...)

getFirstLineOffset(["name"]) -> integer 

Gets the offset of the first line of text inside text frame "name". If "name" is not given the currently selected item is used. 

getFirstLinkedFrame(...)

getFirstLinkedFrame(["name"]) -> string 

Return the first text frame in the chain. If "name" is not given the currently selected item is used. 

getFont(...)

getFont(["name"]) -> string 

Returns the font name for the text frame "name". If this text frame has some text selected the value assigned to the first character of the selection is returned. If "name" is not given the currently selected item is used. 

getFontSize(...)

getFontSize(["name"]) -> float 

Returns the font size in points for the text frame "name". If this text frame has some text selected the value assigned to the first character of the selection is returned. If "name" is not given the currently selected item is used. 

getFrameText(...)

getFrameText(["name"]) -> string 

Returns the text visible in text frame "name". If this text frame has some text selected, the selected text is returned. If "name" is not given the currently selected item is used.

This function returns only the text visible in specified frame. If you need to retrieve the text contained in a text chain, use [getAllText()](#-getAllText) instead.

As this function depends on text layout being up-to-date, you may need to call [layoutText()](#-layoutText) or [layoutTextChain()](#-layoutTextChain) before calling this function in order to get expected result. 

getLastLinkedFrame(...)

getLastLinkedFrame(["name"]) -> string 

Return the last text frame in the chain. If "name" is not given the currently selected item is used. 

getLineSpacing(...)

getLineSpacing(["name"]) -> float 

Returns the line spacing ("leading") of the text frame "name" expressed in points. If "name" is not given the currently selected item is used. 

getNextLinkedFrame(...)

getNextLinkedFrame(["name"]) -> string 

Return the next text frame in the chain or None if specified frame is the last frame in the chain. If "name" is not given the currently selected item is used. 

getPrevLinkedFrame(...)

getPrevLinkedFrame(["name"]) -> string 

Return the previous text frame in the chain or None if specified frame is the first frame in the chain. If "name" is not given the currently selected item is used. 

getText(...)

getText(["name"]) -> string 

Deprecated. Use getFrameText() instead. 

getTextColor(...)

getTextColor(["name"]) -> string 

Returns the name of the text color used for text frame "name". If this text frame has some text selected the value assigned to the first character of the selection is returned. If "name" is not given the currently selected item is used.

May raise WrongFrameTypeError if the target frame is not a text frame 

getTextDistances(...)

getTextDistances(["name"]) -> tuple 

Returns the text distances of the text frame "name" expressed in points. The distances are returned as a tuple like (left, right, top, bottom). If "name" is not given the currently selected item is used. 

getTextLength(...)

getTextLength(["name"]) -> integer 

Returns the length of the text in the text frame "name". If "name" is not given the currently selected item is used. 

getTextLines(...)

getTextLines(["name"]) -> integer 

Returns the number of lines of text in text frame "name". If "name" is not given the currently selected item is used.

As this function depends on text layout being up-to-date, you may need to call [layoutText()](#-layoutText) or [layoutTextChain()](#-layoutTextChain) before calling this function in order to get expected result. 

getTextShade(...)

getTextShade(["name"]) -> integer 

Returns the shade of text color used for text frame "name". If this text frame has some text selected the value assigned to the first character of the selection is returned. If "name" is not given the currently selected item is used.

May raise WrongFrameTypeError if the target frame is not a text frame 

getTextVerticalAlignment(...)

getTextVerticalAlignment(["name"]) -> integer 

Gets the vertical alignment of text inside text frame "name". If "name" is not given the currently selected item is used. 

hyphenateText(...)

hyphenateText(["name"]) -> bool 

Does hyphenation on text frame "name". If "name" is not given the currently selected item is used.

May raise WrongFrameTypeError if the target frame is not a text frame 

insertHtmlText(...)

insertHtmlText("file", ["name"]) 

Inserts the text from "file" into the text frame "name". Text must be UTF encoded (see [setText](#-setText)() as reference). If "name" is not given the currently selected item is used.

May raise WrongFrameTypeError if the target frame is not a text frame 

insertText(...)

insertText("text", pos, ["name"]) 

Inserts the text "text" at the position "pos" into the text frame "name". Text must be UTF encoded (see [setText](#-setText)() as reference) The first character has an index of 0. Inserting text at position -1 appends it to the frame. If "name" is not given the currently selected item is used.

For performance reason, this function does not update text layout in any way. As a consequence, you may need to call [layoutText()](#-layoutText) or [layoutTextChain()](#-layoutTextChain) at appropriate times after calling this function and before calling functions such as [getFrameText()](#-getFrameText) or [getTextLines()](#-getTextLines).

May throw IndexError for an insertion out of bounds. 

isPDFBookmark(...)

isPDFBookmark(["name"]) -> bool 

Returns true if the text frame "name" is a PDF bookmark. If "name" is not given the currently selected item is used.

May raise WrongFrameTypeError if the target frame is not a text frame 

layoutText(...)

layoutText(["name"]) 

Relayout text in the text frame "name". If "name" is not given the currently selected item is used. 

layoutTextChain(...)

layoutTextChain(["name"]) 

Relayout the whole text chain whom the text frame "name" belongs. If "name" is not given the currently selected item is used. 

linkTextFrames(...)

linkTextFrames("fromname", "toname") 

Link two text frames. The frame named "fromname" is linked to the frame named "toname". The source frame must not already link to another frame. The target frame must not be linked from another frame.

May throw [ScribusException](#ScribusException) if linking rules are violated. 

selectFrameText(...)

selectFrameText(start, count, ["name"]) 

Selects "count" characters of text in the text frame "name" starting from the character "start". Character counting starts at 0. If "count" is zero, any text selection will be cleared. If "count" is -1, the selection will extend to the end of the frame. If "name" is not given the currently selected item is used.

This function only acts on the text visible in the specified frame. If you need to work on the text contained in a text chain, use selectText() instead.

As this function depends on text layout being up-to-date, you may need to call [layoutText()](#-layoutText) or [layoutTextChain()](#-layoutTextChain) before calling this function in order to get expected result.

May throw IndexError if the selection is outside the bounds of the text. 

selectText(...)

selectText(start, count, ["name"]) 

Selects "count" characters of text in the text frame "name" starting from the character "start". Character counting starts at 0. If "count" is zero, any text selection will be cleared. If "name" is not given the currently selected item is used.

May throw IndexError if the selection is outside the bounds of the text.

There is no specific command to select all of the text in a frame. To accomplish this, you might create a function in your script which you would call with the name of the frame as follows:

def SelectAllText(textframe): 

  texlen = scribus.getTextLength(textframe) 

  scribus.selectText(0,texlen,textframe) 

  return

One of the reasons this is important is that, should you want to select a frame and then apply a Paragraph Style to the frame, you will find that a frame with multiple paragraphs will not have the style set for all of the text, only the last paragraph. Therefore, the solution is to select all the text of the frame, and then apply the style. 

setColumns(...)

setColumns(nr, ["name"]) 

Sets the number of columns of the text frame "name" to the integer "nr". If "name" is not given the currently selected item is used.

May throw ValueError if number of columns is not at least one. 

setColumnGap(...)

setColumnGap(size, ["name"]) 

Sets the column gap of the text frame "name" to the value "size". If "name" is not given the currently selected item is used.

May throw ValueError if the column gap is out of bounds (must be positive). 

setFirstLineOffset(...)

setFirstLineOffset(offset, ["name"]) 

Sets the offset of the first line of text inside text frame "name" to the specified offset policy. If "name" is not given the currently selected item is used. "offset" should be one of the FLOP_* constants defined in this module - see dir(scribus).

May throw ValueError for an invalid offset constant. 

setFont(...)

setFont("font", ["name"]) 

Sets the font of the text frame "name" to "font". If there is some text selected only the selected text is changed. If "name" is not given the currently selected item is used.

May throw ValueError if the font cannot be found. 

setFontSize(...)

setFontSize(size, ["name"]) 

Sets the font size of the text frame "name" to "size". "size" is treated as a value in points. If there is some text selected only the selected text is changed. "size" must be in the range 1 to 512. If "name" is not given the currently selected item is used.

May throw ValueError for a font size that's out of bounds. 

setLineSpacing(...)

setLineSpacing(size, ["name"]) 

Sets the line spacing ("leading") of the text frame "name" to "size". "size" is a value in points. If "name" is not given the currently selected item is used.

May throw ValueError if the line spacing is out of bounds. 

setLineSpacingMode(...)

setLineSpacingMode(mode, ["name"]) 

Sets the line spacing mode of the text frame "name" to "mode". If "name" is not given the currently selected item is used. Mode values are the same as in createParagraphStyle.

May throw ValueError if the line spacing mode is out of bounds. 

setPDFBookmark(...)

setPDFBookmark("toggle", ["name"]) 

Sets whether (toggle = 1) the text frame "name" is a bookmark or not. If "name" is not given the currently selected item is used.

May raise WrongFrameTypeError if the target frame is not a text frame 

setText(...)

setText("text", ["name"]) 

Sets the text of the text frame "name" to the text of the string "text". Text must be UTF8 encoded - use e.g. unicode(text, 'iso-8859-2'). See the FAQ for more details. If "name" is not given the currently selected item is used. 

setTextAlignment(...)

setTextAlignment(align, ["name"]) 

Sets the text alignment of the text frame "name" to the specified alignment. If "name" is not given the currently selected item is used. "align" should be one of the ALIGN_ constants defined in this module - see dir(scribus).

May throw ValueError for an invalid alignment constant. 

setTextDistances(...)

setTextDistances(left, right, top, bottom, ["name"]) 

Sets the text distances of the text frame "name" to the values "left" "right", "top" and "bottom". If "name" is not given the currently selected item is used.

May throw ValueError if any of the distances are out of bounds (must be positive). 

setTextScalingH(...)

setTextScalingH(scale, ["name"])) 

Sets the horizontal character scaling of the object "name" to "scale" in percent. If "name" is not given the currently selected item is used. 

setTextScalingV(...)

setTextScalingV(scale, ["name"])) 

Sets the vertical character scaling of the object "name" to "scale" in percent. If "name" is not given the currently selected item is used. 

setTextColor(...)

setTextColor("color", ["name"]) 

Sets the text color of the text frame "name" to the color "color". If there is some text selected only the selected text is changed. If "name" is not given the currently selected item is used. 

setTextShade(...)

setTextShade(shade, ["name"]) 

Sets the shading of the text color of the object "name" to "shade". If there is some text selected only the selected text is changed. "shade" must be an integer value in the range from 0 (lightest) to 100 (full color intensity). If "name" is not given the currently selected item is used. 

setTextStroke(...)

setTextStroke("color", ["name"]) 

Set "color" of the text stroke. If "name" is not given the currently selected item is used. 

setTextVerticalAlignment(...)

setTextVerticalAlignment(align, ["name"]) 

Sets the vertical alignment of text inside text frame "name" to the specified alignment. If "name" is not given the currently selected item is used. "align" should be one of the ALIGNV_ constants defined in this module - see dir(scribus).

May throw ValueError for an invalid alignment constant. 

textOverflows(...)

textOverflows(["name", nolinks]) -> integer 

Returns 1 if there are overflowing characters in text frame "name", 0 if not. If nolinks is set to non zero value, it takes only one frame - it doesn't use text frame linking. Without this parameter it searches all linking chain.

May raise WrongFrameTypeError if the target frame is not an text frame 

unlinkTextFrames(...)

unlinkTextFrames("name") 

Remove the specified (named) object from the text frame flow/linkage. If the frame was in the middle of a chain, the previous and next frames will be connected, eg 'a->b->c' becomes 'a->c' when you [unlinkTextFrames](#-unlinkTextFrames)(b)'

May throw [ScribusException](#ScribusException) if linking rules are violated. 

## Commands for Images & Vectors 

createImage(...)

createImage(x, y, width, height, ["name"]) -> string 

Creates a new image frame on the current page and returns its name. The coordinates are given in the current measurement units of the document. "name" should be a unique identifier for the object because you need this name for further access to that object. If "name" is not given Scribus will create one for you.

May raise [NameExistsError](scripterapi.html#NameExistsError) if you explicitly pass a name that's already used. 

deleteObject(...)

deleteObject(["name"]) 

Deletes the item with the name "name". If "name" is not given the currently selected item is deleted. 

loadImage(...)

loadImage("filename" [, "name"]) 

Loads the picture "picture" into the image frame "name". If "name" is not given the currently selected item is used.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError) if the target frame is not an image frame 

getImageFile(...)

getImageFile(["name"]) -> string 

Returns the filename for the image in the image frame. If "name" is not given the currently selected item is used. 

setScaleFrameToImage(...)

setScaleFrameToImage([name]) 

Set frame size on the selected or specified image frame to image size.

May raise WrongFrameTypeError. 

setScaleImageToFrame(...)

setScaleImageToFrame(scaletoframe, proportional=None, name=<selection>) 

Sets the scale to frame on the selected or specified image frame to `scaletoframe'. If `proportional' is specified, set fixed aspect ratio scaling to `proportional'. Both `scaletoframe' and `proportional' are boolean.

May raise WrongFrameTypeError. 

getImageScale(...)

getImageScale(["name"]) -> (x,y) 

Returns a (x, y) tuple containing the scaling values of the image frame "name". If "name" is not given the currently selected item is used. 

setImageScale(...)

setImageScale(x, y [, "name"]) 

Sets the scaling factors of the picture in the image frame "name". If "name" is not given the currently selected item is used. A number of 1 means 100 %. Scaling factors are equal to the values shown on properties palette.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError) if the target frame is not an image frame 

getImageOffset(...)

getImageOffset(["name"]) -> (x,y) 

Returns a (x, y) tuple containing the offset values in point unit of the image frame "name". If "name" is not given the currently selected item is used. 

setImageOffset(...)

setImageOffset(x, y [, "name"]) 

Sets the position of the picture in the image frame "name". If "name" is not given the currently selected item is used. The specified offset values are equal to the values shown on properties palette when point unit is used.

May raise [WrongFrameTypeError](scripterapi.html#WrongFrameTypeError) if the target frame is not an image frame 

placeEPS(...)

placeEPS("filename", x, y) Places the EPS "filename" onto the current page, x and y specify the coordinate of the topleft corner of the EPS placed on the page If loading was successful, the selection contains the imported EPS 

placeODG(...)

placeODG("filename", x, y) Places the ODG "filename" onto the current page, x and y specify the coordinate of the topleft corner of the ODG placed on the page If loading was successful, the selection contains the imported ODG 

placeSVG(...)

placeSVG("filename", x, y) Places the SVG "filename" onto the current page, x and y specify the coordinate of the topleft corner of the SVG placed on the page If loading was successful, the selection contains the imported SVG 

placeSXD(...)

placeSXD("filename", x, y) Places the SXD "filename" onto the current page, x and y specify the coordinate of the topleft corner of the SXD placed on the page If loading was successful, the selection contains the imported SXD 

savePageAsEPS(...)

savePageAsEPS("name") 

Saves the current page as an EPS to the file "name".

May raise ScribusError if the save failed. 