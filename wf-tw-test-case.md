**Bot Tasks** contain work to be done by WorkFusion\'s Bots. These Bots
perform steps in your Business Process which are more suited for
automation than human labor. Bot Tasks can exist only as a Business
Process (BP) step.

For example, address parsing, determining the width and height of an
image, interacting with your API or repository, or filtering content
that does not meet certain criteria.

**Bot Configs** are written using the Web-Harvest library and are
executed for each Record separately. For writing Web-Harvest XML configs
you can employ predefined Web-Harvest XML elements described here or
WorkFusion\_plugins.

**Bot Config Bundle** is a bundled java library containing a bot config
and a java code reference that can be used in this bot config.

**How to Create, Test, and Run**

1.  Create and test a Web-Harvest config using WorkFusion Studio (Eclipse-based IDE).

2.  Create a Bot Use Case in WorkFusion. Choose the Bot Use Case type.(ETL is the best practice because it better fits for reusing and adds flexibility.)

3.  Create a BP and include a Bot Step based on this Use Case.
    Alternatively, you can use WorkFusion Repository and import a Bot Config Bundle to WorkFusion.

4.  Test the Bot Config in the BP using a small input batch.

5.  Make changes, if needed: column names, use proxy, datastore
    connection, output column names.

6.  Update the created Bot Use Case and use it in your production BP.

Alternatively, you can create a Bot Task in the BP (Design Process tab) from scratch (Blank Use Case) and paste your code, but this approach leads to multiple issues.

**Execution Details**

XML configuration is executed for each submission. If your input CSV file contains 40 Records, the WebHarvest XML configuration will be executed 40 times, once for each Record.

If an error occurs, the Bot Config will be run 5 times.

**Results**

The Bot Task results are defined in the \<export\> plugin settings.

All the Bot Task created columns can be used in further BP steps (both
Manual and Bot).

**Hello World Example**

The following example:

1.  gets an HTTP response from URLs listed in the **url\_to\_check** column of the input data file;

2.  records the HTTP response into the **http\_response** variable;

3.  exports all original columns and appends a new **http** column containing the **http\_response** variable value.

**Bot Config Example**

```
<?xml version="1.0" encoding="UTF-8"?>
   <config>
	<!--defining variable-->
	<var-def name="http_response">
	 <!--passing the appropriate value from url_to_check column in input data file as a parameter for http plugin-->
	 <http url = "${url_to_check}"></http>
	</var-def>

	<!--exporting all original input columns-->
	<export include-original-data="true">
	 <!--adding a new column with the http plugin result to the export file-->
	 <single-column name="http" value= "${http_response }"/>
	</export>
	
	</config>

```
