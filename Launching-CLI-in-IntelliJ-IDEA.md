Sometimes some problems may appear during launching CLI in IntelliJ IDEA with resources resolving. So, we introduce this guide.

1. Clone CUBA CLI project to your workspace.
2. In Idea choose File -> Open, specify cloned project build.gradle file. Click `Open as Project`, `OK`.
3. Navigate to `src/main/kotlin/com/haulmont/cuba/cli/EntryPoint.kt`
4. Right click on file, choose `Create 'com.haulmont.cuba.cli.EntryPointKt' run `configuration`.
5. Open created configuration.
6. Firstly, specify the working directory, otherwise, CLI will generate all artifacts inside its own project.
7. In `Before Launch` area click on green plus, `Run external tool`, green plus again.
8. In the Name field input `copy resources`. Fill field Program with `cp` and arguments with `-r build/resources/main build/classes/java`.
9. Press `OK`, `OK` again. Make sure that created external tool follows after Build. Press `OK`.
10. Open Idea settings. Navigate to Build, Execution, Deployment -> Build Tools -> Gradle -> Runner. Check `Delegate IDE build/run actions to gradle`. Press `OK`.
11. Now, you can launch CLI.