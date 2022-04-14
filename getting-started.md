# Getting Started

## Prerequisites
Since this library is based on Java programming language, you may install tools below :
- JDK 8
- Maven
- IDE of your choice (IntelliJ IDEA, etc.)
- Appium desktop

## Setting up
Open `pom.xml` of the Maven project that you want to have Tetikus set up, then insert this code snippet inside `<project>` element to be able to fetch dependencies from JitPack.
```xml
<repositories>
        <repository>
            <id>jitpack.io</id>
            <url>https://jitpack.io</url>
        </repository>
</repositories>
```

Then insert Tetikus dependency inside `<dependencies>` element. You may adjust the version based on the latest version released on the Github page.
```xml
<dependency>
    <groupId>com.github.ubaifadhli</groupId>
    <artifactId>tetikus-core</artifactId>
    <version>0.2.1</version>
</dependency>
```