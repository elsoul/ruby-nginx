# Docker Nginx for Ruby APP
Docker Nginx for Ruby APP. No Configuration, No files.

Just Run Docker and Your Ruby APP's Ready for localhost.

<p align="center">

  <a aria-label="Ruby logo" href="https://el-soul.com">
    <img src="https://badgen.net/badge/icon/Made%20by%20ELSOUL?icon=ruby&label&color=black&labelColor=black">
  </a>
  <br/>
</p>


## Dependency
- [Docker](https://www.docker.com/)



## Usage

1. Create Docker Network

```
docker network create --driver bridge shared
```


2. Run Ruby APP
```
docker run -d --name web \
    -p 3000:3000 \
    --network shared \
    poppinfumi/ruby-nginx:latest
```

※docker run option arguments are fixed

3. Run ruby-nginx Container

```
docker run -d --name nginx \
    -e VIRTUAL_HOST=el-soul.com \
    -e LETSENCRYPT_HOST=el-soul.com \
    -e LETSENCRYPT_EMAIL=info@gmail \
    --network shared \
    --link web \
    poppinfumi/souls_api:latest
```

※You can set your domain in case you need SSL in your future.


Now you can see your app;

[http://localhost](http://localhost)


## HTTPS / SSL (Optional)

4. Create  Proxy 

```
docker run -d --name proxy \
    -p 80:80 -p 443:443 \
    -v "/var/run/docker.sock:/tmp/docker.sock:ro" \
    -v "/home/certs:/etc/nginx/certs:ro" \
    -v "/etc/nginx/vhost.d" \
    -v "/usr/share/nginx/html" \
    --network shared \
    --restart always \
    jwilder/nginx-proxy
```


5. Create Let's Encrtypt

```
docker run -d --name letsencrypt \
    -v "/home/certs:/etc/nginx/certs" \
    -v "/var/run/docker.sock:/var/run/docker.sock:ro" \
    --volumes-from proxy \
    --network shared \
    --restart always \
    jrcs/letsencrypt-nginx-proxy-companion
```

Check Docker Containers

```
docker ps
```

You can see 4 containers running

```
CONTAINER ID        IMAGE                                    COMMAND                  CREATED             STATUS              PORTS                                      NAMES
608cb6742535        poppinfumi/ruby-nginx:latest             "nginx -g 'daemon of…"   2 hours ago         Up 2 hours          80/tcp                                     nginx
029b2052c2c8        poppinfumi/souls_api:latest              "foreman start"          3 hours ago         Up 3 hours          0.0.0.0:3000->3000/tcp                     web
5445e369dc7d        jrcs/letsencrypt-nginx-proxy-companion   "/bin/bash /app/entr…"   5 hours ago         Up 5 hours                                                     letsencrypt
67dc0f4622dc        jwilder/nginx-proxy                      "/app/docker-entrypo…"   5 hours ago         Up 5 hours          0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   proxy
```



Now Your Ruby APP on HTTPS


[https://el-soul.com](https://el-soul.com)



※You need to do DNS settings with your domain




## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/elsoul/ruby-nginx. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [Apache-2.0 License](https://www.apache.org/licenses/LICENSE-2.0).

## Code of Conduct

Everyone interacting in the HotelPrice project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/elsoul/ruby-nginx/blob/master/CODE_OF_CONDUCT.md).
