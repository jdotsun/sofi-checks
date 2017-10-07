# SoFi Checks

This repository is a place to put config files related to code and programming style checks.

Currently this only includes checkstyle configs (see [the checkstyle documentation](http://checkstyle.sourceforge.net/)), but it could conceivably also include configs for related tools like PMD and findbugs.

## Usage

To use the checkstyle configs contained in this repository, add the [sbt-checkstyle-plugin plugin](https://github.com/etsy/sbt-checkstyle-plugin) to your project, using the latest version of checkstyle:

```
addSbtPlugin("com.etsy" % "sbt-checkstyle-plugin" % "3.0.0")

dependencyOverrides += "com.puppycrawl.tools" % "checkstyle" % "7.7"
```

Then to use a particular config reference it's URL in your config location:
```
checkstyleConfigLocation :=
  CheckStyleConfigLocation.URL("https://raw.githubusercontent.com/SocialFinance/sofi-checks/master/checks/checkstyle-config.xml")
```

## Questions

Field questions and complaints to Bridger Howell (bhowell@sofi.org).
