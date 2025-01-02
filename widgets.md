<field label="The UI label" var="label" description="For simple, unconstrained input">default value</field>

<select label="The UI label" var="select" description="Multi select from a list of  options" 
options="Option1,Option2,Option3">Option1</select>
<yaml label="Yaml input" var="yaml" description="Yaml input which will be converted to an object in the data context">
defaultKey: defaultValue
</yaml>
<json label="Json input" var="json" description="Json input which will be converted to an object in the data context">
{
"hello": {
"world": "hello!"
}
}
</json>

<script>
return `echo 'Simple script which will be used to generate a command. All fields are available via the data object, and all top level keys can be accessed directly. 
Data: ${JSON.stringify(data)}
label: ${label}
select: ${select}
yaml: ${JSON.stringify(yaml)}
json: ${JSON.stringify(json)}'
`;

</script>
