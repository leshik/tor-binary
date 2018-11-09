# Tor Binary files

Package Tor files from [Tor Browser project](https://github.com/TheTorProject/gettorbrowser) in a way that can use by any java projects



# Install

require GPG and 7Zip installed

```apt-get install -y p7zip-full```

run ```maven install -Drevision=your-tor-version-here```

This project verify GPG signature, unpack Tor Browser and package TOR binary for each platform.


# Usage

In order to integrate this package into your maven project, you have to add
```
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-antrun-plugin</artifactId>
                <version>1.8</version>
                <dependencies>
                    <dependency>
                        <groupId>org.apache.ant</groupId>
                        <artifactId>ant-compress</artifactId>
                        <version>1.4</version>
                    </dependency>
                </dependencies>
                <executions>
                    <execution>
                        <id>fetch tor-binaries</id>
                        <phase>generate-resources</phase>
                        <configuration>
                            <target>
                                <taskdef resource="org/apache/ant/compress/antlib.xml"
                                         classpathref="maven.plugin.classpath"/>

                                <get
                                    src="https://github.com/JesusMcCloud/tor-binary/archive/master.zip"
                                    dest="${project.build.directory}/tor-binary.zip"
                                    skipexisting="true"/>

                                <unzip src="${project.build.directory}/tor-binary.zip" dest="${project.build.directory}/"/>

                                <exec dir="${project.build.directory}/tor-binary-master/" executable="mvn" failonerror="true">
                                    <arg line="install -Drevision=${tor-binary.version}"/>
                                </exec>
                            </target>
                        </configuration>
                        <goals>
                            <goal>run</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
```
to your pom.xml. Note the `${tor-binary.version}` property!

Tor binary are simple zip files:

```
<dependency>
    <groupId>com.cedricwalter</groupId>
    <artifactId>tor-binary-linux32</artifactId>
    <version>7.0.6</version>
    <type>tar.xz</type>
    <classifier>bin</classifier>
</dependency>
```
```
<dependency>
    <groupId>com.cedricwalter</groupId>
    <artifactId>tor-binary-linux64</artifactId>
    <version>7.0.6</version>
    <type>tar.xz</type>
    <classifier>bin</classifier>
</dependency>
```
```
<dependency>
    <groupId>com.cedricwalter</groupId>
    <artifactId>tor-binary-macos</artifactId>
    <version>7.0.6</version>
    <type>tar.xz</type>
    <classifier>bin</classifier>
</dependency>
```
```
<dependency>
    <groupId>com.cedricwalter</groupId>
    <artifactId>tor-binary-windows</artifactId>
    <version>7.0.6</version>
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
                        <version>${tor-binary.version}</version>
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
