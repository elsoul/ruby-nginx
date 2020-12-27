# Docker Nginx for Ruby APP
Docker Nginx for Ruby APP. No Configuration, No files.
Just Run Docker and Your Ruby APP's Ready for `localhost:80`

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

```ruby
  docker create network shared
```

2. Run Ruby APP
```ruby
  docker run -d --name web \
      -p 3000:3000 \
      --network shared \
      poppinfumi/ruby-nginx:latest
```

※docker run option arguments are fixed

3. Run ruby-nginx Container

```ruby
  docker run -d --name nginx \
      -e VIRTUAL_HOST=el-soul.com \
      -e LETSENCRYPT_HOST=el-soul.com \
      -e LETSENCRYPT_EMAIL=info@gmail \
      --network shared \
      --link web \
      poppinfumi/ruby-nginx:latest
```

※You can set your domain in case you need SSL in your future.


[http://localhost](http://localhost)


## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/elsoul/ruby-nginx. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [Apache-2.0 License](https://www.apache.org/licenses/LICENSE-2.0).

## Code of Conduct

Everyone interacting in the HotelPrice project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/elsoul/ruby-nginx/blob/master/CODE_OF_CONDUCT.md).
