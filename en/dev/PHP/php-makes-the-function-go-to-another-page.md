---
title: Navigate web browser to another page in PHP
description: 
published: true
date: 2022-12-24T19:36:00.874Z
tags: english, php
editor: markdown
dateCreated: 2022-12-24T19:35:29.187Z
---

## Using headers() function

- You can use php's `header()` to direct the web browser to a specific page.
- `header()` operates through the HTTP Response Header transmitted to the client.

```php
<?php
   // redirect to example.com
   header('Location: https://www.example.com');
   exit;
?>
```

- If you need a delay before moving the page, you can use `refresh`. It also works as an HTTP Header.

```php
<?php
   // Redirect to example.com after 5 seconds
   header('refresh: 5; url=https://www.example.com');
   exit;
?>
```

## Using \<script>

- The downside of using `headers()` is that it ignores code that operates synchronously, such as the `alert()` function of `<script>`.
- For example, in the code below, "Hello, World!" The warning window (Alert) is not displayed and moves directly to `example.com`.


```php
<?php
   // The alert is not displayed and the page moves immediately.
   echo '<script>alert("Hello, World!");</script>';
   header('Location: https://www.example.com');
?>
```

- In this case, using javascript's `window.location.href` rather than `header()` ensures the desired operation.

```php
<?php
   // Displays a warning with the message "Hello, World!" and moves to example.com
   echo '<script>
           alert("Hello, World!");
           window.location.href = "https://www.example.com";
         </script>';
?>
```

- If delay time is required before page movement, it can be used in combination with `setTimeout`.


```php
<?php
   // After displaying a warning with the message "Hello, World!", go to example.com 5 seconds later
   echo '<script>
           alert("Hello, World!");
           setTimeout(function() {
             window.location.href = "https://www.example.com";
           }, 5000);
         </script>';
?>
```