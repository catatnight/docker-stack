docker-nginx-nodejs
==========

 A Dockerfile which produces a docker image that runs Nginx with Node.js.

## Requirement
+ Docker 1.0

## Features
+ Ubuntu Trusty
+ Nginx 1.6
+ Node.js latest
+ Rsyslog and logrotate

## Usage
1. save nodejs source code and nginx config file

	```
	nginx-nodejs/
	 |-Dockerfile			<-- required: Dockerfile
	 |-src/					<-- required: nodejs source code
	 |-nginx/
	 	|-sites-enabled/	<-- required: nginx config file
	 	|-www/ 				<-- optional: static files
	 	|-certs/			<-- optional: ssl certs

	```
2. edit your own Dockerfile

	```bash
	From catatnight/nginx-nodejs
	...
	```
3. build image and run

	```bash
	docker build -t mysite .
	docker run -p 80:80 --name mysite -d mysite
	```

## Note
The image assumes that your application:

- has a file named [`package.json`](https://www.npmjs.org/doc/json.html) listing its dependencies.
- has a file named `server.js` as the entrypoint script or define in `package.json` the attribute: `"scripts": {"start": "node <entrypoint_script_js>"}` ([example](https://github.com/GoogleCloudPlatform/nodejs-docker/tree/master/runtime))

## Reference
+ [google/nodejs-runtime](https://github.com/GoogleCloudPlatform/nodejs-docker/tree/master/runtime)
+ TBD
