# SoFi Checks

This repository is a place to put config files related to code and programming style checks.

Currently this supports both Java and Scala configurations, but it could conceivably also include configs for other languages and tools like PMD and findbugs.

### Java ###

This includes IDE (both IntelliJ and Eclipse) and checkstyle configs for java (see [the checkstyle documentation](http://checkstyle.sourceforge.net/)).

### Scala ###

Currently this only includes scalastyle configs (see [the scalastyle documentation](http://www.scalastyle.org/))


## Usage  

### Checkstyle
To use the checkstyle configs contained in this repository, add the [sbt-checkstyle-plugin plugin](https://github.com/etsy/sbt-checkstyle-plugin) to your project, using the latest version of checkstyle:

```
addSbtPlugin("com.etsy" % "sbt-checkstyle-plugin" % "3.0.0")

dependencyOverrides += "com.puppycrawl.tools" % "checkstyle" % "7.7"
```

Then to use a particular config reference it's URL in your config location:
```
checkstyleConfigLocation :=
  CheckStyleConfigLocation.URL("https://raw.githubusercontent.com/SocialFinance/sofi-checks/master/checks/java/checkstyle-config.xml")
```
To have checkstyle run as part of the compile and fail on style errors add the following to the build.sbt
```
checkstyleSeverityLevel := Some(CheckstyleSeverityLevel.Error)
(checkstyle in Compile) <<= (checkstyle in Compile) dependsOn (compile in Compile)
```

### Scalastyle

To check coding style for scala use the [scalastyle plugin](http://www.scalastyle.org/)
Add the following to the project/plugins.sbt file
```
//Scalastyle plugin
addSbtPlugin("org.scalastyle" %% "scalastyle-sbt-plugin" % "1.0.0")
```

And the configuration goes in the build.sbt
```
(scalastyleConfigUrl in Compile) := Some(url("https://raw.githubusercontent.com/SocialFinance/sofi-checks/master/checks/scala/checkstyle/scalastyle-config.xml"))
```

You can configure the plugin to run automatically as part of the compile process by adding to build.sbt
```
scalastyleFailOnError := true
lazy val compileScalastyle = taskKey[Unit]("compileScalastyle")
compileScalastyle := scalastyle.in(Compile).toTask("").value
(compile in Compile) := (compile in Compile dependsOn compileScalastyle).value
```

## Ide-Style
In the ide-style directory there are code style configurations for both IntelliJ and eclipse. These can be imported into the ide to setup the code style and formatting to match SoFi's code style. 

### IntelliJ
The location to import the code style in IntelliJ is at Preferences -> Editor -> Code Style. Using the gear icon you can import from an exiting file and either update your current scheme or add a new one. The configuration file provided has sections for each langauge

### Eclipse
The location in Eclipse to import a code style is located at Preferences -> Java -> Code Style -> Formatter. You can import the xml file provided to either your current formatter or add a new one.

## Questions

Field questions and complaints to Bridger Howell (bhowell@sofi.org) or Kent Pilkington (kpilkington@sofi.org).
