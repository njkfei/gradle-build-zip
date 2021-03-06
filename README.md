# gradle-build-zip
 配置打包，类似于maven asseamble插件。
 如下所示 build.gradle。
 
```
buildscript {
  repositories {
    maven { url "https://repo.spring.io/libs-release" }
    mavenLocal()
    mavenCentral()
  }
  dependencies {
    classpath("org.springframework.boot:spring-boot-gradle-plugin:1.3.3.RELEASE")
  }
}
apply plugin: 'application'
apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'idea'
apply plugin: 'spring-boot'
apply plugin: 'maven'
apply plugin: 'maven-publish'
//apply plugin: 'jar'
apply plugin: 'distribution'



distributions {
    main {
        baseName = 'teacherfeed'
        contents {
            from 'src/main/resources'
        }
    }
}

jar {
    group = 'com.sanhao.tech'
    baseName = 'teacherfeed'
    version =  '0.1.0'
    manifest {
        attributes 'mainClassName': 'com.sanhao.tech.teacherfeed.App'
    }
}

repositories {
  mavenLocal()
  mavenCentral()
  maven { url "https://repo.spring.io/libs-release" }
}

// best way to set group ID
group = 'com.sanhao.tech'
// 指定程序入口
mainClassName = 'com.sanhao.tech.teacherfeed.App'
install {
    repositories.mavenInstaller {
        // only necessary if artifact ID diverges from project name
        // the latter defaults to project directory name and can be
        // configured in settings.gradle
        pom.artifactId = 'teacherfeed'
        // shouldn't be needed as this is the default anyway
        pom.packaging = 'jar'
        
        pom.version = '0.0.1'
    }
}

task someTar(type: Tar) {
    compression = Compression.GZIP
    classifier = 'src'
    from projectDir
    include {
        sourceSets.collect {
            it.allSource.asPath
        }
    }
    exclude{
        'src/test'
    }
}

dependencies {
  	compile("org.springframework.boot:spring-boot-starter")
    compile("org.springframework.boot:spring-boot-starter-web")
    compile("org.springframework.boot:spring-boot-starter-tomcat")
    compile("org.springframework.boot:spring-boot-starter-data-mongodb")
    compile("org.springframework.boot:spring-boot-starter-security")
    compile("org.springframework:spring-webmvc")
    compile("org.mybatis:mybatis-spring:1.2.3")
    compile("org.springframework.boot:spring-boot-starter-jdbc")
    compile("mysql:mysql-connector-java")
    compile("org.mybatis:mybatis:3.3.0")
    compile("org.springframework:spring-context-support:4.1.5.RELEASE")
    compile("org.springframework.data:spring-data-redis")
    compile("redis.clients:jedis")
    compile("org.springframework:spring-aop:4.1.5.RELEASE")
	compile("org.aspectj:aspectjrt:1.6.11")
	compile("org.aspectj:aspectjweaver:1.6.11")
	compile("aopalliance:aopalliance:1.0")
	compile('com.github.shyiko:mysql-binlog-connector-java:0.3.1')
	compile('org.apache.commons:commons-lang3:3.0')
    compile('commons-dbcp:commons-dbcp:1.4')
	compile('commons-io:commons-io:2.4')
    compile('com.alibaba:fastjson:1.2.8')
    compile('com.fasterxml.jackson.core:jackson-core:2.7.3')
    compile('org.codehaus.jackson:jackson-mapper-asl:1.9.13')
    compile('org.codehaus.jackson:jackson-core-asl:1.9.13')
    compile('com.google.code.gson:gson:2.3.1')
    compile("org.projectlombok:lombok:1.16.8")
    compile('commons-beanutils:commons-beanutils:1.9.2')
    compile("org.apache.httpcomponents:httpclient:4.2.6")
    testCompile("junit:junit")
}

task wrapper(type: Wrapper) {
  gradleVersion = '2.9'
}
```
