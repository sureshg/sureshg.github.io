# Kotlin

<primary-label ref="Kotlin"/>
<secondary-label ref="JVM"/>
<secondary-label ref="OpenJDK"/>

<tldr>
 <p>
   Shortcut: <shortcut>CMD + SPACE</shortcut> 
</p>
<p>
  Configure: <ui-path>Settings | View | Edit</ui-path>
</p>
<p>Press <shortcut key="$Copy"/> to copy.</p>
</tldr>

### Kotlin Compiler Options

  ```bash
  $ kotlinc -X 2>&1 | grep -i release
  ```

### Native Image

```bash
$ sdk u java graalvm-ce-dev
$ cat > App.kt << EOF
fun main() {
  println("Hello Kotlin!")
}
EOF

# $ kotlinc -version \
#           -verbose \
#           -include-runtime \
#           -java-parameters \
#           -jvm-target 19 \
#           -Xjdk-release=19 \
#           -api-version 1.9 \
#           -language-version 2.0 \
#           -Werror \
#           -progressive \
#           App.kt -d app.jar

$ kotlinc -version -include-runtime App.kt -d app.jar
$ java -showversion -jar app.jar
$ native-image \
      --no-fallback \
      --native-image-info \
      --enable-preview \
      -jar app.jar

$ chmod +x app
$ time ./app

# Static image info
$ file app
$ otool -L app
$ objdump -section-headers  app

# Find GraalVM used to generate the image
$ strings -a app | grep -i com.oracle.svm.core.VM
```

### Videos

* https://www.youtube.com/watch?v=SEKsvHYZz8s (crypto 101)

### Samples

<icon src="kodee-loving.png" height="100" width="100"/>

```kotlin
```

{src="kotlin/App.kt" lang="kotlin" validate="true" }

<compare>
    <code-block lang="kotlin">
        if (true) {
            doThis()
        }
    </code-block>
    <code-block lang="kotlin">
        if (true) doThis()
    </code-block>
</compare>

Download <resource src="movies.csv"/>

### Misc

```mermaid
```
{ src="class.mermaid" }

##### Math

$$
\begin{equation}
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
\end{equation}
$$
