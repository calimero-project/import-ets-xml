Import ETS4 XML into Calimero XML
=================================

The contained **.xsl** files transform part of ETS4 source XML documents to Calimero XML source documents.

Copyright (C) 2010, 2011 Thomas Wimmer<br>
Documentation by Wolfgang Granzer, Boris Malinowsky<br>
Licensed under the GNU Lesser General Public License (LGPL), version 2.1

Version: 1.3<br>
Date:    09.01.2015<br>
Tested with ETS 4.0.3

1. Export ETS4 project<br>
Save your ETS4 project and export it. To do so, choose the slider _ETS_, click on the button _Projects_, choose your project, and click _Export..._ . You get a file with the extension **.knxproj**, which is a ZIP archive. 
2. Transform to Calimero XML using XSLT, either by using Maven or do it manually.

Using Maven
----------- 
  * Copy the **.knxproj** archives into _src/main/resources_. 
  * Execute the Maven goal `process-resources`. For example, in the terminal change to the directory where the _pom.xml_ file resides, and type `mvn process-resources`. The output files are written to _target/generated-resources/xml/xslt_.

Manual invocation
-----------------
  * Copy the chosen XSL file into the root directory of the extracted ETS4 project. 
  * Invoke an appropriate XSLT tool. Under Linux/OS X you may use `xsltproc`: `xsltproc -o <output_XML_file> <XSL_file> <source_XML_file>`

Choose the appropriate XSL style sheet:

  * `ets4_calimero_group.xsl`: Generates for each KNX group address one single datapoint. The resulting file can be loaded by Calimero.
  * `ets_calimero_group_name.xsl`: Generates for each KNX group address one single datapoint where the KNX group address name is used as name for the datapoint. The resulting file can be loaded by Calimero.
  * `ets4_calimero.xsl`: Generates for each application object one single datapoint. Note that different application objects may have the same group address. Therefore, the output can _not_ be imported into Calimero! However, it can be used for further (manual) processing.


The source XML file is called _0.xml_ which is contained within the sub directory that begins with a _P_ (e.g., _P-0497_).<br>
Example invocation: `xsltproc -o calimero.xml ets4_calimero_group_name.xsl P-0497/0.xml`

Under Microsoft Windows, you may use:
http://saxon.sourceforge.net/

------------------------------------------------
Developed at the A-Lab, Automation Systems Group<br>
Vienna University of Technology<br>
www.auto.tuwien.ac.at/a-lab
