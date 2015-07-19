# Overview #
The fb.fbWidget Plugin API consists of 2 set of API function:
  * API must be implemented by plugin extends from it
  * API for re-usable field setting components

## API must be implemented by plugin extends from it ##
The following function must be implemented by field plugin:
```
_getWidget : function(event, fb) {
},
_getFieldSettingsLanguageSection : function(event, fb) {
},
_getFieldSettingsGeneralSection : function(event, fb) {
}, 
_languageChange : function(event, fb) {
}
```

All functions above accept 2 parameters. The first one is jQuery event object and the second is object specific to the field plugin. The `fb` object has the following properties:
  * **fb.target:** The field plugin instance.
  * **fb.item:** The field instance rendered in Builder Panel.
  * **fb.item.selected:** the value is true, if the field is selected in Builder Panel. This property use by `_languageChange` function only.
  * **fb.settings:** The settings of field instance rendered in Builder Panel.

![http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/override-functions.png](http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/override-functions.png)

The diagram above showing the implementation of Plain Text field for all functions above except `_languageChange` function which trigger by changing language in Form Settings tab.

## API for re-usable field setting components ##
Most function of this API accept one parameter: the options object in the following structure:
```
var options = {
  label: 'Label of Field Setting',
  name : 'field.name',
  value: 'Default Value',
  description: 'Field Setting Description' // display as in-line help 
};
```

Also, all API function return JQuery object.

<table border='1'>
<tr>
<th>No.</th><th>Field Setting</th><th>API Function</th><th>Sample Code</th>
</tr>
<tr valign='top'>
<td>1.</td>
<td><b>Label</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/label.png' />
</td>
<td>
<pre><code>_label(options)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._label({ <br>
  label: 'Text', <br>
  name: 'field.text', <br>
  description: 'Text entered below will display in the form.' <br>
});<br>
</code></pre>
<ul><li>The <code>description</code> property will display as in-line help.<br>
</td>
</tr>
<tr valign='top'>
<td>2.</td>
<td><b>In-line Help</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/help.png' />
</td>
<td>
<pre><code>_help(options)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._help({ <br>
  description: 'Text entered below will display in the form.' <br>
});<br>
</code></pre>
</li><li>When user click on the question mark, the description will display as tooltip.<br>
</li><li>The tooltip was implemented by <a href='http://craigsworks.com/projects/qtip2/'>qTip2</a> plugin.<br>
</td>
</tr>
<tr valign='top'>
<td>3.</td>
<td><b>Horizontal Alignment</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/horizontal-alignment.png' />
</td>
<td>
<pre><code>_horizontalAlignment(options)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._horizontalAlignment({ <br>
  name: 'field.horizontalAlignment', <br>
  value: 'rightAlign' <br>
});<br>
</code></pre>
</li><li>The default label is "Horizontal Align".<br>
</td>
</tr>
<tr valign='top'>
<td>4.</td>
<td><b>Vertical Alignment</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/vertical-alignment.png' />
</td>
<td>
<pre><code>_verticalAlignment(options)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._verticalAlignment({<br>
  name: 'field.verticalAlignment', <br>
  value: 'topAlign'<br>
});<br>
</code></pre>
</li><li>The default label is "Vertical Align".<br>
</td>
</tr>
<tr valign='top'>
<td>5.</td>
<td><b>Font Picker</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/font-picker.png' />
</td>
<td>
<pre><code>_fontPicker(options)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._fontPicker({ <br>
  name: 'field.fontFamily', <br>
  value: 'Tahoma' <br>
});<br>
</code></pre>
</li><li>The default label is "Font".<br>
</li><li>The font picker was customized for Form Builder based on the works of <a href='http://plugins.jquery.com/project/fontpicker-regios'>Regios Font Picker</a> plugin.<br>
</li><li>The customized source code located at <a href='http://code.google.com/p/jquery-form-builder-plugin/source/browse/trunk/src/js/jquery.fontpicker.js'>here</a>.<br>
</td>
</tr>
<tr valign='top'>
<td>6.</td>
<td><b>Font Size</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/font-size.png' />
</td>
<td>
<pre><code>_fontSize(options)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._fontSize({ <br>
  label: 'Size', <br>
  name: 'field.fontSize', <br>
  value: 12<br>
});<br>
</code></pre>
</td>
</tr>
<tr valign='top'>
<td>7.</td>
<td><b>Font Styles</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/font-styles.png' />
</td>
<td>
<pre><code>_fontStyles(options)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._fontStyles({ <br>
  names: ['field.bold', 'field.italic', 'field.underline'],<br>
  checked: [1, 0, 0]<br>
});<br>
</code></pre>
</td>
</tr>
<tr valign='top'>
<td>8.</td>
<td><b>Font Panel</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/font-panel.png' />
</td>
<td>
<pre><code>_fontPanel(options)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._fontPanel({ <br>
  fontFamily: 'Tahoma', <br>
  fontSize: 12, <br>
  fontStyles: [1, 0, 0],<br>
  idPrefix: 'field.'<br>
});<br>
</code></pre>
</td>
</tr>
<tr valign='top'>
<td>9.</td>
<td><b>Color Picker</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/color-picker.png' />
</td>
<td>
<pre><code>_colorPicker(options)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._colorPicker({ <br>
  label: 'Text', <br>
  name: 'field.color', <br>
  value: 'ffffff', <br>
  type: 'basic'<br>
});<br>
</code></pre></li></ul>

