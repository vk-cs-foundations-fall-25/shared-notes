# Building and Packaging Software

## What is a Build Tool?

A build tool automates the process of:
- Compiling source code
- Managing dependencies
- Running tests
- Creating deployable artifacts (JARs, WARs, etc.)
- Cleaning up build artifacts
- Documenting code

## Why Build Tools?
- **Build changes only**: only need to recompile the changed files (small number), not all the files (large number) in the project
- **Reduce errors**: Repeatedly typing compilation commands leads to mistakes
- **Manage complex dependencies**: Modern software has multiple source files, libraries, and resources
- **Reproducibility**: Everyone on the team needs to build the same way
- **Automation**: Build, test, package, and deploy with single commands
- **Consistency**: Same process in development, testing, and production environments

## Build Tool Choice

- Common ones:
  - **Make** (1976): uses shell commands
    - OG!
  - **Ant** (2000): XML, primarily used for Java
  - **Apache Maven** (2004): Project Object Model (POM)
  - **Gradle** (2012): domain-specific language

- Our choice: **Ant**
  - Why?
    - Simple and clear
    - Uses standard XML (instead of domain-specific language)
  - Acronym (backronym): "Another Neat Tool"


## Ant Fundamentals

### Basic Structure of build.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="ProjectName" default="compile" basedir=".">
    <!-- Properties -->
    <!-- Targets -->
    <!-- Tasks -->
</project>
```

**Key elements:**
- `<project>`: Root element
  - `name`: Project name
  - `default`: Default target to execute
  - `basedir`: Base directory (usually ".")

---

## Ant Concepts

### Targets
- **Definition**: Named collection of tasks (like a method/function)
- **Dependencies**: Targets can depend on other targets
- **Execution**: Ant ensures dependencies run first, only once

```xml
<target name="compile" depends="init">
    <!-- compilation tasks -->
</target>
```

### Tasks
- **Definition**: Units of work (copy files, compile code, create JARs)
- **Built-in**: Ant provides many tasks
- **Custom**: Can write your own in Java

### Properties
- **Definition**: Variables that hold values
- **Immutable**: Once set, cannot be changed
- **Usage**: `${property.name}`

```xml
<property name="src.dir" value="src"/>
<property name="build.dir" value="build"/>
```

## Common Directory Structure

```
project/
├── build.xml
├── src/
│   └── com/
│       └── example/
│           └── Main.java
├── lib/
│   └── external-library.jar
├── build/
│   └── classes/
│       └── com/
│           └── example/
│               └── Main.class
└── dist/
    └── myproject.jar
```

**Conventions:**
- `src/`: Source code
- `lib/`: External libraries
- `build/`: Compiled classes (temporary)
- `dist/`: Distributable artifacts

## Essential Ant Tasks

### Directory Management

```xml
<target name="init">
    <mkdir dir="${build.dir}"/>
    <mkdir dir="${dist.dir}"/>
</target>

<target name="clean">
    <delete dir="${build.dir}"/>
    <delete dir="${dist.dir}"/>
</target>
```

### Compilation

```xml
<target name="compile" depends="init">
    <javac srcdir="${src.dir}" 
           destdir="${build.dir}"
           includeantruntime="false">
        <classpath>
            <fileset dir="${lib.dir}">
                <include name="*.jar"/>
            </fileset>
        </classpath>
    </javac>
</target>
```

**Key attributes:**
- `srcdir`: Source directory
- `destdir`: Destination for .class files
- `includeantruntime`: Whether to include Ant runtime in classpath

## Creating JAR Files

### Basic JAR Task

```xml
<target name="jar" depends="compile">
    <jar destfile="${dist.dir}/${ant.project.name}.jar" 
         basedir="${build.dir}">
        <manifest>
            <attribute name="Main-Class" 
                      value="com.example.Main"/>
        </manifest>
    </jar>
