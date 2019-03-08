Import ETS XML into Calimero XML
=================================

Transform KNX datapoints of ETS source XML documents to Calimero XML source documents.

Copyright (C) 2010, 2011 Thomas Wimmer<br>
Copyright (C) 2015, 2018 Boris Malinowsky<br>
Documentation by Wolfgang Granzer, Boris Malinowsky<br>
Licensed under the GNU Lesser General Public License (LGPL), version 2.1

Tested with ETS 4.0.3 and ETS 5.x (latest v5.6.4). ETS 5.7 or later is not supported!

**Required steps**

1. Export your ETS project: click on _ETS_, select your project, and click _Export..._ . You get a file with the extension **.knxproj** (a ZIP archive). 
2. Check your ETS version (ETS 4/5)
3. Transform to Calimero XML using XSLT, either by using Gradle, Maven, or do it manually (see below).

**Know your ETS version!**

*Note: namespace version &ge; 20 is not supported.*

Select the correct version inside the calimero `xsl` file (line 5) you want to use. If you don't know the version, use _try and error_ with versions 11 to 14.
With the wrong version, the transformed output file will not contain any datapoints! This adjustment of the version is necessary due to ETS `.knxproj` files using versioned XML namespaces. 

* ETS 4 uses `http://knx.org/xml/project/11` or `http://knx.org/xml/project/12`
* ETS 5 uses `http://knx.org/xml/project/13` or `http://knx.org/xml/project/14`

By default, the transformation assumes a recent ETS 5 with namespace version `14`.

Import using Gradle
-------------------
* Copy the **.knxproj** archives into _src/main/resources_ (do not extract the archives).
* On the command line, execute `./gradlew`. The imported _calimero.xml_` file of each archive is written to the corresponding _build/imports/&lt;Project Name&gt;_ folder.

Import using Maven
------------------
  * Copy the **.knxproj** archives into _src/main/resources_ (do not extract the archives). 
  * Execute the Maven goal `process-resources`. For example, in the terminal change to the directory where the _pom.xml_ file resides, and type `mvn process-resources`. The output files are written to _target/generated-resources/xml/xslt_.

Manual import
-------------
  * Choose the appropriate XSL style sheet (see below).
  * Copy the chosen XSL file into the root directory of the extracted ETS project.
  * Invoke an appropriate XSLT tool. On Linux/MacOS you can use `xsltproc`, i.e., `xsltproc -o <output_XML_file> <XSL_file> <source_XML_file>`. On Microsoft Windows, you may use Saxon (http://saxon.sourceforge.net/).

Choose the appropriate XSL style sheet:

  * `ets_calimero_group.xsl`: Generates for each KNX group address one single datapoint. The resulting file can be loaded by Calimero.
  * `ets_calimero_group_name.xsl`: Generates for each KNX group address one single datapoint where the KNX group address name is used as name for the datapoint. The resulting file can be loaded by Calimero.
  * `ets_calimero.xsl`: Generates for each application object one single datapoint. Note that different application objects may have the same group address. Therefore, the output _cannot_ be imported into Calimero! However, it can be used for further (manual) processing.


The source XML file is called _0.xml_ which is contained within the sub directory that begins with a _P_, e.g., _P-0497_.

**Example invocation** 

`xsltproc -o calimero.xml ets_calimero_group_name.xsl P-0497/0.xml`

------------------------------------------------
Developed at the A-Lab, Automation Systems Group<br>
Vienna University of Technology<br>
www.auto.tuwien.ac.at/a-lab
