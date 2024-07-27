---
title: How to Urlbox with fetch 74
author: "@OlaHolstVea"
date: 2024-05-04
---


# How to Urlbox with fetch

```js
    const baseEndpoint = 'https://api.github.com';
    const usersEndpoint = `${baseEndpoint}/users`;
    const userEl = document.querySelector('.user');

    async function displayUser(username) {
      userEl.textContent = 'loading...';
      const response = await fetch(`${usersEndpoint}/${username}`);
      const data = await response.json();
      console.log(data);
      console.log(data.blog);
      console.log(data.name);
      console.log(data.location);
      userEl.textContent = `${data.name} - ${data.blog}`;
    }

    function handleError(err) {
      console.log('OH NO!');
      console.log(err);
      userEl.textContent = `Something went wrong: ${err}`
    }

    displayUser('stolinski').catch(handleError);



```

```js

---

---
<head>
    <title>APIs</title>
</head>

<body>
    <h1>APIs</h1>
    <p class="user"></p>
    <script>
        const endpoint = 'https://api.github.com/users/urlbox';
        const userEl = document.querySelector('.user');

        async function displayUser(username) {

            const response = await fetch(endpoint);
            const data = await response.json();

            console.log(data);
            console.log(data.name);
            console.log(data.blog);


        }
        function handleError(err) {
            console.log('OH NO!');
            console.log(err);
        }

        displayUser('urlbox')




    </script>
</body>
```