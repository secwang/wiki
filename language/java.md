<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [java genenic](#java-genenic)
- [junit useage](#junit-useage)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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


