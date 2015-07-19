# Pre-requisite #
Thanks for your consideration to contribute to the project,
we assumed that you have gone through the [Design](Design.md) document
and have basic understanding of the design of the Form Builder plugin
prior to reading this document.

# How To Create New Field In 3 Steps #
1. Mock up the design of the new field and it's Field Settings tab in static html file. You can start with [Field Design Template](http://code.google.com/p/jquery-form-builder-plugin/source/browse/trunk/src/templates/field-design-template.html) and refer to the [Plain Text field mock up](http://code.google.com/p/jquery-form-builder-plugin/source/browse/trunk/src/PlainText.html).

2. Create the new field `JavaScript` file. You can start with [jQuery Form Builder Field Template](http://code.google.com/p/jquery-form-builder-plugin/source/browse/trunk/src/templates/jquery.formbuilder.field.template.js) and refer to the [fbWidget API documentation](http://code.google.com/p/jquery-form-builder-plugin/wiki/fbWidgetPluginAPI) and [Plain Text field](http://code.google.com/p/jquery-form-builder-plugin/source/browse/trunk/src/js/jquery.formbuilder.plaintext.js) implementation.

3. Integrate the new field to [form builder core plugin](http://code.google.com/p/jquery-form-builder-plugin/source/browse/trunk/src/js/jquery.formbuilder.core.js) by update `fields` property at line 17 with value you specified in plugin's `options._type` property. Done! You are ready to test drive the new field created by you.