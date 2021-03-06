HTTPServer [![Build Status](https://secure.travis-ci.org/parroty/http_server.png?branch=master "Build Status")](http://travis-ci.org/parroty/http_server)
============
A simple and self-contained HTTP Server for elixir.
It's intended for simple testing of HTTP request/response without setting up stand-alone http server.

### Usage
Add `:http_server` to `mix.exs` to initialize its dependencies.
```Elixir
defmodule HttpServerTest.Mixfile do
  use Mix.Project

  def application do
    [ applications: [:http_server] ]
  end
```

Use `HttpServer.start` to define responses.
```Elixir
defmodule HttpServerTest do
  use ExUnit.Case

  setup_all do
    HTTPotion.start
  end

  test "test default server response" do
    HttpServer.start
    response = HTTPotion.get("http://localhost:8080")
    assert(response.body == "Hello World")
  end

  test "test custom server response" do
    HttpServer.start(path: "/test", port: 4000, response: "Custom Response")
    response = HTTPotion.get("http://localhost:4000/test")
    assert(response.body == "Custom Response")
  end
end
```
