In this directory are two sub directories that contain necessary components
for configuring a THREDDS Data Server (TDS) specifically for the RDA.

ConfigFiles/

   context.xml
      - TDS-specifc settings for access restriction (mysql db connection,
        logging access, etc.)
      - Makes connection to Custom RDA DataSourceRealm
      - placed in $CATALINA_HOME/webapps/thredds/META-INF
      - NOTE: this file is used upon deployment (initial launch of war file)
        and not at all afterward.  Any changes to be made should be done
        through thredds.xml (below).  This file is included for completeness.
      - NOTE: Be sure to change username & passwords where necessary.  

   thredds.xml
      - Essentially the context.xml file that is used upom restart of Tomcat
      - placed in $CATALINA_HOME/conf/localhost


   web.xml 
      - Contains configuration for locking down subdirectories
      - placed in $CATALINA_HOME/webapps/thredds/WEB-INF


RDA_RealmSourceCode/

   Contains the source code and jar files for the customized authentication
   via the RDA user database.  Pay close attention to the three files found
   under RDA_RealmSourceCode/Source/src/edu/ucar/rda/RDARealms/

   If you want to implemet role-based authorization, this would be a good
   place to do that.

   Place in $CATALINA_HOME/lib/


grib-4.3.18_YOTCTendencies.jar

   The TDS grib jar file containing grib table definitions fails to include 
   "tendency" parameters found in RDA ds629.x See:
   http://rda.ucar.edu/metadata/ParameterTables/WMO_GRIB1.98-0.162.xml
   for parameters that are needed for ds629.x.

   The included grib table jar file contains these parameter definitions.
   This file should be placed in

   webapps/thredds/WEB-INF/lib/ 

   and probably needs to be renamed (or soft linked) to match the version
   number of the current TDS installation.

   Restart the TDS after making this change.

IMPORTANT!

   Upon thredds.war deployment (new/upgrade), Steps should be:

   + Back up the files found in ConfigFiles - just in case.  If you forget,
     that why we have them in bersion control!

   + Deploy the new thredds.war

   + Place the respective files in their respective directories

   + Restart Tomcat