</target>
```

**Manifest attributes:**
- `Main-Class`: Entry point for executable JARs
- `Class-Path`: External dependencies
- `Implementation-Version`: Version number

### Including Libraries

```xml
<target name="jar-with-libs" depends="compile">
    <jar destfile="${dist.dir}/${ant.project.name}.jar" 
         basedir="${build.dir}">
        <manifest>
            <attribute name="Main-Class" value="com.example.Main"/>
        </manifest>
        <!-- Include library contents -->
        <zipgroupfileset dir="${lib.dir}" includes="*.jar"/>
    </jar>
</target>
```

## Complete Build File Example

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="Calculator" default="jar" basedir=".">
    
    <!-- Properties -->
    <property name="src.dir" value="src"/>
    <property name="build.dir" value="build"/>
    <property name="dist.dir" value="dist"/>
    <property name="lib.dir" value="lib"/>
    
    <!-- Initialize directories -->
    <target name="init">
        <mkdir dir="${build.dir}"/>
        <mkdir dir="${dist.dir}"/>
        <echo message="Building ${ant.project.name}..."/>
    </target>
    
    <!-- Clean build artifacts -->
    <target name="clean">
        <delete dir="${build.dir}"/>
        <delete dir="${dist.dir}"/>
        <echo message="Cleaned build directories"/>
    </target>
    
    <!-- Compile source code -->
    <target name="compile" depends="init">
        <javac srcdir="${src.dir}" 
               destdir="${build.dir}"
               includeantruntime="false"
               debug="true"
               deprecation="true">
            <classpath>
                <fileset dir="${lib.dir}">
                    <include name="**/*.jar"/>
                </fileset>
            </classpath>
        </javac>
        <echo message="Compilation complete"/>
    </target>
    
    <!-- Create JAR file -->
    <target name="jar" depends="compile">
        <jar destfile="${dist.dir}/${ant.project.name}.jar" 
             basedir="${build.dir}">
            <manifest>
                <attribute name="Main-Class" 
                          value="com.example.Calculator"/>
                <attribute name="Implementation-Version" 
                          value="1.0"/>
            </manifest>
        </jar>
        <echo message="JAR created: ${dist.dir}/${ant.project.name}.jar"/>
    </target>
    
    <!-- Run the application -->
    <target name="run" depends="jar">
        <java jar="${dist.dir}/${ant.project.name}.jar" 
              fork="true"/>
    </target>
    
    <!-- Full rebuild -->
    <target name="rebuild" depends="clean,jar"/>
    
</project>
```

## Path Structures and Classpaths

### Defining Paths

```xml
<!-- Define reusable classpath -->
<path id="compile.classpath">
    <fileset dir="${lib.dir}">
        <include name="**/*.jar"/>
    </fileset>
    <pathelement location="${build.dir}"/>
</path>

<!-- Use the classpath -->
<target name="compile">
    <javac srcdir="${src.dir}" destdir="${build.dir}">
        <classpath refid="compile.classpath"/>
    </javac>
</target>
```

**Benefits:**
- Reusability across targets
- Cleaner, more maintainable build files
- Easier to modify dependencies

## Filesets and Pattern Matching

### Filesets
Collections of files based on patterns:

```xml
<fileset dir="${src.dir}">
    <include name="**/*.java"/>
    <exclude name="**/*Test.java"/>
</fileset>
```

**Patterns:**
- `*`: Matches zero or more characters
- `**`: Matches zero or more directories
- `?`: Matches exactly one character

### Copy Task with Filesets

```xml
<target name="copy-resources">
    <copy todir="${build.dir}">
        <fileset dir="${src.dir}">
            <include name="**/*.properties"/>
            <include name="**/*.xml"/>
        </fileset>
    </copy>
</target>
```

## Target Dependencies

### Simple Dependencies

```xml
<target name="jar" depends="compile">
    <!-- JAR tasks -->
</target>

<target name="compile" depends="init">
    <!-- Compile tasks -->
</target>

<target name="init">
    <!-- Initialization tasks -->
</target>
```

**Execution order:** init → compile → jar

