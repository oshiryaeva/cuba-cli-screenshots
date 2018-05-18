This section describes how to create custom templates and generate artifacts from them by CUBA CLI.

### 1. Templates basics

All user templates should be in the `$USER_HOME/.haulmont/cli/templates` directory. Template itself is a directory with descriptor file template.xml and files used in generation, optionally divided by CUBA Platform version in separate version directories.

So the template structure may be following:
```
.
+--template.xml
+--6.8.5
|  +--... // template files for CUBA Platform 6.8.5
+--6.9.0
   +--... // template files for CUBA Platform 6.9.0
```
or following:
```
.
+--template.xml
+--... // template files for any CUBA version
```

CUBA CLI uses Apache Velocity template engine.
You can read about how to create Apache Velocity templates on its [documentation](http://velocity.apache.org/engine/1.7/user-guide.html).

### 2. template.xml structure

Basically, template.xml has following structure:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<template xmlns="http://schemas.haulmont.com/cuba/cli/template.xsd"
          modelName="entity">
    <quesitons>
        <!-- Questions block. All answers will be stored to the CliContext and will be available to 
             Apache Velocity by ${modelName.questionName}.-->
        <plain name="name" caption="Entity Name"/>
        <plain name="packageName" caption="Package Name"/>
        <options name="entityType" caption="Entity type">
            <option>Persistent</option>
            <option>Persistent embedded</option>
            <option>Not persistent</option>
        </options>
    </quesitons>
    <operations>
        <!-- Template processing block. Operations may be of two types: transform and copy.

             Transform operations indicates, that part of template, specified in 'src' attribute 
             should be processed by Apache Velocity, and result stored to 'dst' directory. Absence of
             dst attribute means, that result should be stored at project root.

             Copy operations does the same, without processing by template engine. It may be necessary for
             such things as images, or other resources, that doesn't need to be processed by template 
             engine and may be accidentally corrupted by it.-->
        <transform src="modules"/>
    </operations>
</template>
```

### 3. Template example

Lets create out own template.
For brevity, simply copy content of `cuba-cli/src/main/resources/com/haulmont/cuba/cli/cubaplugin/templates/entity` to directory `~/.haulmont/cli/template/entity`.
Than, in that directory create file `template.xml`. Fill it with template.xml example from section 2.

In terminal, go to your CUBA Platform project. Launch CLI.

To generate artifact with your template, use command `template teplateName`. For our case, the templateName will be `entity`.

