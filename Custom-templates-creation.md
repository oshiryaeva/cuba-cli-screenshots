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