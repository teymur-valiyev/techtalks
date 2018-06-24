

```
maven help:effective-pom
```


maven inheritance 
use parent tag for inheritance

profiles for different enviroment
```
<profiles>
	<profile>
		<id>development</id>
		<build>
			<directory>target/development</directory>
		</build>
	</profile>
</profiles>	
```

apply profile

mvn -Pdevelopment package

for not add -Pdevelopment you can use activation node


```
<profiles>
	<profile>
		<id>development</id>
		<activation>
			<property>
				<name>env.PACKAGE_ENV</name>
				<value>DEV</value>
			</property>
		<activation>
		<build>
			<directory>target/development</directory> 
		</build>
	</profile>
</profiles>	
```

```
mvn dependency:copy-dependencies
```

dependency scope 

```
<scope>compile</scope>
```

it add java classpath dependencies by life cycles

provider - scope except dependency will be avilable build test  phases but not for deploy web app jar
example servlet api we need for compile time 

runtime - is needed we execute system or test application not use for  compile
system - dependency will be provided by filesystem path for jar 


goal if boud yo life cycle
  
```
mvn clean
```

clean phases clean lifecycle


we have build cycles (basically, set of actions for a specific overall goal), which consist of phases (lower granularity, a cycle step), which can invoke a set of configured goals provided by certain plugins

Maven build lifecycle
* default
* clean
* site

phases


There are three built-in build lifecycles: default, clean and site. The default lifecycle handles your project deployment, the clean lifecycle handles project cleaning, while the site lifecycle handles the creation of your project's site documentation.

A Build Lifecycle is Made Up of Phases

a build phase represents a stage in the lifecycle.


* validate - validate the project is correct and all necessary information is available
* compile - compile the source code of the project
* test - test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
* package - take the compiled code and package it in its distributable format, such as a JAR.
* verify - run any checks on results of integration tests to ensure quality criteria are met
* install - install the package into the local repository, for use as a dependency in other projects locally
* deploy - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.


```
mvn install
```

This command executes each default life cycle phase in order (validate, compile, package, etc.), before executing install. You only need to call the last build phase to be executed, in this case, install:

A Build Phase is Made Up of Plugin Goals

A plugin goal represents a specific task

The clean and package arguments are build phases, 
while the dependency:copy-dependencies is a goal (of a plugin).



The first, and most common way, is to set the packaging for your project via the equally named POM element <packaging>. Some of the valid packaging values are jar, war, ear and pom. If no packaging value has been specified, it will default to jar.


Each packaging contains a list of goals to bind to a particular phase.


process-resources	resources:resources
compile	compiler:compile
process-test-resources	resources:testResources
test-compile	compiler:testCompile
test	surefire:test
package	jar:jar
install	install:install
deploy	deploy:deploy


Plugins
The second way to add goals to phases is to configure plugins in your project
```
 <plugin>
   <groupId>com.mycompany.example</groupId>
   <artifactId>display-maven-plugin</artifactId>
   <version>1.0</version>
   <executions>
     <execution>
       <phase>process-test-resources</phase>
       <goals>
         <goal>time</goal>
       </goals>
     </execution>
   </executions>
 </plugin>
```




If you have several Maven projects, and they all have similar configurations, you can refactor your projects by pulling out those similar configurations and making a parent project. Thus, all you have to do is to let your Maven projects inherit that parent project, and those configurations would then be applied to all of them.

And if you have a group of projects that are built or processed together, you can create a parent project and have that parent project declare those projects as its modules. By doing so, you'd only have to build the parent and the rest will follow.


Properties
You are also able to reference any properties defined in the project as a variable. Consider the following example
```
<project>
  ...
  <properties>
    <mavenVersion>2.1</mavenVersion>
  </properties>
  <dependencies>
    <dependency>
      <groupId>org.apache.maven</groupId>
      <artifactId>maven-artifact</artifactId>
      <version>${mavenVersion}</version>
    </dependency>
    <dependency>
      <groupId>org.apache.maven</groupId>
      <artifactId>maven-project</artifactId>
      <version>${mavenVersion}</version>
    </dependency>
  </dependencies>
  ...
</project>
```

The dependency management section is a mechanism for centralizing dependency information. When you have a set of projects that inherits a common parent it's possible to put all information about the dependency in the common POM and have simpler references to the artifacts in the child POMs. 


the minimal set of information for matching a dependency reference against a dependencyManagement section is actually {groupId, artifactId, type, classifier}.
since the default for the type field is jar, and the default classifier is null.


<build> element.
Using the <executions> Tag

```
/**
 * @goal query
 * @phase package
 */
```

```
<project>
  ...
  <build>
    <plugins>
      <plugin>
        <artifactId>maven-myquery-plugin</artifactId>
        <version>1.0</version>
        <executions>
          <execution>
            <id>execution1</id>
            <phase>install</phase>
            <configuration>
              <url>http://www.bar.com/query</url>
              <timeout>15</timeout>
              <options>
                <option>four</option>
                <option>five</option>
                <option>six</option>
              </options>
            </configuration>
            <goals>
              <goal>query</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
  ...
</project>
```

Using the <inherited> Tag In Build Plugins
By default, plugin configuration should be propagated to child POMs, so to break the inheritance, you could uses the <inherited> tag:


```
<project>
  ...
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-antrun-plugin</artifactId>
        <version>1.2</version>
        <inherited>false</inherited>
        ...
      </plugin>
    </plugins>
  </build>
  ...
</project>
```


In the parent POM, the main difference between the <dependencies> and <dependencyManagement> is this:

Artifacts specified in the <dependencies> section will ALWAYS be included as a dependency of the child module(s).

Artifacts specified in the <dependencyManagement> section, will only be included in the child module if they were also specified in the <dependencies> section of the child module itself. Why is it good you ask? because you specify the version and/or scope in the parent, and you can leave them out when specifying the dependencies in the child POM.


pluginManagment - for changing default plugin behavior



jar plugin 

configuration 
	excludes exclude name of file that will not be include in jar

```
<configuration>
	<excludes>
		<exclude>**/ExcludeMe.class</exclude>
	</excludes>
</configuration>
```


<dirtributionManagment> -- for remote repository storage

```
mvn archetype:create-from-project
```












