Stream to S3
========================

A quick script to **stream large files to Amazon S3 using node.js**

[![Build Status](https://travis-ci.org/nelsonic/stream-to-s3.png?branch=master)](https://travis-ci.org/nelsonic/stream-to-s3)
[![Code Climate](https://codeclimate.com/github/nelsonic/stream-to-s3.png)](https://codeclimate.com/github/nelsonic/stream-to-s3)
[![Coverage Status](https://coveralls.io/repos/nelsonic/stream-to-s3/badge.png?branch=master)](https://coveralls.io/r/nelsonic/stream-to-s3?branch=master)
[![Dependencies](https://david-dm.org/nelsonic/stream-to-s3.png?theme=shields.io)](https://david-dm.org/nelsonic/stream-to-s3)
[![devDependency Status](https://david-dm.org/nelsonic/stream-to-s3/dev-status.svg)](https://david-dm.org/nelsonic/stream-to-s3#info=devDependencies)

[![NPM stats](https://nodei.co/npm/stream-to-s3.png?downloads=true)](https://www.npmjs.org/package/stream-to-s3)

Node.js is the *perfect* tool for streaming large files to Amazon Web Services S3.


![Node.js and Amazon S3](http://i.imgur.com/w1S84gJ.png)

## Use Cases

- Rolling your own cloud backup service
- Uploading files/photos from a mobile app or website
- Drop Box Clone using S3 as backend


## Usage

Install from NPM:

```sh
npm install stream-to-s3 --save
```

```
var S3 = require('stream-to-s3');
var file = '/your-file-name.jpg';      // any file format!
S3.streamFileToS3(file, function(err) { // standard callback function:
  console.log(file,' Was uploaded. Visit:',S.S3FileUrl(file));
});
```

### Require Environment Variables

`stream-to-s3` uses [environment variables](https://github.com/dwyl/**learn-environment-variables)
for Amazon WebServices Secret Keys  
(*to help people avoid hard-coding passwords in your code...*)

> If you're ***new to Environment Variables***
check out our ***complete beginners guide***:
[https://github.com/dwyl/**learn-environment-variables**](https://github.com/dwyl/learn-environment-variables)

you will need to *set* the following environment variables:

```sh
AWSAccessKeyId=ReplaceWithYourActualKey
AWSSecretKey=DownloadThisFromYourAWSConsole
S3BUCKET=YourS3BucketName
AWSREGION=eu-west-1
ACL=public-read
```

> While you are developing your app, we recommend managing your environment
variables using [**env2**](https://github.com/dwyl/env2)  
this will allow you to use a *file* to keep your AWS/S3 keys which
you can easily share with your co-developers and still *exculde* from GitHub
(*by listing it in your `.gitignore` file*)

# tl;dr

**Note**: we have deliberately kept the stream-uploader simple,
if you need to transform the data in the read-stream before
uploading it, fork this repo, add a new test/method and submit a PR.

## The Solution

See: **index.js** for the implementation details.

## Tests! :open_mouth:

**Three steps** to running the test suite:

1. Install (Dev) Dependencies (Mocha etc.) <br/>
```sh
npm install
```

2. **Copy** the **config_example.json** file **to config.json**
and put your *real* Amazon S3 credentials in the config.json file:
```sh
cp config_example.json config.json  &&  atom config.json
```

3. Run ***real***tests using using the following command:
```sh
npm run realtest
```


***Note***: Because I don't want to make my S3 Keys ***Public***
(on GitHub), <br />
I've had to "fake" the `npm test` command for Travis.<br/>
But don't fear, there are tests and they are easy to run. <br/>
(and I don't encourage others to do the **exit 0** "hack" unless <br />
there's some sensitive config you don't want to open-source...)

## Useful Links

Node.js Docs for Readable Streams:
- http://nodejs.org/api/stream.html#stream_class_stream_readable

Best place to learn Node.js Streams:
- SubStack's Streams Intro: [**github.com/substack/stream-handbook**](http://github.com/substack/stream-handbook)
- Max's stream intro: http://maxogden.com/node-streams.html
- http://ejohn.org/blog/node-js-stream-playground
- http://codewinds.com/blog/2013-08-04-nodejs-readable-streams.html


## Background

### "It Cannot Be Done" (Challenge Accepted!)

According to
[this StackOverflow Q/A](http://stackoverflow.com/a/17326079/1148249)
stream-uploading large files to S3
is "not possible" because S3 requires the file-size up-front.
(i.e. before you can upload the file you need to tell S3 its size
  and since we are streaming the file in chunks we don't know
  its size before hand... or so the answer suggests.)


# To update
- [ ] http://stackoverflow.com/questions/25156716/how-to-apply-async-on-for-loop-of-range
- [ ] http://stackoverflow.com/questions/17309559/stream-uploading-file-to-s3-on-node-js-using-formidable-and-knox-or-aws-sdk
(requires using the HTML5 File API to get the File Size/Mime client-side...)
