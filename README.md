# twitter

Twitter-like application, built with [Node][node] and [Redis][redis].

## Live demo

https://twitterlikeapp.herokuapp.com/

## Features

The following features checked are currently implemented, otherwise they are still work in progress.

- [x] Sign up / Log in / Log out
- [x] Post tweet
- [x] Delete tweet
- [x] Follow user
- [x] Unfollow user
- [ ] Favorite tweet

## Design

### Users

User IDs are generated sequencially via increments:

```js
redis.incr('user:ids', function(err, id) {
  user.id = id;
});
```

Users are stored into Redis hashes, the key name of the hash representing a given user is `user:123`. Every hash has the following fields:

```
name (the name of the user)
pass (encripted password)
fullname (the full name of the user)
```

### Tweets

Tweets also have sequencial IDs, generated by incrementing the following key:

```js
redis.incr('tweet:ids', function(err, id) {
  tweet.id = id;
});
```

Every tweet is stored into an hash named `tweet:456` with the following fields:

```
text (the body of the tweet)
created_at (time created)
user (user object)
```

Additionaly there is a list of tweets in the `tweets` key.

## Development

### Download project

First, clone this repository. When download finished, move into the project directy then run:

```
$ npm install
```

This will install all required dependent modules.

### Install Redis

Since this application requires Redis installed on your machine, you'll need to install it. For Mac OSX, the most easiest way would be using [Homebrew][homebrew].

```
$ brew install redis
```

Otherwise, please check [Redis's official documentaiton][redis] out.

### Start application

This application is based on [Express][express] framework. To start the application, run:

```
$ npm start
```

It will serve application at `http://localhost:3000/`.

## Deployment

For deployment, `Procfile` is packaged as a default default configuration for integration with Heroku. If you are not familiar with Heroku I would recommend you to first read through the documentation of [how to get started with Node.js on Heroku][heroku-getting-started-with-node].

The whole deployment process should be as simple as the follwing three steps.

Login to Heroku:

```
$ heroku login
````

Create an app on Heroku:

```
$ heroku create
```

Deploy an app:

```
$ git push heroku master
```

## References

- [antirez/retwis][retwis] - A Twitter-toy clone written in PHP and Redis

## License

MIT © Tatsuya Oiwa

[node]: https://nodejs.org/
[redis]: http://redis.io/
[homebrew]: http://brew.sh/
[express]: http://expressjs.com/
[heroku-getting-started-with-node]: https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction
[retwis]: https://github.com/antirez/retwis
