---
title: "java"
date: 2016-08-21 08:00
---
[TOC]

# java genenic
```
public <T> T getService(Class<T> serviceClass)
{
    ...
}
```

# junit useage 

```
    <plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-dependency-plugin</artifactId>
	<executions>
	    <execution>
		<id>copy-dependencies</id>
		<phase>prepare-package</phase>
		<goals>
		    <goal>copy-dependencies</goal>
		</goals>
		<configuration>
		    <outputDirectory>${project.build.directory}/lib</outputDirectory>
		    <overWriteReleases>false</overWriteReleases>
		    <overWriteSnapshots>false</overWriteSnapshots>
		    <overWriteIfNewer>true</overWriteIfNewer>
		</configuration>
	    </execution>
	</executions>
    </plugin>

    mvn dependency:copy-dependencies 
    java -Djava.ext.dirs=dependency -cp .:classes  org.junit.runner.JUnitCore classfullname 
```