<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/color-picker-basic.png' />

<ul><li>If the type property is unspecified, it is default to "basic".<br>
</li><li>The color picker was customized for Form Builder based on the works of <a href='http://andreaslagerkvist.com/jquery/colour-picker/'>Andreas Lagerkvist</a>.<br>
</li><li>The customized source code located at <a href='http://code.google.com/p/jquery-form-builder-plugin/source/browse/trunk/src/js/jquery.colorpicker.js'>here</a>.</li></ul>

<pre><code>fb.target._colorPicker({ <br>
  label: 'Text', <br>
  name: 'field.color', <br>
  value: 'ffffff', <br>
  type: 'webSafe'<br>
});<br>
</code></pre>

<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/color-picker-websafe.png' />
</td>
</tr>
<tr valign='top'>
<td>10.</td>
<td><b>Color Panel</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/color-panel.png' />
</td>
<td>
<pre><code>_colorPanel(options)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._colorPanel({ <br>
  color: '000000', <br>
  backgroundColor: 'ffffff', <br>
  idPrefix: 'field.'<br>
});<br>
</code></pre>
</td>
</tr>
<tr valign='top'>
<td>11.</td>
<td><b>Layout</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/layout.png' />
</td>
<td>
<pre><code>_oneColumn($e);<br>
<br>
_twoColumns($e1, $e2);<br>
<br>
_twoRowsOneRow(row1col1, row2col1, row1col2);<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._oneColumn($name);<br>
<br>
fb.target._twoColumns($fontPicker, $fontSize);<br>
<br>
fb.target._twoRowsOneRow($heading, $horizontalAlignment, $fontStyles);<br>
</code></pre>
</td>
</tr>
<tr valign='top'>
<td>12.</td>
<td><b>Label, Value and Description Color Panel</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/label-value-description-color-panel.png' />
</td>
<td>
<pre><code>_labelValueDescriptionColorPanel(options)<br>
</code></pre>
</td>
<td>
<pre><code>var options = {<br>
	label: {<br>
	  color : '000000',<br>
	  backgroundColor : 'ffffff'<br>
	},<br>
	value: {<br>
	  color : '000000',<br>
	  backgroundColor : 'ffffff'<br>
	},<br>
	description: {<br>
		color : '777777',<br>
		backgroundColor : 'ffffff'<br>
	}				<br>
};<br>
<br>
fb.target._labelValueDescriptionColorPanel(options);<br>
</code></pre>
</td>
</tr>
<tr valign='top'>
<td>13.</td>
<td><b>Three Columns</b><br />
<img src='http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/api/three-columns.png' />
</td>
<td>
<pre><code>_threeColumns($e1, $e2, $e3)<br>
</code></pre>
</td>
<td>
<pre><code>fb.target._threeColumns($('&lt;div&gt;&lt;/div&gt;'), $('&lt;div&gt;Text&lt;/div&gt;'), $('&lt;div&gt;Background&lt;/div&gt;'));<br>
</code></pre>
</td>
</tr>
</table>