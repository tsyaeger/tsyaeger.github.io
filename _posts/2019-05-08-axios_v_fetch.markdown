---
layout: post
title:      "Axios v Fetch"
date:       2019-05-08 22:18:30 -0400
permalink:  axios_v_fetch
---


No disrespect to Fetch, but axios is awesome. Axios and Fetch are both promise-based methods of making http network requests. They both do the job, but there are significant differences that can inform your decision to use one over the other.

Fetch is a medium-level native API created as an alternative to XMLHttpRequest, while axios is a 3rd party package built upon XMLHttpRequest. By using XMLHttpRequest, axios provides some functionality that Fetch lacks, for example upload progress monitoring. Both options support modern browsers, though Fetch does not support older IE, while axios supports IE8+ (although the rest of your app may not).

In practice, with fetch you can control every step of the request, but many settings have to be manually implemented — for instance cors, cookie-based authentication, and parsing JSON — whereas axios handles these by default.

When making a request, a Promise is created (to handle asynchronous operations without the need for a callback) and it must be resolved in order to access the data. If you use Fetch when handing JSON data this is at minimum a two-step process. The first step is to make the initial http request and the second is to parse the response with the json() method. For Post requests, the JSON must be converted to a string using JSON.stringify() and the ‘Content-Type’ header must indicate that the payload is JSON, otherwise the server will treat it as a string.


```fetch(‘/things', {
  headers: { "Content-Type": "application/json; charset=utf-8" },
  method: 'POST',
  body: JSON.stringify({
    thing: 'stuff',
    anotherThing: ‘additional stuff',
  })
})```

Axios automatically serializes JavaScript objects to JSON and returns responses that are JSON strings parsed into a JS objects that you can immediately access. So there’s no need to parse JSON with the json() method.

Error handling is tricky with Fetch, as the catch block will only return an error when a network error occurs.  So for instance, if your backend returns the status code 500, fetch will treat it as the same as status code as a 200 --  indicating that the request was successful. Fortunately, you can check that the response was error-free by using response.ok, like so:

```
fetch(url)
  .then(response => {
    if (response.ok) {
      return response.json()
    } else {
      return Promise.reject({
        status: response.status,
        statusText: response.statusText
      })
    }
  })
  .catch(error => {
      console.log(error)
  })```



As for axios, once you use 'npm install axios' you can create an instance with a custom configuration like so:

```
// httpClient.js
import axios from ‘axios’;

const params = {
  baseURL: 'https://blahblah.com/'
};

const httpClient = axios.create(params);
export default httpClient;
```

And axios handles the particulars:

```
// services.js
import httpClient from './httpClient';

export const getThings = () => {
	return httpClient.get('/things');
}

export const saveThings = (things) => {
  	return httpClient.post('/things', 
		{ things }
	)
}
```

Learn more about axios here:
https://www.npmjs.com/package/axios
