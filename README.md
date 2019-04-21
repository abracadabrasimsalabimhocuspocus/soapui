JDK11 Linux build
=================

Check original repository for the real README.MD. 

JDK11 build fails otherwise because of:
- Dependency on internal com.sun api
- XMLBeans generates code differently on higher javaSource-versions

It works for now because:
- XMLBeans code generation is done using JDK8 with the old
  settings
- JavaFX is added the compiler args for JDK11

This should work once the JavaFX module is configured correctly:
```
$ export JAVA_HOME=~/lib/java11 PATH=~/lib/java11/bin:$PATH  ;  mvn install -P '!xmlbeans,soapui,assembly' -DskipTests
```

Remember to check the contents of the tar file, didn't bother
to fix the build including both the indy and non-indy variants
of groovy (get rid of the non indy ones)

Build log:
```
developer@debian:~/workspace/soapui$ export JAVA_HOME=~/lib/java8 PATH=~/lib/java8/bin:$PATH  ;  mvn clean install -P 'xmlbeans,!soapui' -DskipTests ; export JAVA_HOME=~/lib/java11 PATH=~/lib/java11/bin:$PATH  ;  mvn install -P '!xmlbeans,soapui,assembly' -DskipTests ;
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Build Order:
[INFO] 
[INFO] SoapUI project                                                     [pom]
[INFO] SoapUI XMLBeans                                                    [jar]
[INFO] 
[INFO] ----------------< com.smartbear.soapui:soapui-project >-----------------
[INFO] Building SoapUI project 5.6.0-kimholan                             [1/2]
[INFO] --------------------------------[ pom ]---------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ soapui-project ---
[INFO] Deleting /home/developer/workspace/soapui (includes = [*.log], excludes = [])
[INFO] 
[INFO] --- maven-install-plugin:2.4:install (default-install) @ soapui-project ---
[INFO] Installing /home/developer/workspace/soapui/pom.xml to /home/developer/.m2/repository/com/smartbear/soapui/soapui-project/5.6.0-kimholan/soapui-project-5.6.0-kimholan.pom
[INFO] 
[INFO] ----------------< com.smartbear.soapui:soapui-xmlbeans >----------------
[INFO] Building SoapUI XMLBeans 5.6.0-kimholan                            [2/2]
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ soapui-xmlbeans ---
[INFO] Deleting /home/developer/workspace/soapui/soapui-xmlbeans/target
[INFO] Deleting /home/developer/workspace/soapui/soapui-xmlbeans (includes = [*.log], excludes = [])
[INFO] 
[INFO] --- xmlbeans-maven-plugin:2.3.3:xmlbeans (default) @ soapui-xmlbeans ---
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ soapui-xmlbeans ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 435 resources
[INFO] Copying 5413 resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.0:compile (default-compile) @ soapui-xmlbeans ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1418 source files to /home/developer/workspace/soapui/soapui-xmlbeans/target/classes
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ soapui-xmlbeans ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /home/developer/workspace/soapui/soapui-xmlbeans/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.0:testCompile (default-testCompile) @ soapui-xmlbeans ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ soapui-xmlbeans ---
[INFO] Tests are skipped.
[INFO] 
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ soapui-xmlbeans ---
[INFO] Building jar: /home/developer/workspace/soapui/soapui-xmlbeans/target/soapui-xmlbeans-5.6.0-kimholan.jar
[INFO] 
[INFO] --- maven-jar-plugin:2.4:test-jar (default) @ soapui-xmlbeans ---
[WARNING] JAR will be empty - no content was marked for inclusion!
[INFO] Building jar: /home/developer/workspace/soapui/soapui-xmlbeans/target/soapui-xmlbeans-5.6.0-kimholan-tests.jar
[INFO] 
[INFO] --- maven-install-plugin:2.4:install (default-install) @ soapui-xmlbeans ---
[INFO] Installing /home/developer/workspace/soapui/soapui-xmlbeans/target/soapui-xmlbeans-5.6.0-kimholan.jar to /home/developer/.m2/repository/com/smartbear/soapui/soapui-xmlbeans/5.6.0-kimholan/soapui-xmlbeans-5.6.0-kimholan.jar
[INFO] Installing /home/developer/workspace/soapui/soapui-xmlbeans/pom.xml to /home/developer/.m2/repository/com/smartbear/soapui/soapui-xmlbeans/5.6.0-kimholan/soapui-xmlbeans-5.6.0-kimholan.pom
[INFO] Installing /home/developer/workspace/soapui/soapui-xmlbeans/target/soapui-xmlbeans-5.6.0-kimholan-tests.jar to /home/developer/.m2/repository/com/smartbear/soapui/soapui-xmlbeans/5.6.0-kimholan/soapui-xmlbeans-5.6.0-kimholan-tests.jar
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary for SoapUI project 5.6.0-kimholan:
[INFO] 
[INFO] SoapUI project ..................................... SUCCESS [  0.323 s]
[INFO] SoapUI XMLBeans .................................... SUCCESS [ 30.285 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  30.712 s
[INFO] Finished at: 2019-04-21T11:35:17+02:00
[INFO] ------------------------------------------------------------------------
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Build Order:
[INFO] 
[INFO] SoapUI project                                                     [pom]
[INFO] SoapUI                                                             [jar]
[INFO] SoapUI installer                                                   [jar]
[INFO] SoapUI system test                                                 [jar]
[INFO] 
[INFO] ----------------< com.smartbear.soapui:soapui-project >-----------------
[INFO] Building SoapUI project 5.6.0-kimholan                             [1/4]
[INFO] --------------------------------[ pom ]---------------------------------
[INFO] 
[INFO] --- maven-install-plugin:2.4:install (default-install) @ soapui-project ---
[INFO] Installing /home/developer/workspace/soapui/pom.xml to /home/developer/.m2/repository/com/smartbear/soapui/soapui-project/5.6.0-kimholan/soapui-project-5.6.0-kimholan.pom
[INFO] 
[INFO] --------------------< com.smartbear.soapui:soapui >---------------------
[INFO] Building SoapUI 5.6.0-kimholan                                     [2/4]
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ soapui ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 435 resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.0:compile (default-compile) @ soapui ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1916 source files to /home/developer/workspace/soapui/soapui/target/classes
[INFO] /home/developer/workspace/soapui/soapui/src/main/java/com/eviware/soapui/impl/wsdl/panels/request/actions/WSIValidateRequestAction.java: Some input files use or override a deprecated API.
[INFO] /home/developer/workspace/soapui/soapui/src/main/java/com/eviware/soapui/impl/wsdl/panels/request/actions/WSIValidateRequestAction.java: Recompile with -Xlint:deprecation for details.
[INFO] /home/developer/workspace/soapui/soapui/src/main/java/com/eviware/soapui/impl/support/AbstractHttpRequest.java: Some input files use unchecked or unsafe operations.
[INFO] /home/developer/workspace/soapui/soapui/src/main/java/com/eviware/soapui/impl/support/AbstractHttpRequest.java: Recompile with -Xlint:unchecked for details.
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ soapui ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 56 resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.0:testCompile (default-testCompile) @ soapui ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-surefire-plugin:2.12.1:test (default-test) @ soapui ---
[INFO] Tests are skipped.
[INFO] 
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ soapui ---
[INFO] 
[INFO] --- maven-jar-plugin:2.4:test-jar (default) @ soapui ---
[INFO] 
[INFO] --- maven-install-plugin:2.4:install (default-install) @ soapui ---
[INFO] Installing /home/developer/workspace/soapui/soapui/target/soapui-5.6.0-kimholan.jar to /home/developer/.m2/repository/com/smartbear/soapui/soapui/5.6.0-kimholan/soapui-5.6.0-kimholan.jar
[INFO] Installing /home/developer/workspace/soapui/soapui/pom.xml to /home/developer/.m2/repository/com/smartbear/soapui/soapui/5.6.0-kimholan/soapui-5.6.0-kimholan.pom
[INFO] Installing /home/developer/workspace/soapui/soapui/target/soapui-5.6.0-kimholan-tests.jar to /home/developer/.m2/repository/com/smartbear/soapui/soapui/5.6.0-kimholan/soapui-5.6.0-kimholan-tests.jar
[INFO] 
[INFO] ---------------< com.smartbear.soapui:soapui-installer >----------------
[INFO] Building SoapUI installer 5.6.0-kimholan                           [3/4]
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ soapui-installer ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 2 resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.0:compile (default-compile) @ soapui-installer ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ soapui-installer ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /home/developer/workspace/soapui/soapui-installer/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.0:testCompile (default-testCompile) @ soapui-installer ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ soapui-installer ---
[INFO] Tests are skipped.
[INFO] 
[INFO] >>> exec-maven-plugin:1.2.1:java (default) > validate @ soapui-installer >>>
[INFO] 
[INFO] <<< exec-maven-plugin:1.2.1:java (default) < validate @ soapui-installer <<<
[INFO] 
[INFO] 
[INFO] --- exec-maven-plugin:1.2.1:java (default) @ soapui-installer ---
[INFO] 
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ soapui-installer ---
[INFO] 
[INFO] --- maven-assembly-plugin:2.3:single (default) @ soapui-installer ---
[INFO] Reading assembly descriptor: src/main/assembly/dist.xml
[INFO] Reading assembly descriptor: src/main/assembly/dist-standalone.xml
[INFO] Reading assembly descriptor: src/main/assembly/windows-bin.xml
[INFO] Reading assembly descriptor: src/main/assembly/win32-standalone-bin.xml
[INFO] Reading assembly descriptor: src/main/assembly/linux-bin.xml
[INFO] Reading assembly descriptor: src/main/assembly/mac-bin.xml
[INFO] Copying files to /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-dist
[WARNING] Assembly file: /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-dist is not a regular file (it may be a directory). It cannot be attached to the project build for installation or deployment.
[INFO] Copying files to /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-dist-standalone
[WARNING] Assembly file: /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-dist-standalone is not a regular file (it may be a directory). It cannot be attached to the project build for installation or deployment.
[INFO] Building zip: /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-windows-bin.zip
[INFO] Building zip: /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-win32-standalone-bin.zip
[INFO] Building tar: /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-linux-bin.tar.gz
[INFO] Building zip: /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-mac-bin.zip
[INFO] 
[INFO] --- maven-install-plugin:2.4:install (default-install) @ soapui-installer ---
[INFO] Installing /home/developer/workspace/soapui/soapui-installer/target/soapui-installer-5.6.0-kimholan.jar to /home/developer/.m2/repository/com/smartbear/soapui/soapui-installer/5.6.0-kimholan/soapui-installer-5.6.0-kimholan.jar
[INFO] Installing /home/developer/workspace/soapui/soapui-installer/pom.xml to /home/developer/.m2/repository/com/smartbear/soapui/soapui-installer/5.6.0-kimholan/soapui-installer-5.6.0-kimholan.pom
[INFO] Installing /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-windows-bin.zip to /home/developer/.m2/repository/com/smartbear/soapui/soapui-installer/5.6.0-kimholan/soapui-installer-5.6.0-kimholan-windows-bin.zip
[INFO] Installing /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-win32-standalone-bin.zip to /home/developer/.m2/repository/com/smartbear/soapui/soapui-installer/5.6.0-kimholan/soapui-installer-5.6.0-kimholan-win32-standalone-bin.zip
[INFO] Installing /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-linux-bin.tar.gz to /home/developer/.m2/repository/com/smartbear/soapui/soapui-installer/5.6.0-kimholan/soapui-installer-5.6.0-kimholan-linux-bin.tar.gz
[INFO] Installing /home/developer/workspace/soapui/soapui-installer/target/assemblies/SoapUI-5.6.0-kimholan-mac-bin.zip to /home/developer/.m2/repository/com/smartbear/soapui/soapui-installer/5.6.0-kimholan/soapui-installer-5.6.0-kimholan-mac-bin.zip
[INFO] 
[INFO] --------------< com.smartbear.soapui:soapui-system-test >---------------
[INFO] Building SoapUI system test 5.6.0-kimholan                         [4/4]
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ soapui-system-test ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /home/developer/workspace/soapui/soapui-system-test/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.0:compile (default-compile) @ soapui-system-test ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ soapui-system-test ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 81 resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.0:testCompile (default-testCompile) @ soapui-system-test ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ soapui-system-test ---
[INFO] Tests are skipped.
[INFO] 
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ soapui-system-test ---
[WARNING] JAR will be empty - no content was marked for inclusion!
[INFO] 
[INFO] --- maven-jar-plugin:2.4:test-jar (default) @ soapui-system-test ---
[INFO] 
[INFO] --- maven-install-plugin:2.4:install (default-install) @ soapui-system-test ---
[INFO] Installing /home/developer/workspace/soapui/soapui-system-test/target/soapui-system-test-5.6.0-kimholan.jar to /home/developer/.m2/repository/com/smartbear/soapui/soapui-system-test/5.6.0-kimholan/soapui-system-test-5.6.0-kimholan.jar
[INFO] Installing /home/developer/workspace/soapui/soapui-system-test/pom.xml to /home/developer/.m2/repository/com/smartbear/soapui/soapui-system-test/5.6.0-kimholan/soapui-system-test-5.6.0-kimholan.pom
[INFO] Installing /home/developer/workspace/soapui/soapui-system-test/target/soapui-system-test-5.6.0-kimholan-tests.jar to /home/developer/.m2/repository/com/smartbear/soapui/soapui-system-test/5.6.0-kimholan/soapui-system-test-5.6.0-kimholan-tests.jar
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary for SoapUI project 5.6.0-kimholan:
[INFO] 
[INFO] SoapUI project ..................................... SUCCESS [  0.196 s]
[INFO] SoapUI ............................................. SUCCESS [ 12.495 s]
[INFO] SoapUI installer ................................... SUCCESS [ 32.811 s]
[INFO] SoapUI system test ................................. SUCCESS [  0.064 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  45.680 s
[INFO] Finished at: 2019-04-21T11:36:03+02:00
[INFO] ------------------------------------------------------------------------

```

