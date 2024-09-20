# What is Stakz?

Stakz is an AI tutorial platform that helps you and execute CLI
commands, html snippets, and more.

## How does it work?

Stakz implements a custom markdown parser that allows widgets to be
embedded in markdown. There are two main types of widgets: data and script.

#### Data Widgets

A data widget is a small input element that allows the user to input data to a page. These data values are then made available as variables to script widgets.

Here is a sample data widget:

<field label="hello" description="this binds to the hello variable">World</field>
`<field label="hello" description="this binds to the hello variable">World</field>`

#### Script Widgets 
A script widget uses the values entered into data widgets, and turns them into a shell command. The script widget is not executed until the user clicks the button to prevent XSS attacks.
<script> return "echo " + hello </script>
`<script> return "echo " + hello </script>`

...and that using that variable in a script was as simple as:

