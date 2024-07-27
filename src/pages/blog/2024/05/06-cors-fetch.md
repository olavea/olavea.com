---
title: How to Urlbox with fetch 74
author: "@OlaHolstVea"
date: 2024-05-04
---


# How to Urlbox with fetch


cors-fetch
```js

---

---
<body>
    <script>

        const proxy = `https://cors-anywhere.herokuapp.com/`;
        const endpoint = 'https://github.com';

        async function displayUser(username) {
            const response = await fetch(`${proxy}${endpoint}`);
            const data = await response.json();
            console.log(data);
        }
        function handleError(err) {
            console.log('Oh NO!');
            console.log(err);
        }

        displayUser('urlbox').catch(handleError);
    </script>
</body>
```


```js
const baseEndpoint = 'https://api.github.com';

async function fetchGithub(query) {
    const res = await fetch(`${baseEndpoint}?q={query}`);
    const data = await res.json();
}

fetchGithub('pizza');


```
