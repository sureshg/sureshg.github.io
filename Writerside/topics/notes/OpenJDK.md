# OpenJDK

<primary-label ref="Java"/>
<secondary-label ref="JVM"/>
<secondary-label ref="KT"/>

### Java Commands

##### 1. Create Source Code Structure

```bash
$ mkdir -p src/{main,test}/{java,resources}
```

##### 2. Preview features

```bash
$ javac --enable-preview -release 24 Foo.java
$ java  --enable-preview Foo
```

- [JEP12](https://openjdk.java.net/jeps/12)
- [Preview Features](https://docs.oracle.com/en/java/javase/24/language/preview-language-and-vm-features.html)
- [Gradle - Enabling Java preview features](https://docs.gradle.org/current/userguide/building_java_projects.html#sec:feature_preview)

##### 3. Java Platform Module Systems (JPMS)

```bash
$ java --list-modules
$ java --describe-module java.se
$ java --show-module-resolution java.base

# Replace upgradeable modules in the runtime image
$ java --upgrade-module-path $DIR
```

- [Java Compiler Upgradeable module]( https://docs.oracle.com/en/java/javase/24/docs/api/java.compiler/module-summary.html)

##### 4. Disassembles a class

```bash
$ javap -p -v <classfile>

# Show the class version
$ javap -p -v build.classes.kotlin.main.App | grep version
```

- **[Javap Pastebin](https://javap.yawk.at/)**

##### 5. App CDS

```bash
# Before JDK 18
if [ ! -f app.jsa ]; then
  java -XX:ArchiveClassesAtExit=app.jsa -jar app.jar
else
  java -XX:ShareArchiveFile=app.jsa -jar app.jar
fi

# Since JDK 19, auto generate the CDS archive
$ java -XX:+AutoCreateSharedArchive -XX:SharedArchiveFile=app.jsa -jar app.jar

# Create default CDS archive
$ jlink-runtime/java -Xshare:dump [-XX:-UseCompressedOops]
# Check if it worked, this will fail if it can't map the archive (lib/server/classes.jsa)
$ jlink-runtime/java -Xshare:on --version
```

- https://ionutbalosin.com/2022/04/application-dynamic-class-data-sharing-in-hotspot-jvm
- https://dev.java/learn/class-data-sharing-and-application-class-data-sharing-in-hotspot
- https://mbien.dev/blog/entry/custom-java-runtimes-with-jlink

##### 6. Show Java VMProperty Settings

```bash
$ java --version
$ java -Xinternalversion

# Show Java Version (Useful for shell scripts)
$ java -XshowSettings:properties -version 2>&1 | grep "java.specification.version =" | awk '{print $3}'
$ jshell --feedback=silent -  <<< 'System.out.println(System.getProperty("java.specification.version"))'

# Show all settings
$ java -XshowSettings:all --version

# Show all Javac linter options
$ javac --help-lint

# Show all system properties
$ java -XshowSettings:properties --version

# VM extra options
$  java -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+PrintFlagsFinal --version

# Java JIT compiler options
$ java -Xcomp            forces compilation of methods on first invocation (slow startup)
$ java -Xint             interpreted mode execution only (fast startup)
$ java -Xmixed           mixed mode execution (default)
```

- [Java Command Options*](https://docs.oracle.com/en/java/javase/24/docs/specs/man/java.html)
- [VM Options](https://www.oracle.com/java/technologies/javase/vmoptions-jsp.html)
- [`class` file format major versions](https://docs.oracle.com/javase/specs/jvms/se20/html/jvms-4.html#jvms-4.1-200-B.2)

##### 7. Scan deprecated APIs

```bash
# Print dependency summary
$ jdeps -summary  app.jar

# Check the dependencies on JDK internal APIs
$ jdeps --jdk-internals --classpath libs.jar app.jar

# List of module dependences to be used in JLink
$ jdeps --ignore-missing-deps --print-module-deps  app.jar

# List all service providers
$ jlink --suggest-providers java.security.Provider

# List all jlink plugins
$ jlink --list-plugins

# Generate module-info
$ jdeps --generate-module-info ./  app.jar

# List all deprecated APIs for a release
$ jdeprscan --for-removal --release 24 --list

# Scan deprecated APIs
$ jdeprscan --for-removal --release 24 app.jar
```

- [Java EE Maven artifacts](https://openjdk.java.net/jeps/320)

##### 8. JPMS

```bash
# Start ModuleMainClass
$ java -m jdk.httpserver -b 127.0.0.1

# Compile all modules at once (Start from the main module)
$ javac  --enable-preview \
         --release 24 \
         -parameters  \    // Optional, Generate metadata for reflection on method parameters
         --add-modules ALL-MODULE-PATH \  // Optional, Root modules to resolve in addition to the initial modules
         --module-path ... \           // Optional, where to find application modules
         --module-source-path "src" \  // Source files for multiple modules
         -d classes  \
         --module MainApp              // Compile only the specified module(s)

# Package all modules (Create for all modules)
$ jar --create \
      --file mods/app.jar \
      --main-class dev.suresh.MainKt \
      --module-version 1.0 \    // Optional
      -C app/ classes resources // Or *.class

# Launch app
$ java  --enable-preview \
        --show-version \
        --show-module-resolution \
        --module-path mods \
        --module app   // OR <module>/<mainclass>

# Build native image from modular jars
$ native-image \
    -p base-module.jar:main-module.jar \
    -m dev.suresh.Main

# JavaFX 24 using jlink & jpackage
$ wget "https://download.java.net/java/early_access/.../openjfx-xxx_macos-aarch64_bin-jmods.tar.gz"
$ tar -xvzf openjfx-xxx_macos-aarch64_bin-jmods.tar.gz

$ jlink --output javafx-jdk \
        --module-path $JAVA_HOME/jmods:javafx-jmods-24 \
        --add-modules javafx.controls,java.desktop,java.logging
#       --add-modules ALL-MODULE-PATH

$ javafx-jdk/bin/java --list-modules

$ jpackage --main-jar app.jar \
           --runtime-image javafx-jdk \
           --type app-image \
           --name app \
           --java-options "-Xmx64m" \
           --arguments "arg" \
           --icon app.ico \
           --input app \
           --dest bin
```

- [JPMS Quickstart](https://openjdk.java.net/projects/jigsaw/quick-start)
- [Docs and Resources](https://openjdk.java.net/projects/jigsaw/)
- [**Java Modules Cheat Sheet**](https://nipafx.dev/build-modules/)
- [JPackage Scripts](https://github.com/dlemmermann/JPackageScriptFX)

##### 9. JShell

```bash
# JShell with preview feature enabled
$ jshell --enable-preview
$ jshell --show-version --enable-preview  --enable-native-access --startup JAVASE --feedback concise

# Use custom startup script
$ jshell --enable-preview --startup DEFAULT --startup ~/calc.repl

# Query system properties/run java code
$ fileEncoding="$(echo 'System.out.println(System.getProperty("file.encoding"))' | jshell -s -)"
```

##### 10. Java TEMP Config

  ```bash
  $ echo "-------- TMP PATH for $OSTYPE --------"
  $ MKTEMP_PATH="$(dirname "$(mktemp -u)")/"
  $ JAVA_TMP_DIR="$(java -XshowSettings:properties -version 2>&1 | awk 'tolower($0) ~ /java.io.tmpdir/{print $NF}')/"
  $ JAVA_FILE_ENC="$(echo 'System.out.println(System.getProperty("file.encoding"))' | jshell -s -)"

  $ echo "MKTEMP_PATH    = $MKTEMP_PATH"
  $ echo "TMP            = $TMP"
  $ echo "TEMP           = $TEMP"
  $ echo "TMPDIR (Mac)   = $TMPDIR"
  $ echo "RUNNER_TEMP    = $RUNNER_TEMP"
  $ echo "JAVA_IO_TMPDIR = $JAVA_TMP_DIR"
  $ echo "JAVA_FILE_ENC  = $JAVA_FILE_ENC"
  $ echo "/TMP           = $(ls -l /tmp)"
  ```

### IDEs and Tools

- IntelliJ Selection Modes

    - All Actions - <kbd>CMD</kbd> + <kbd>SHIFT</kbd> + <kbd>A</kbd>

    - Select all occurrences - <kbd>CMD</kbd> + <kbd>CTRL</kbd> + <kbd>G</kbd>

    - Column selection mode - <kbd>CMD</kbd> + <kbd>SHIFT</kbd> + <kbd>8</kbd>

    - Multiple Cursors - <kbd>SHIFT</kbd> + <kbd>ALT</kbd> + <kbd>Left Click</kbd>

    - Multi Selection - <kbd>SHIFT</kbd> + <kbd>ALT</kbd> + Select as usual

    - Caret Cloning - <kbd>SHIFT</kbd> + <kbd>ALT</kbd> + Middle click on end line

    - Move line - <kbd>SHIFT</kbd> + <kbd>ALT</kbd> + <kbd>Arrow UP/DOWN</kbd>


- Plugin Version Update

  ```bash
  $ PLUGIN_VERSION="1.2.6.2594"
  $ wget --content-disposition "https://plugins.jetbrains.com/plugin/download?rel=true&updateId=331908"
  $ unzip github-copilot-intellij-${PLUGIN_VERSION}.zip
  $ cd github-copilot-intellij/lib
  $ jar -tvf github-copilot-intellij-${PLUGIN_VERSION}.jar | grep plugin.xml
  $ unzip github-copilot-intellij-${PLUGIN_VERSION}.jar
  # Change until-build="223.*"
  $ vi META-INF/plugin.xml
  $ zip -r github-copilot-intellij-${PLUGIN_VERSION}.jar META-INF
  $ rm -rf META-INF
  $ cd ../../
  $ zip -r github-copilot-intellij-${PLUGIN_VERSION}.zip github-copilot-intellij/
  $ rm -rf github-copilot-intellij

  # Now upload github-copilot-intellij-${PLUGIN_VERSION}.zip (Preferences -> Plugins -> ⚙️ -> Install Plugin from Disk)
  ```


* IntelliJ Plugin Channels

    * https://plugins.jetbrains.com/plugins/beta/list
    * https://plugins.jetbrains.com/plugins/snapshots/org.jetbrains.compose.desktop.ide

### Networking & Security

[🚨Security Developer’s Guide](https://docs.oracle.com/en/java/javase/24/security/index.html)

##### 1. [Allow Unsafe Server Cert Change](https://github.com/openjdk/jdk/blob/6a905b6546e288e86322ae978a1f594266aa368a/src/java.base/share/classes/sun/security/ssl/ClientHandshakeContext.java#L35-L76)

```bash
# This is Unsafe. Don't use in prod.
-Djdk.tls.allowUnsafeServerCertChange=true
-Dsun.security.ssl.allowUnsafeRenegotiation=true
```

##### 2. Debugging TLS

- https://docs.oracle.com/en/java/javase/24/security/java-secure-socket-extension-jsse-reference-guide.html#GUID-4D421910-C36D-40A2-8BA2-7D42CCBED3C6
- https://docs.oracle.com/en/java/javase/24/security/java-secure-socket-extension-jsse-reference-guide.html
- https://github.com/sureshg/InstallCerts/blob/master/src/main/kotlin/io/github/sureshg/extn/Certs.kt

  ```bash
  # Turn on all debugging
  $ java -Djavax.net.debug=all

  # Override HostsFileNameService
  $ java -Djdk.net.hosts.file=/etc/host/style/file

  # Force IPv4
  $ java -Djava.net.preferIPv4Stack=true

  # The entropy gathering device can also be specified with the system property
  $ java -Djava.security.egd=file:/dev/./urandom
  ```

##### 3. Java Networking Properties

- http://htmlpreview.github.io/?https://github.com/openjdk/jdk/blob/master/src/java.base/share/classes/java/net/doc-files/net-properties.html
- https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/net/doc-files/net-properties.html
- [All Java Networking System Properties](https://docs.oracle.com/en/java/javase/24/core/java-networking.html#GUID-E6C82625-7C02-4AB3-B15D-0DF8A249CD73)
- https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html

| Config             | Description                                   |
|:-------------------|:----------------------------------------------|
| http.proxyHost     | The host name of the proxy server             |
| http.proxyPort     | The port number, the default value being `80` |
| http.nonProxyHosts |                                               |

- **HTTP**

  ```bash
  # Use JAVA_TOOL_OPTIONS
  $ export JAVA_TOOL_OPTIONS="
  ${JAVA_TOOL_OPTIONS}
  -Dhttp.useProxy=true
  -Dhttps.useProxy=true
  -Dhttp.proxyHost=172.10.10.1
  -Dhttp.proxyPort=8100
  -Dhttps.proxyHost=172.10.10.1
  -Dhttps.proxyPort=8100
  -Dhttp.nonProxyHosts='localhost|127.0.0.1|cdn.test.org|*-prod.app.com|slack.com'"

  # OR use system properties
  $ java -Dhttp.proxyHost=webcache.example.com -Dhttp.proxyPort=8080 -Dhttp.nonProxyHosts=”localhost|host.example.com” <URL>
  ```

- **Env vars**

  ```bash
  export HTTP_PROXY=http://USERNAME:PASSWORD@10.0.1.1:8080/
  export HTTPS_PROXY=https://USERNAME:PASSWORD@10.0.0.1:8080/
  export NO_PROXY=master.hostname.example.com
  ```

##### 4. [HTTP Client](https://openjdk.java.net/groups/net/httpclient/#incubatingAPI) Properties

```bash
-Djdk.internal.httpclient.disableHostnameVerification
-Djdk.httpclient.HttpClient.log=headers
-Djdk.internal.httpclient.debug=false
-Djdk.tls.client.protocols="TLSv1.2"
```

### Gradle Kotlin DSL

##### 1. Docs

- [Gradle Kotlin DSL Samples](https://github.com/gradle/kotlin-dsl-samples/tree/master/samples)
- [Gradle Kotlin DSL Primer](https://docs.gradle.org/current/userguide/kotlin_dsl.html)
- [Migrating Guide to Kotlin DSL](https://guides.gradle.org/migrating-build-logic-from-groovy-to-kotlin/)
- [Building Kotlin JVM Libraries](https://guides.gradle.org/building-kotlin-jvm-libraries/)

##### 2. [Name Abbrevation](https://docs.gradle.org/6.8/userguide/command_line_interface.html#sec:name_abbreviation)

```bash
$ ./gradlew --console=plain \
            --continuous \
            --dry-run \
            --no-daemon \
            -Dauthor=Suresh \
            -Pmyprop=myvalue \
            cle dU
```

##### 3. [Configure/Create Tasks](https://docs.gradle.org/current/userguide/kotlin_dsl.html#kotdsl:containers)

- ###### Eager

  ```kotlin
  val p: Jar = getByName<Jar>("jar")       // Get existing task
  val q: Jar = create<Jar>("jar") {}       // Create new task
  val r: Jar by getting(Jar::class)        // Get task using property delegate
  val s: Copy by creating(Copy::class) {}  // Create task using property delegate
  ```

- ###### Lazy ([Configuration Avoidance API](https://docs.gradle.org/current/userguide/task_configuration_avoidance.html))

  ```kotlin
  val t: TaskProvider<Jar> = named<Jar>("jar"){}        // Get existing task
  val u: TaskProvider<Jar> = register<Jar>("jar"){}     // Create new task
  val v: TaskProvider<Jar> by registering(Jar::class){} // Create task using property delegate
  val jar: TaskProvider<Task> by existing // Get task using property delegate

  val foo: FooTask by existing            // Take Task type from val (Kotlin 1.4)
  val bar: BarTask by registering {}      // Take Task type from val (Kotlin 1.4)
  ```

##### 4. [Reproducible builds](https://docs.gradle.org/current/userguide/working_with_files.html#sec:reproducible_archives)

```kotlin
withType<AbstractArchiveTask>().configureEach {
    isPreserveFileTimestamps = false
    isReproducibleFileOrder = true
}
```

- [reproducible-builds.org](https://reproducible-builds.org/docs/jvm/)
- https://github.com/jvm-repo-rebuild/reproducible-central

##### 5. [Multi Release Jar](https://blog.gradle.org/mrjars)

```kotlin
// See https://github.com/melix/mrjar-gradle for more on multi release jars
val mrVersion = "11"
if (JavaVersion.current().isJava11Compatible) {
    sourceSets {
        create("java$mrVersion") {
            java {
                srcDirs("src/main/java$mrVersion")
            }
        }
    }

    tasks {
        // For each source set, Gradle will automatically create a compile task.
        val mrJavaCompile = named<JavaCompile>("compileJava${mrVersion}Java") {
            sourceCompatibility = mrVersion
            targetCompatibility = mrVersion
            options.compilerArgs = listOf("--release", mrVersion)
        }

        named<Jar>("jar") {
            into("META-INF/versions/$mrVersion") {
                from(sourceSets.named("java$mrVersion").get().output)
            }
            manifest.attributes(
                "Multi-Release" to "true"
            )

            dependsOn(mrJavaCompile)
        }
    }
}
```

##### 6. Dependencies

```bash
# Direct dependencies
$ ./gradlew -q dependencies --configuration implementation
# Transitive dependencies
$ ./gradlew -q dependencies --configuration runtimeClasspath

# Dependencies insight for a dependency group.
$ ./gradlew -q dependencyInsight --configuration runtimeClasspath --dependency kotlin
$ ./gradlew -q dependencyInsight --dependency log4j-core

# Task Dependencies
$ ./gradlew clean build --dry-run

# Dependency updates
$ ./gradlew clean dependencyUpdates -Drevision=release
```

- [Refresh dependencies & Caching](https://stackoverflow.com/a/42058780/416868)

```bash
# Force Gradle to execute all tasks ignoring up-to-date checks
$ ./gradlew clean build --rerun-tasks

# Don't reuse outputs from previous builds (org.gradle.caching=false)
$ ./gradlew clean build --no-build-cache

# To refresh all dependencies in the dependency cache
$ ./gradlew clean build --refresh-dependencies
```

- [Debugging Dependencies](https://docs.gradle.org/current/userguide/viewing_debugging_dependencies.html)
- [Gradle Conflict Resolution](https://docs.gradle.org/current/userguide/dependency_resolution.html#sec:conflict-resolution)

### [Maven](https://search.maven.org/search?q=org.jetbrains.kotlin)

##### 1. [Create a Project](http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)

```bash
$ mvn archetype:generate -DgroupId=dev.suresh -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
```

##### 2. [Enabling Java preview feature](https://blog.codefx.org/java/enable-preview-language-features/#Enabling-Previews-In-Tools)

```xml

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.2</version>
            <configuration>
                <release>15</release>
                <compilerArg>--enable-preview</compilerArg>
            </configuration>
        </plugin>

        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <configuration>
                <argLine>--enable-preview</argLine>
            </configuration>
        </plugin>

        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-failsafe-plugin</artifactId>
            <configuration>
                <argLine>--enable-preview</argLine>
            </configuration>
        </plugin>
    </plugins>
</build>
```

##### 3. [Reproducible Builds](https://maven.apache.org/guides/mini/guide-reproducible-builds.html)

```xml

<properties>
    <project.build.outputTimestamp>2020-04-02T08:04:00Z</project.build.outputTimestamp>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

##### 4. [Maven Wrapper](https://maven.apache.org/wrapper/)

```bash
$ mvn wrapper:wrapper -Dmaven=3.8.5
```

##### 5. [Update Version number](http://www.mojohaus.org/versions-maven-plugin/)

```bash
$ ./mvnw versions:set -DnewVersion=1.0.1-SNAPSHOT -DprocessAllModules -DgenerateBackupPoms=false
$ ./mvnw versions:revert // Rollback
$ ./mvnw versions:commit
```

##### 6. [Dependency Tree](https://search.maven.org/search?q=fc:kotlin.text.Regex)

```bash
# Show all orginal versions, not the resolved ones.
$ ./mvnw dependency:tree
$ ./mvnw dependency:tree -Ddetail=true
$ ./mvnw dependency:tree -Dverbose -Dincludes=org.jetbrains.kotlin:kotlin-stdlib
$ ./mvnw clean verify

# Dependency and plugin updates
$ ./mvnw clean versions:display-dependency-updates versions:display-plugin-updates

# Search Artifacts by class
https://search.maven.org/search?q=fc:kotlin.text.Regex
```

### Microservices Starters

##### 1. [SpringBoot](https://start.spring.io/)

```bash
$ curl https://start.spring.io/starter.zip \
    -d dependencies=devtools,web \
    -d type=gradle-project \
    -d language=kotlin \
    -d javaVersion=11 \
    -d packaging=jar \
    -d platformVersion=2.2.6.RELEASE \
    -d name=helloworld \
    -d groupId=dev.suresh \
    -d artifactId=helloworld \
    -d packageName=dev.suresh \
    -d description=Hello%20World%20App \
    -d baseDir=helloworld \
    -o helloworld.zip
```

- [SpringBoot](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [Spring and Kotlin Docs](https://docs.spring.io/spring/docs/current/spring-framework-reference/index.html)

### Misc

- [Github Registry](https://help.github.com/en/packages/using-github-packages-with-your-projects-ecosystem/configuring-docker-for-use-with-github-packages)

  ```bash
  $ VERSION=$(date +%s)
  $ docker build . --file Dockerfile --tag docker.pkg.github.com/sureshg/repo/app:${VERSION}
  $ docker login docker.pkg.github.com --username sureshg --password ${{ secrets.GITHUB_TOKEN }}
  $ docker push docker.pkg.github.com/sureshg/repo/app:${VERSION}
  ```

- Install Command Line Tools

  ```bash
  $ xcode-select --install
  ```

### [OpenJDK Build](https://openjdk.java.net/groups/build/doc/building.html)

```bash
$ sdk install java 24-open
$ git clone https://github.com/openjdk/jdk.git
$ cd jdk
# $ make clean
$ bash configure
$ make images
$ build/*/images/jdk/bin/java --version
```

### [Oracle A1 Flex](https://cloud.oracle.com/?region=us-sanjose-1)

```bash
# Reset the password
# https://docs.oracle.com/en-us/iaas/Content/Compute/References/serialconsole.htm#four__opcpasswordreset
$ /usr/sbin/load_policy -i
$ sudo /bin/mount -o remount, rw /
$ sudo passwd opc
$ sudo reboot -f

# Install softwares
$ sudo yum upgrade -y
$ sudo yum install curl wget tree docker git zsh -y
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
$ curl -s "https://get.sdkman.io" | bash
$ sdk i java 24.ea-open

# For Github self hosted runners on Aarch64
export LD_LIBRARY_PATH=/opt/oracle/oracle-armtoolset-8/root/usr/lib64:/usr/local/lib:/usr/lib:/usr/local/lib64:/usr/lib64
export DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1
export JAVA_HOME_11_X64=/home/opc/.sdkman/candidates/java/11.0.11.hs-adpt

# Install EPEL
$ sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

* Open Ports

  ```bash
   # Networking > Virtual cloud networks > Security List > Add Ingress Rules (open tcp/8080)
   $ firewall-cmd  --permanent --zone=public --add-port=8080/tcp
   $ firewall-cmd  --reload
   $ http://ip:8080
  ```

### Awesome Svgs

##### Illustrations

- https://undraw.co/illustrations
- https://www.manypixels.co/gallery/
- https://www.pixeltrue.com/free-illustrations

##### Background

- https://www.svgbackgrounds.com/

##### Icons

- https://icons.getbootstrap.com/
- https://material.io/resources/icons/?style=baseline (not sag)
- https://fontawesome.com/v4.7.0/icons/ (not sag)
- https://simpleicons.org/ (Brand Icons - good one)
- https://github.com/microsoft/fluentui-system-icons
- https://tablericons.com/
- https://tabler-icons.io/
- https://systemuicons.com/
- https://github.com/c5inco/intellij-icons-compose
- https://www.visiwig.com/icons/
- https://standart.io/
- https://thenounproject.com/
- https://www.flaticon.com/
- https://www.iconfinder.com/
- https://ionicons.com/
- https://icons8.com/
- https://github.com/game-icons/icons

##### Emojis

- https://emojipedia.org/search/
- https://github.com/twitter/twemoji/tree/master/assets

##### Awesome List

- https://github.com/vkarampinis/awesome-icons
- https://github.com/notlmn/awesome-icons
- https://github.com/ikatyang/emoji-cheat-sheet

##### Tools

- https://jakearchibald.github.io/svgomg/
- https://css-tricks.com/tools-for-optimizing-svg/
- https://imageoptim.com/mac
- https://xmlgraphics.apache.org/batik/
- https://github.com/svg/svgo-osx-folder-action

```bash
$ pip3 install mkdocs-macros-plugin
$ ./gradlew dokka
$ cp  docs/mkdocs.yml build/dokka
$ cp -R docs/images build/dokka/my-app
$ cp CHANGELOG.md build/dokka/my-app/CHANGELOG.md
$ cp README.md build/dokka/my-app/Overview.md
$ Fix the img reference on Overview.md
$ cd build/dokka
$ mkdocs build
```