### Multiple Dependencies

```xml
<target name="dist" depends="jar,docs,test">
    <!-- Distribution tasks -->
</target>
```

### Conditional Execution

```xml
<target name="compile-if-needed" depends="init" 
        unless="compile.not.needed">
    <javac srcdir="${src.dir}" destdir="${build.dir}"/>
</target>
```

**Conditions:**
- `if`: Execute only if property is set
- `unless`: Execute only if property is NOT set

## Best Practices

### 1. Use Properties for All Paths
```xml
<!-- Good -->
<property name="src.dir" value="src"/>
<javac srcdir="${src.dir}" .../>

<!-- Avoid -->
<javac srcdir="src" .../>
```

### 2. Provide a Clean Target
Always allow users to start fresh:
```xml
<target name="clean">
    <delete dir="${build.dir}"/>
    <delete dir="${dist.dir}"/>
</target>
```

### 3. Set a Sensible Default Target
```xml
<project name="MyApp" default="jar" basedir=".">
```

### 4. Add Echo Messages
Help users understand what's happening:
```xml
<echo message="Compiling ${ant.project.name}..."/>
```

### 5. Use Target Dependencies
Don't duplicate tasks; use dependencies:
```xml
<!-- Good -->
<target name="jar" depends="compile">

<!-- Avoid duplicating compile tasks in multiple targets -->
```

### 6. Document Your Build File
```xml
<!-- Compile all Java source files to the build directory -->
<target name="compile" depends="init" 
        description="Compile source code">
    ...
</target>
```

## Running Ant

### Command-Line Usage

```bash
# Run default target
ant

# Run specific target
ant compile

# Run multiple targets
ant clean jar

# Set property from command line
ant -Dversion=2.0 jar

# Use different build file
ant -f mybuild.xml

# List all targets
ant -projecthelp

# Verbose output
ant -v compile

# Debug output
ant -d compile
```

## Standard Build Lifecycle

```xml
<target name="clean"/>
<target name="init" depends="clean"/>
<target name="compile" depends="init"/>
<target name="test" depends="compile"/>
<target name="jar" depends="test"/>
<target name="dist" depends="jar"/>
```

## Debugging Build Issues

### Common Problems

**1. ClassNotFoundException**
- Check classpath configuration
- Verify all JARs are included
- Ensure Main-Class is correct in manifest

**2. Files Not Found**
- Verify directory properties
- Check basedir setting
- Use absolute paths for debugging

**3. Outdated Classes**
- Run clean target
- Check file timestamps
- Verify destdir is correct

### Debugging Techniques

```xml
<!-- Print property values -->
<echo message="Source directory: ${src.dir}"/>
<echo message="Build directory: ${build.dir}"/>

<!-- List files being processed -->
<fileset dir="${src.dir}" id="source.files">
    <include name="**/*.java"/>
</fileset>
<pathconvert refid="source.files" property="source.list"/>
<echo message="Files to compile: ${source.list}"/>
```

## Summary

### Key Takeaways
1. **Build automation** is essential for modern software development
2. **Ant** uses XML-based configuration for platform-independent builds
3. **Targets** organize build steps; **tasks** perform actual work
4. **Properties** make build files flexible and maintainable
5. **JAR files** package compiled code for distribution
6. **Dependencies** between targets ensure correct build order
7. **Best practices** lead to maintainable build systems

### When to Use Ant
- **Legacy projects** already using Ant
- **Custom build processes** requiring fine-grained control
- **Learning** build automation concepts
- **Simple projects** without complex dependency management

### Modern Alternatives
- **Maven**: Dependency management, convention over configuration
- **Gradle**: Flexible, powerful, uses Groovy/Kotlin DSL
- **Build tools** continue to evolve; understand the concepts!

## Further Reading

- Apache Ant Manual: https://ant.apache.org/manual/
- JAR File Specification: https://docs.oracle.com/javase/tutorial/deployment/jar/
- Build Automation Patterns
- Continuous Integration practices

---


