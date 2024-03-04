---
external: false
title: "Using springboot as backend for android projects"
description: "Native android projects with springboot as backend"
date: 2024-03-03
---

## Setting up a springboot project

- Go to [Spring Initializr](https://start.spring.io)
- Generate a springboot project with some dependencies, namely web, lombok etc.
- Generate the project and download the zip file and then open the extracted folder in Intellij Idea or STS.
- Create a controller with following code --
    ```
    import org.springframework.web.bind.annotation.CrossOrigin;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    @CrossOrigin("*")
    public class UserController {

        @GetMapping("/hello")
        public String hello() {
            return "Hello from User Service";
        }

        @GetMapping("/user")
        public String user() {
            return "Hello User";
        }

    }
    
    ```