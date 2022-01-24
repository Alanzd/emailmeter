# emailmeter Ana María Lanz
Coding test for frontend position at Emailmeter.
This project contains my implementation to the first part: user ranking
The project has been developed using Vue 3, Bootstrap and Axios.
During the coding process I had some issues:
* I got some CORS-related errors in Chrome trying to get data from the API. Chrome bloqued the second request to obtain the next 10 users. I tried with Firefox and everything was ok.

* I didn't find a way to sort the results after receiving all the pages from the `/users` API, so I added buttons at the header of the table which sort in descending order.

I also included my approach to solving the second part. For that I included the template I would use to render the charts: [UserDetails.vue](src/components/UserDetails.vue)

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```


