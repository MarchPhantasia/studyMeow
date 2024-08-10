在 Spring Boot 项目中，你可以通过几种方式控制 HTTP 响应的状态码。当创建资源或操作成功时，通常会返回 HTTP 状态码 201，这表示已经在服务器上创建了新资源。以下是如何实现这一行为的几种方法：

### 1. 使用 `@ResponseStatus` 注解

你可以在控制器的方法上使用 `@ResponseStatus` 注解来指定返回的状态码。这种方式简单直接，特别适用于那些返回状态而不需要返回特定数据的操作：

```java
import org.springframework.web.bind.annotation.*;
import org.springframework.http.HttpStatus;

@RestController
@RequestMapping("/api/items")
public class ItemController {

    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public void addItem(@RequestBody Item item) {
        // 添加项目的逻辑
        // 数据库操作等
    }
}
```

在这个例子中，每当 `addItem` 方法被调用并成功执行后，它会返回状态码 201（`HttpStatus.CREATED`）。

### 2. 使用 `ResponseEntity` 对象

如果你需要更细粒度的控制，比如除了状态码之外，还要控制响应头或返回一些响应体数据，你可以使用 `ResponseEntity` 对象：

```java
import org.springframework.http.ResponseEntity;

@RestController
@RequestMapping("/api/users")
public class UserController {

    @PostMapping
    public ResponseEntity<User> createUser(@RequestBody User user) {
        User savedUser = userService.save(user);
        return ResponseEntity.status(HttpStatus.CREATED).body(savedUser);
    }
}
```

在这个例子中，`createUser` 方法创建一个用户并返回这个新创建的用户对象。通过 `ResponseEntity.status(HttpStatus.CREATED).body(savedUser)`，你不仅设置了状态码为 201（`HttpStatus.CREATED`），还将新创建的用户对象作为响应体返回。

### 3. 使用 `HttpServletResponse` 对象

你也可以通过注入 `HttpServletResponse` 对象直接操作响应：

```java
import javax.servlet.http.HttpServletResponse;

@RestController
@RequestMapping("/api/files")
public class FileController {

    @PostMapping("/upload")
    public void uploadFile(@RequestParam("file") MultipartFile file, HttpServletResponse response) {
        // 处理文件上传的逻辑
        // 成功后设置状态码
        response.setStatus(HttpServletResponse.SC_CREATED); // 设置状态码为201
    }
}
```

这种方式允许你在控制器方法中直接设置响应状态码。使用 `HttpServletResponse` 是一种较为底层的做法，适用于需要直接操作响应细节的场景。

以上方法均可以根据你的具体需求选择使用，以实现在 Spring Boot 应用中自定义 HTTP 响应的状态码。