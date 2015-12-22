Elements are positioned on the layout through the use of JDOC:include statements. 

The avaliable jdoc include types are 

- <jdoc:include type="head" /> This is used to set the style, script and meta elements inside the templates <head> area. 
- <jdoc:include type="component" /> This is used only once in the template to set the placement of the main content for components area.
- <jdoc:inlcude type="message" /> This is used where you want system messages to appear on the page. 
- <jdoc:include type="modules" name="modulepositionname" /> This is used to place the module position holders in the template. Additional attributes to control the layout and apperance may be added.  

**Module position holders must not only be placed in the index.php file but must also be declared in the templateDetails.xml file.**