
Sightly replaces JSPs in AEM to give a better, more readable, maintainable, secure code. Does so by distinctly separating markup and logic.

Adobe donated Sightly to Apache and after that became HTL (HTMLTemplate Language)
Sightly extension- HTML

We can include sightly in JSP:
```
<cq:include script="template.html"/>
```
Or we can include JSP in sightly:
```
<sly data-sly-include="template.jsp"/>
```

HTL = HTML+Java/JavaScript

Steps to create sightly page: 
  * Create template, page and component in AEM.
  * Modify the basic component to be used as a Sightly component
  * Test Sightly

Two different kind of syntaxes:
  1. Block statements eg. data-sly-test 
  2. Expression language ${ and }
  
