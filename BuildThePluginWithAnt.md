# Overview #
[Apache Ant](http://ant.apache.org/) is assumed pre-installed and properly configured in your machine.

All files built created in the dist directory by default.

# Different ways to build the project #
In the main directory of the project, type the following to build Form Builder plugin and it's accompanying CSS and images:
```
ant all
```

You can also create each individual component using these commands:
```
ant formbuilder  # Build non-minified Form Builder source
ant min          # Build minified Form Builder source
ant pack         # Build minified and packed Form Builder source (Smallest filesize!)
ant css          # Build CSS files
ant images       # Build images
```

To build and test the source code against JSLint type this:
```
ant lint
```

To remove all the built files using the following command:
```
ant clean
```

To retain log statements of built Javascript files which will display on Firebug's console using the following command:
```
ant -Ddev=true all
```
**Note:** The -D prepended to the `dev` parameter is a flag to tell the compiler you're defining a parameter. Don't omit it!

You can release all the built files as a zip file using the command below:
```
ant release
```

Finally, you can upload the release file to google code by using the following command:
```
ant -Dusername=<username> -Dpassword=<password> upload
```
**Note:** `<password>` is your hosting password at https://code.google.com/hosting/settings.

# Choosing fields #
Thanks to Form Builder plugin modular design, it's possible to remove features you don't need/want from the library without re-factoring the code. If you want more control over what fields are included, you can do so by adding some extra parameters to your build commands above.

To define which fields are included in your build, simply define the PLUGINS parameter with value of `options._type` of the field, like so:
```
ant -DPLUGINS="PlainText" all
```

You can specify multiple fields by separating them with a comma:
```
ant -DPLUGINS="PlainText, SingleLineText, Phone" all
```

By default all fields are included in the build.

**Note:** The -D prepended to the `PLUGINS` parameter is a flag to tell the compiler you're defining a parameter. Don't omit it!

# Grails Plugin Integration #
You can run the command below to update jQuery Form Builder plugin resources (JS, CSS, images, etc.) prior to release the grails plugin:
```
ant copyToGrails
```

# Deploy to Google App Engine (GAE) #
The jQuery Form Builder plugin live demo is hosted in Google App Engine(GAE) at
http://jquery-form-builder-plugin.appspot.com/.

You can update the live demo by using the following command:
```
ant appengine
```