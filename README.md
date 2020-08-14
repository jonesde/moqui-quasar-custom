# moqui-quasar-custom

Example component for a Quasar + Vue (render mode 'qvt') based application with custom root template for the header, etc.

This component contains two screens mounted under the root screen (webroot.xml, see MoquiConf.xml file):

1. **/custom**: custom application root screen, all screens for the app (like the custom/dashboard screen) go under this screen 
2. **/capps**: render wrapper, similar to qapps and vapps, containing the Vue + Quasar SPA shell

This uses most of the files from the moqui-runtime component but has copies of two files that need changes to use this way:

1. **capps.xml**: copied from qapps.xml with small change on line 79 to use the WebrootVue.qvt.ftl file from this component instead of from moqui-runtime
2. **WebrootVue.qvt.ftl**:
    1. change line 19 to refer to /custom instead of /apps so that capps uses screens under custom.xml instead of under apps.xml
    2. change line 20 to refer to /capps instead of /qapps so that the JavaScript in WebrootVue.qvt.js knows where it is running to translate internally
    
To use different mount points and screen names these are the places to make changes.

The custom.xml screen requires authentication so also requires authorization. The data needed for authorization is in the data/CustomSetupData.xml file and must be loaded to access the app.
 
When rendering screens through capps (just like qapps and vapps) the apps root screen (in this case custom.xml) is just a placeholder and is never rendered.
To access the screens under /custom go to /capps instead (just like going to /qapps instead of /apps), ie something like:

http://localhost:8080/capps 
