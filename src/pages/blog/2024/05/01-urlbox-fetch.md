---
title: How to Urlbox with fetch
author: "@OlaHolstVea"
date: 2024-05-01
---


# How to Urlbox with fetch

```js

---
const Urlbox_Secret_Key = import.meta.env.URLBOX_SECRET_KEY;
const Urlbox_Pub_Key = import.meta.env.URLBOX_PUB_KEY;


async function fetchUrl({Urlbox_Pub_Key}, {Urlbox_Secret_Key}) {

  const response = await fetch(
    `https://api.urlbox.io/v1/Urlbox_Pub_Key/Urlbox_Secret_Key/jpg?url=github.com&thumb_width=600&quality=80`,
    {
      method: "GET",
      headers: {
        "x-api-key": apiKey,
      },
    }
  ).then((response) => response.json());

  return response.data;
}


---
```