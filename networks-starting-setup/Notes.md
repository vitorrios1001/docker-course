# Docker commands

## Localhost

We can use localhost in the container docker doing this:

```js
// Old
mongoose.connect(
  'mongodb://localhost:27017/swfavorites',
  { useNewUrlParser: true },
  (err) => {
    if (err) {
      console.log(err);
    } else {
      app.listen(3000);
    }
  }
);

// New

mongoose.connect(
  'mongodb://host.docker.internal:27017/swfavorites',
  { useNewUrlParser: true },
  (err) => {
    if (err) {
      console.log(err);
    } else {
      app.listen(3000);
    }
  }
);
```

## Network

#### Create Network

```docker shell
$ docker network create favorites-net
```

#### Run Container + Network

```docker shell
$ docker run -d --name mongo-db --network favorites-net mongo

$ docker run --name favorites -d --rm --network favorites-net -p 3000:3000 favorites-node
```

### Use in the code

```js
mongoose.connect(
  'mongodb://mongo-db:27017/swfavorites',
  { useNewUrlParser: true },
  (err) => {
    if (err) {
      console.log(err);
    } else {
      app.listen(3000);
    }
  }
);
```
