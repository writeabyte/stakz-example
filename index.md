# What is Stakz?

**Stakz is an AI tutorial platform that helps you generate and share automation tutorials.**
Tutorials can be published on github and will be available at stakz.dev/browse/{org}/{repo}/path_to_file.

## How does it work?

Stakz implements a custom markdown parser that allows widgets to be
embedded in markdown. Pretty neat huh?

There are two main types of widgets: data and script.

#### Data Widgets

A data widget is a small input element that allows the user to input data to a page. These data values are then made available as variables to script widgets.

Here is a sample data widget:

<field label="hello" description="this binds to the hello variable">World</field>
`<field label="hello" description="this binds to the hello variable">World</field>`

#### Script Widgets

A script widget uses the values entered into data widgets and turns them into a shell command. Evaluating the script widget does not occur until the user clicks the execute button where the content of the result of the script will be copied to the clipboard.

**Be sure to read script widgets before execution to ensure security**

<script> return "echo " + hello </script>

`<script> return "echo " + hello </script>`

## Running the Script

There are two ways of running the script: pasting the command into a locally running terminal, or using the browser terminal along with a local stakz server.

## [Stakz Server](https://github.com/curtismj1/stakz-server)

The stakz server is the bridge between staz.dev and your local machine. The stakz server has two primary purposes: Persisting tutorial files and **optionally** executing commands from stakz.dev on your local machine.

Wait, the server just executes commands locally?
By now, you should be going

🚩🚩🚩**Sounds like a bad idea - Batman**🚩🚩🚩 (is this addressing Batman, or spoken by Batman? Either way...)

And it's true that browsers provide numerous layers of security designed to isolate someones local machine from any kind of remote code execution. Therefore stakz server will only execute commands when the following criteria are met.

1. Stakz Server is running with the --execute flag explicitly enabled. Without the --execute flag, the server is a basic file server.
2. The anonymous token generated when starting the stakz server matches the token specified in the terminal window (also required for saving files).

Stakz-server may also be run via the docker container to provide a layer of isolation between the commands being run and your local computer.
