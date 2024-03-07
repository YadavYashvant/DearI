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

## Integrating the Spring Boot Project with an Android App

Now that we have set up our Spring Boot project, let's integrate it with our Android application. Follow these steps to establish communication between the Android frontend and the Spring Boot backend:

1. **Retrieve Backend Base URL**: Determine the base URL of your Spring Boot backend. This URL will be used by the Android app to send HTTP requests to the server. You can find this URL by running your Spring Boot application locally or deploying it to a server.

2. **Add Internet Permission**: In your AndroidManifest.xml file, make sure to add the internet permission to allow the Android app to make network requests:
    ```xml
    <uses-permission android:name="android.permission.INTERNET" />
    ```

3. **Send HTTP Requests from Android**: In your Android app, use libraries like Retrofit, Volley, or OkHttp to send HTTP requests to the Spring Boot backend. Here's an example using Retrofit:

    Add Retrofit dependency to your app-level build.gradle file:
    ```gradle
    implementation 'com.squareup.retrofit2:retrofit:2.9.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
    ```

    Create a Retrofit instance with the base URL of your Spring Boot backend:
    ```java
    Retrofit retrofit = new Retrofit.Builder()
            .baseUrl("YOUR_BACKEND_BASE_URL")
            .addConverterFactory(GsonConverterFactory.create())
            .build();
    ```

    Define an interface with methods corresponding to the API endpoints in your Spring Boot backend:
    ```java
    public interface UserService {
        @GET("/hello")
        Call<String> getHelloMessage();

        @GET("/user")
        Call<String> getUserMessage();
    }
    ```

    Create an instance of the UserService interface using the Retrofit instance:
    ```java
    UserService userService = retrofit.create(UserService.class);
    ```

    Finally, make HTTP requests using the UserService methods:
    ```java
    Call<String> helloCall = userService.getHelloMessage();
    helloCall.enqueue(new Callback<String>() {
        @Override
        public void onResponse(Call<String> call, Response<String> response) {
            if (response.isSuccessful()) {
                String message = response.body();
                // Handle successful response
            } else {
                // Handle unsuccessful response
            }
        }

        @Override
        public void onFailure(Call<String> call, Throwable t) {
            // Handle failure
        }
    });
    ```

4. **Handle Responses in Android**: Implement the logic to handle responses from the Spring Boot backend in your Android app's UI or business logic.

---

By integrating your Spring Boot backend with your Android app using the provided steps and code snippets, you can create a seamless user experience with efficient data exchange between the frontend and backend.

Stay tuned for more tutorials and guides on Android development with Spring Boot! Feel free to reach out if you have any questions or need further assistance.
