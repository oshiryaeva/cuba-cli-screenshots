This section describes the process of creating an application using CUBA CLI.

Make sure that the necessary software is already installed and set up on your computer, see [Installation and Setup](#).

### 1. CUBA CLI basics

CUBA CLI is a tool for CUBA Platform projects scaffolding. CLI can work in two modes: shell mode and single command mode. 

### 2. Creating a project

1. Create a directory for the future project, for example `sales`, and navigate to it in a terminal.
2. Start CUBA CLI.
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/1_cuba-cli.png)
3. Input command `create-app`. You can use tab auto-completion.
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/2_cuba-cli.png)
4. CLI will ask you questions about the project. If a question implies default answer, you can press enter to accept it. You will be asked the following questions:
* **Project name** – the project name.
* **Project namespace** – the namespace which will be used as a prefix for entity names and database tables. The namespace can consist of Latin letters only and should be as short as possible.
* **Platform version** – the platform version used in the project. The platform artifacts will be automatically downloaded from the repository on project build. Choose `6.8.5`.
* **Root package** – the root package of Java classes.
* **Database** – the SQL database to use. Choose `HSQLDB`.
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/3_create-app.png)
4. The empty project will be created in the current directory.
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/4_create-app.png)
5. Close CLI or open new terminal window. Run `./gradlew assemble`
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/5_gradlew-assemble.png)
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/6_gradlew-assemble.png)
6. Run `./gradlew startDb` to start the local HyperSQL server.
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/7_gradlew-startDb.png)
7. Run `./gradlew createDb` to create a database.
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/8_gradlew-createDb.png)
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/9_gradlew-createDb.png)
8. Run `./gradlew setupTomcat deploy start`.
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/10_gradlew-start.png)
9. In your browser go to http://localhost:8080/app

The username and password are admin / admin.

### 3. Importing project into IDE

1. Open IntelliJ IDEA
2. File -> Open, navigate to project directory, choose `build.gradle`, press `OK`.
3. In gradle settings choose `Use gradle 'wrapper' task configuration`.
4. Press `OK`.

### 4. Creating entities

1. In terminal navigate to project directory.
2. Start CUBA CLI.
3. Enter `entity`. You will be asked the following questions:
* **Entity name** – entity class name. Enter `Customer`.
* **Package name** – entity class package name. Accept default.
* **Entity type** – entity may be Persistent, Persistent embedded or Not Persistent. Choose Persistent to make the entity able to be saved in the database.
 ![Start CUBA CLI](https://github.com/cuba-platform/cuba-cli/blob/master/screenshots/11_cuba-cli_entity.png)
5. Let's add some fields. Open the created class in your IDE.
Add the following field and methods:
```java
@Column(name = "NAME")
protected String name;

public void setName(String name) {
    this.name = name;
}

public String getName() {
    return name;
}
```
6. Now let's add SQL scripts to create the entity table.
Create a file `modules/core/db/init/hsql/10.create-db.sql` with the content
```sql
-- begin SALES_CUSTOMER
create table SALES_CUSTOMER (
    ID varchar(36) not null,
    VERSION integer not null,
    CREATE_TS timestamp,
    CREATED_BY varchar(50),
    UPDATE_TS timestamp,
    UPDATED_BY varchar(50),
    DELETE_TS timestamp,
    DELETED_BY varchar(50),
    --
    NAME varchar(255),
    --
    primary key (ID)
)^
-- end SALES_CUSTOMER
```
Also, create a file with name `modules/core/db/update/hsql/{yy}/{yymmdd}-createCustomer.sql` with the same content.
You can read more about create and update scripts on [official documentation](https://doc.cuba-platform.com/manual-6.9/db_scripts.html).

7. Run `./gradlew updateDb` to create the table for the `Customer` entity.