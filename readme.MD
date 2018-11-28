# Tor Binary files

Package native Tor files from [Tor Browser project](https://www.torproject.org/) in a way that can be uses by java projects.

# Install

require GPG installed

Change in pom to get the desired version

```<torbrowser.version>your TorBrowserBundle version here</torbrowser.version>```

run ```maven install```

alternatively, you can source jitpack.io:

Maven:
```
    <repositories>
        <repository>
            <id>jitpack.io</id>
            <url>https://jitpack.io</url>
        </repository>
        ...
    </repositories>
```

Gradle:
```
    repositories {
        maven { url 'https://jitpack.io' }
        ...
    }
```


# Usage

Tor binary are simple zip files:

```
<dependency>
    <groupId>com.github.JesusMcCloud.tor-binary</groupId>
    <artifactId>tor-binary-linux32</artifactId>
    <version>${torbrowser.version}</version>
    <type>tar.xz</type>
    <classifier>bin</classifier>
</dependency>
```
```
<dependency>
    <groupId>com.github.JesusMcCloud.tor-binary</groupId>
    <artifactId>tor-binary-linux64</artifactId>
    <version>${torbrowser.version}</version>
    <type>tar.xz</type>
    <classifier>bin</classifier>
</dependency>
```
```
<dependency>
    <groupId>com.github.JesusMcCloud.tor-binary</groupId>
    <artifactId>tor-binary-macos</artifactId>
    <version>${torbrowser.version}</version>
    <type>tar.xz</type>
    <classifier>bin</classifier>
</dependency>
```
```
<dependency>
    <groupId>com.github.JesusMcCloud.tor-binary</groupId>
    <artifactId>tor-binary-windows</artifactId>
    <version>${torbrowser.version}</version>
    <type>tar.xz</type>
    <classifier>bin</classifier>
</dependency>
```

you may want to unpack these dependencies if required using
```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-dependency-plugin</artifactId>
    <executions>
        <execution>
            <id>copy</id>
            <phase>generate-resources</phase>
            <goals>
                <goal>copy</goal>
            </goals>
            <configuration>
                <artifactItems>
                    <artifactItem>
                        <groupId>com.cedricwalter</groupId>
                        <artifactId>tor-binary-linux32</artifactId>
                        <version>${torbrowser.version}</version>
                        <type>tar.xz</type>
                        <classifier>bin</classifier>
                        <overWrite>false</overWrite>
                        <outputDirectory>${project.build.directory}/classes/native/linux/x86
                        </outputDirectory>
                        <destFileName>tor.tar.xz</destFileName>
                    </artifactItem>
                 </artifactItems>
            </configuration>
        </execution>
    </executions>
</plugin>
```
