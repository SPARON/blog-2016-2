---
layout: post
title: 【Maven】Maven的发布Plugin配置
date: 2017-11-21
categories: 配置
description: Maven打包、发布相关信息配置
---


## Plugin配置

  ```xml
    <build>
        <plugins>
            <plugin>
                <!-- 编译插件 -->
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3.2</version>
                <configuration>
                    <source>1.5</source>
                    <target>1.5</target>
                </configuration>
            </plugin>
            <plugin>
                <!-- 发布插件 -->
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-deploy-plugin</artifactId>
                <version>2.5</version>
            </plugin>
            <plugin>
                <!-- 打包插件 -->
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>2.3.1</version>
            </plugin>
            <plugin>
                <!-- 安装插件 -->
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-install-plugin</artifactId>
                <version>2.3.1</version>
            </plugin>
            <plugin>
                <!-- 单元测试插件 -->
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.7.2</version>
                <configuration>
                    <skip>true</skip>
                </configuration>
            </plugin>
            <plugin>
                <!-- 源码插件 -->
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-source-plugin</artifactId>
                <version>2.1</version>
                <!-- 发布时自动将源码同时发布的配置 -->
                <executions>
                    <execution>
                        <id>attach-sources</id>
                        <goals>
                            <goal>jar</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
  ```


## Maven命令

- Maven发布命令
  > mvn deploy
- Maven源码打包命令
  > mvn source:jar