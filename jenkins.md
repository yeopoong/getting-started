CI
===

Jenkins 
-------

http://jenkins-ci.org/

>$ adduser jenkins  
>$ su - jenkins   
>$ wget http://mirrors.jenkins-ci.org/war-stable/latest/jenkins.war  
>$ java -jar jenkins.war --httpPort=5000

`http://호스트:5000/`로 접근해서 확인해 보자! 

### Maven repository 설정
Nexus 서버의 접근권한을 설정하기 위해서 maven 설정파일인 `setting.xml`에 다음의 내용을 추가한다.

```
<servers>
...
    <server>
      <id>releases</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>  
    <server>
      <id>snapshots</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>  
    <server>
      <id>thirdparty</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>
...
</servers>
```

### 플러그인 설치
 * Git plugin
 * Deploy to container Plugin

### 시스템 설정 
 * JDK 
 >`Name`: java1.8  
 >`JAVA_HOME`: /usr/lib/jvm/java-1.8.0-openjdk
 * Git 
 >`Path to Git executable`: /usr/bin/git
 * Maven
 >`Name`: maven  
 >`MAVEN_HOME`: /user/share/maven 


SonarQube
---------

```
# adduser sonar
# su - sonar
# wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-5.5.zip
# unzip sonarqube-5.5.zip
# ./sonarqube-5.5/bin/linux-x86-64/sonar.sh start
```

`http://서버주소:9000/` 로 접근해서 확인해 보자! (admin/admin)


Nexus
-----

```
# adduser nexus
# su - nexus
# wget  http://download.sonatype.com/nexus/oss/nexus-2.13.0-01-bundle.tar.gz
# tar zxvf nexus-2.13.0-01-bundle.tar.gz
# ln -s nexus-2.13.0-01 nexus
# vi nexus/bin/nexus
  RUN_AS_USER=nexus
# ./nexus/bin/nexus start
```

`http://서버주소:8081/nexus` 로 접근해서 확인해 보자!

Private library repository 를 사용하기 위해서 Nexus를 설정한다.

### Nexus 서버 설정
* Nexus 서버에 접속한다.
    * [http://localhost:8080/nexus](http://localhost:8080/nexus/#welcome) 
* admin/admin123 으로 로그인한다.
* 좌측 메뉴에서 Repositories를 클릭하고 우측목록화면에서 Central Repository를 선택한다.
* Configuration 탭에서 Download Remote Indexes를 True로 변경한 후 저장한다.

개발환경
=======

Nexus
-----

Maven Central 레포지토리 대신에 Nexus 서버를 프록시 서버로 사용하도록 다음의 설정을 pom.xml 에 추가한다.

```
    <repositories>
      <repository>
        <id>central</id>
        <url>http://192.168.0.115:8080/nexus/content/groups/public</url>
        <releases><enabled>true</enabled></releases>
        <snapshots><enabled>true</enabled></snapshots>
      </repository>
    </repositories>

    <pluginRepositories>
      <pluginRepository>
        <id>central</id>
        <url>http://192.168.0.115:8080/nexus/content/groups/public</url>
        <releases><enabled>true</enabled></releases>
        <snapshots><enabled>true</enabled></snapshots>
      </pluginRepository>
    </pluginRepositories>
```

어플리케이션의 배포본을 Nexus Snapshots 레포지토리에 배포하기 위해서 다음의 설정을 pom.xml 에 추가한다.

```
    <distributionManagement>
        <repository>
            <id>releases</id>
            <url>http://192.168.0.115:8080/nexus/content/repositories/releases</url>
        </repository>
        <snapshotRepository>
            <id>snapshots</id>
            <url>http://192.168.0.115:8080/nexus/content/repositories/snapshots</url>
        </snapshotRepository>
    </distributionManagement>
```

Maven Release
-------------

다음과 같이 pom.xml 에 Maven Release Plugin 과 scm 설정을 추가한다.

```
  <scm>
        <connection>scm:git:https://github.com/t3qdev/nextg.git</connection>
        <url>http://github.com/t3qdev/nextg</url>
        <developerConnection>scm:git:https://github.com/t3qdev/nextg.git</developerConnection>
  </scm>
```


```
  <scm>
        <connection>scm:git:https://github.com/t3qdev/nextg.git</connection>
        <url>http://github.com/t3qdev/nextg</url>
        <developerConnection>scm:git:https://github.com/t3qdev/nextg.git</developerConnection>
  </scm>
```

```
    <build>
        <plugins>
            ....
            <plugin>
                <artifactId>maven-release-plugin</artifactId>
                <version>2.5.3</version>
                <configuration>
                    <autoVersionSubmodules>true</autoVersionSubmodules>
                    <goals>deploy</goals>
                    <arguments>-Dmaven.javadoc.skip=true</arguments>
                </configuration>
                <dependencies>
                    <dependency>
                        <groupId>org.apache.maven.shared</groupId>
                        <artifactId>maven-invoker</artifactId>
                        <version>2.2</version>
                    </dependency>
                </dependencies>
            </plugin>
            ...
        </plugins>
    </build>
```
  
