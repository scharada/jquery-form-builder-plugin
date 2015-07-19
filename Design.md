

# Overview #
This document described visual, structural and technical design of the plugin.

# Visual Design #
## Main Screen ##
![http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/design/main.png](http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/design/main.png)

The Form Builder divided to 2 panels, the panel on the left of the screen is Builder Palette and on the right is Builder Panel (form preview).

## Builder Palette ##
The Builder Palette has the follwing tabs:

![http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/design/builder-palette-small.png](http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/design/builder-palette-small.png)

**1. Add Field:** This tab contains fields available (Standard Fields and Fancy Fields) for form creation. New field can be added to Builder Panel by click the field's button or drag it to the Builder Panel. The following table display Standard Fields and Fancy Fields to be supported by the Form Builder.

|<strong>Standard Fields</strong>|<strong>Fancy Fields</strong>|
|:-------------------------------|:----------------------------|
|Single Line Text (Text Box)     |Name                         |
|Number (Digit & Decimal)        |Date (Date Picker)           |
|E-mail Address                  |Time                         |
|Web Address                     |Phone (International & US)   |
|Multi Line Text (Text Area)     |Mailing Address              |
|Multiple Choice (Radios & Checkboxes)|Currency                     |
|File Upload                     |Plain Text                   |
|-                               |Rich Text (Html Text)        |

**2. Field Settings:** This tab display settings of the field selected (To see the field settings of specific field, user need to select the field displayed in the Builder Panel). The field settings tab of image above is field settings of Plain Text.

**3. Form Settings:** This tab display settings of the form such as form heading, fonts, colors, alignment, etc.

**Note :** Both Field Settings and Form Settings tab consists of 2 sections:
  * Language Section for language-specific settings (The plugin support multi-languages, currently support English and Chinese) and
  * General Section for general settings of the field which not relevant to the language.

## Builder Panel ##

![http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/design/builder-panel.png](http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/design/builder-panel.png)

This panel preview the actual outlook of the form and fields added. User can sort the order of a field by dragging the field up or down. Also, user can delete unnecessary field by click on close button (the cross sign) located at the right top of the field.

# Structural Design #

![http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/design/structural.png](http://jquery-form-builder-plugin.googlecode.com/svn/wiki/images/design/structural.png)

The design of the Form Builder is very simple, each box in the diagram above is a plugin itself. All plugins developed for the Form Builder using "fb" as it's namespace (fb stands for form builder, not facebook). Field plugins such as `fbPlainText`, `fbSingleLineText`, etc. must extend/inherit from `fbWidget`.

## Plugin Inheritance ##
Many thanks to JQuery UI developers created ui.widget which support a critical feature: plugin inheritance. This project is built on top of ui.widget. Hardly imagined the design of the form builder plugin to achieve such level of modularity, extensibility and reusabiliy without ui.widget.

## The Core Form Builder plugin ##
The core Form Builder plugin (fb.formbuilder) initialize the Builder Palette such as load fields to the Add Field Tab, create Form Settings tab, enabled drag and drop and sorting, etc. The fb.formbuilder plugin mainly interact with fb.fbWidget plugin.

## The fb.fbWidget plugin ##
The fb.fbWidget plugin is a base plugin for all fields. It encapsulate common functionality of all fields and allow new field to be created easily by inherits or extends from it. For example, the Plain Text field (fb.fbPlainText).

## The Field plugin (fb.fbPlainText, fb.fbSingleLineText, fb.fbNumber, etc) ##
These plugins will extend from fb.fbWidget plugin. Only Plain Text plugin (fb.fbPlainText) was implemented (since 24-Jan-2011).

# Technical Design #
## Naming convention ##
All input components of Field Settings tab prefix by `field.` and Form Settings tab prefix by `form.` to prevent id and name conflicts with input components of Builder Panel.

## The Field plugin's options property ##
The plugin's default options is key building block of any field plugin, it will determine the plugin capability. Let's look at the following fb.fbPlainText's option property:
```
options : { 
  name : 'Plain Text',
  belongsTo : $.fb.formbuilder.prototype.options._fancyFieldsPanel,
  _type : 'PlainText',
  _html : '<div class="PlainText"></div>',
  _counterField : 'text',
  _languages : [ 'en', 'zh' ],
  settings : {
    en : {
      text : 'Plain Text Value',
      classes : [ 'leftAlign', 'topAlign' ]
    },
    zh : {
      text : '無格式文字',
      classes : [ 'rightAlign', 'middleAlign' ]
    },
    styles : {
      fontFamily: 'default', // form builder default
      fontSize: 'default',
      fontStyles: [0, 0, 0], // bold, italic, underline
      color : 'default',
      backgroundColor : 'default'
    }
  }
}
```

First level properties such as name, belongsTo, _type,_html,etc of the options property are mandatory.
Structure of settings property is arbitrary and it is plugin specific, but it need to comply to the following rules:
  * First level define language-specific property by language code such as `en` for English and `zh` for Chinese and follow by language independent properties.
  * Internal structure of language property such as `en` and `zh` must be same.
  * Specify CSS settings into `styles` property.
  * Specify CSS stylesheet class into `classes` array property.

## The Field plugin's properties ##
Each field render in Builder Panel has set of hidden fields (`input type="hidden"`) to store the field's properties.

For example, code below is hidden field set of the Plain Text plugin:
```
<div class="fieldProperties">
  <input type="hidden" value="null" name="fields[0].id" id="fields[0].id"> 
  <input type="hidden" value="plainText1" name="fields[0].name" id="fields[0].name"> 
  <input type="hidden" value="PlainText" name="fields[0].type" id="fields[0].type"> 
  <input type="hidden" name="fields[0].settings" id="fields[0].settings" value="{ en: {text...}}">
  <input type="hidden" value="0" name="fields[0].sequence" id="fields[0].sequence"> 
  <input type="hidden" name="fields[0].status" id="fields[0].status">
</div>
```

The set of hidden fields is same for any type of field.
Each type of field will have the following 6 hidden fields prefix by `fields` and follow by `[index]`:
|<strong>Hidden Field</strong>|<strong>Description</strong>|
|:----------------------------|:---------------------------|
|id                           |Default value is "null". If it is not null means the field is render from server-side.|
|name                         |This field is generated and unique, maybe meaningful and readable as it can be generated from English.|
|type                         |type of the field. This field is important to server-side field implementation.|
|settings                     |Store serialized JSON value of settings property of plugin's options mentioned in previous section.|
|sequence                     |Order of the field. Before fields render by server-side, it need to order in ascending order first.|
|status                       |D or U. D represents deleted and U represent updated. It will change to U when any hidden field above updated except id. It is use by server-side to find out which fields (those rendered by server-side) were updated or deleted.|