Warning
-------

Dont clean the build! The generated sources were left in the
generated directory.

This should build out of the box if the javafx module 
is at the right location.


Prerequisites
-------------

- JDK8 (OpenJDK OpenJ9, but Oracle/HotSpot should work too) 
``
$ ~/lib/java8/bin/java -version
openjdk version "1.8.0_202"
OpenJDK Runtime Environment (build 1.8.0_202-b08)
Eclipse OpenJ9 VM (build openj9-0.12.1, JRE 1.8.0 Linux amd64-64-Bit Compressed References 20190205_213 (JIT enabled, AOT enabled)
OpenJ9   - 90dd8cb40
OMR      - d2f4534b
JCL      - d002501a90 based on jdk8u202-b08)
```
- JDK11  (OpenJDK HotSpot)
- Maven 3.6.0
- Download JFX for JDK11 https://openjfx.io/ and extract it somewhere

Modifications
-------------

Check the diff. Basically this:

- Generated XMLBeans source files are committed from a JDK8
  build of SoapUI, because I couldn't be bothered to figure
  out how to get the code generation to work on JDK11
  - List getXXX methods are generated differently on JDK11
    which causes it to the JDK11 build to fail if the javaSource
    parameter is incrememented in the build
- I have no need for the testserver-api soapui-maven-plugin, so 
  they're removed from the build, I'm planning to move away
  from SoapUI because the OpenSource release is buggy
  and ill suppported, although there's more activity lately
  by SmartBear    
- Concurrency bug that occurs more frequently on SMP-like systems
  such as Ryzen 

What was done to get get this to build on OpenJDK11/HotSpot
-----------------------------------------------------------

- Set JAVA_HOME/PATH to JDK8
```
export JAVA_HOME=~/lib/java8 PATH=~/lib/java8/bin:$PATH
```
- Build the project (skip the tests) 
```
mvn clean install -DskipTests
```
- Switch to JDK11
```
export JAVA_HOME=~/lib/java11 PATH=~/lib/java11/bin:$PATH
```
- Modify the pom.xml to point to a valid JFX installation
```
  <plugin>
     <groupId>org.apache.maven.plugins</groupId>
     <artifactId>maven-compiler-plugin</artifactId>
     <version>3.8.0</version>
     <configuration>
       <source>11</source>
       <target>11</target>
       <compilerArgs>
         <arg>--module-path</arg>
         <arg>/home/developer/lib/javafx-sdk-11.0.2/lib</arg>
         <arg>--add-modules</arg>
         <arg>javafx.controls,javafx.fxml,javafx.web,javafx.swing</arg>
       </compilerArgs>
    </configuration>
  </plugin>
```
- Create the SoapUI assembly
```
mvn install -f soapui-installer/pom.xml -Passembly
```