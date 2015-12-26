# leisurelink/ubuntu-node-runtime

A docker image for running nodejs applications in an ubuntu based container.


## What's in the box

`ubuntu-node-runtime` is intended as a runtime environment for nodejs applications. Its purpose is to run a nodejs application that has already been built, probably via `npm install`. We build ours with [`leisurelink/ubuntu-node-build-machine`](https://github.com/LeisureLink/ubuntu-node-build-machine).


## Use

To use this docker image, simply copy your application's root folder to `/opt/app`. You can do so in a `Dockerfile` like so (this one assumes the `Dockerfile` is in your application's root):

```
FROM leisurelink/ubuntu-node-runtime:latest
MAINTAINER You <email@waat.eva>

COPY . /opt/app
```

You can also try it out by using `docker run`'s `--volume` option (assumes current directory is your application's root):

```bash
docker run --volume `pwd`:/opt/app leisurelink/ubuntu-node-runtime
```


## Conventions

`ubuntu-node-runtime` relies on `npm`'s ability to run scripts. The `run` script is purposely kept simple; it changes the working directory to that of the application, changes the current user to `node` and calls `npm start`.

In order to run your application inside this docker image your `package.json` file must declare a `start` script. Most of the time a script like the following will work:

```json
  ...
  "scripts": {
    "start": "node app.js",
    ...
```

Of course you can use a more sophisticated script if necessary. For a good reference for how to setup and use `npm` scripts, see [Keith Cirkel's How to Use npm as a Build Tool](http://blog.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/).

By default, `ubuntu-node-runtime` expects your application to be available inside of the container at the directory path `/opt/app`. If you choose to change the location of the application, specify the new location in the environment variable `NODE_SERVICE_ROOT`.


## Tags - Asset Versions

* **latest, 1.0.0** (Ubuntu:14.04, nodejs 4.2.4)
* **node-0.12.7** (Ubuntu:14.04, nodejs 0.12.7)


## License

[MIT](https://github.com/LeisureLink/ubuntu-node-runtime/blob/master/LICENSE)
