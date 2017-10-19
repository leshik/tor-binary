# Tor Binary files

Package Tor files from (Tor Browser project)[https://github.com/TheTorProject/gettorbrowser] in a way that can use by any java projects

change here to get the desired version,

This project verify GPG signature, unpack Tor Browser and package tor binary for each platform.


# Usage

```
<dependency>
    <groupId>com.cedricwalter</groupId>
    <artifactId>tor-binary-linux32</artifactId>
    <version>7.0.6</version>
    <type>zip</type>
    <classifier>bin</classifier>
</dependency>
```
```
<dependency>
    <groupId>com.cedricwalter</groupId>
    <artifactId>tor-binary-linux64</artifactId>
    <version>7.0.6</version>
    <type>zip</type>
    <classifier>bin</classifier>
</dependency>
```
```
<dependency>
    <groupId>com.cedricwalter</groupId>
    <artifactId>tor-binary-macos</artifactId>
    <version>7.0.6</version>
    <type>zip</type>
    <classifier>bin</classifier>
</dependency>
```
```
<dependency>
    <groupId>com.cedricwalter</groupId>
    <artifactId>tor-binary-windows</artifactId>
    <version>7.0.6</version>
    <type>zip</type>
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
            <phase>package</phase>
            <goals>
                <goal>copy</goal>
            </goals>
            <configuration>
                <artifactItems>
                    <artifactItem>
                        <groupId>com.cedricwalter</groupId>
                        <artifactId>tor-binary-linux32</artifactId>
                        <version>${tor-binary.version}</version>
                        <type>zip</type>
                        <classifier>bin</classifier>
                        <overWrite>false</overWrite>
                        <outputDirectory>${project.build.directory}/classes/native/linux/x86
                        </outputDirectory>
                        <destFileName>tor.zip</destFileName>
                    </artifactItem>
                 </artifactItems>
            </configuration>
```