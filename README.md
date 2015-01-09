Import ETS4 XML into Calimero XML
=================================

The contained **.xsl** files transform part of ETS4 source XML documents to Calimero XML source documents.

Copyright (C) 2010, 2011 Thomas Wimmer<br>
Documentation by Wolfgang Granzer, Boris Malinowsky<br>
Licensed under the GNU Lesser General Public License (LGPL), version 2.1

Version: 1.3<br>
Date:    09.01.2015<br>
Tested with ETS 4.0.3

1. Export ETS4 project:
Save your ETS4 project and export it. To do so, choose the slider _ETS_, click on the button _Projects_, choose your project, and click _Export..._ . You get a file with the extension **.knxproj**, which is a ZIP archive. Extract that **.knxproj** file using your favorite archiving tool.

2. Transform to Calimero XML using XSLT, by choosing the appropriate XSL file:
  * `ets4_calimero_gui.xsl`: Generates for each KNX group address one single datapoint. The resulting file can be loaded by Calimero.
  * `ets_calimero_gui_grname.xsl`: Generates for each KNX group address one single datapoint where the KNX group address name is used as name for the datapoint. The resulting file can be loaded by Calimero.
  * `ets4_calimero.xsl`: Generates for each application object one single datapoint. Note that different application objects may have the same group address. Therefore, the output can _not_ be imported into Calimero! However, it can be used for further (manual) processing.

To perform the XSLT transformation, copy the chosen XSL file into the root directory of the extracted ETS4 project. Then, you have to invoke an appropriate XSLT tool. Under Linux you may use `xsltproc`:
`xsltproc -o <output_XML_file> <XSL_file> <source_XML_file>`

The source XML file is called _0.xml_ which is contained within the sub directory that begins with a _P_ (e.g., _P-0497_).
For example: `xsltproc -o calimero.xml ets4_calimero_gui.xsl P-0497/0.xml`

Under Microsoft Windows, you may use:
http://saxon.sourceforge.net/

------------------------------------------------
Developed at the A-Lab, Automation Systems Group<br>
Vienna University of Technology<br>
www.auto.tuwien.ac.at/a-lab
