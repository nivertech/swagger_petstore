
# SwaggerPetstore

This is a sample server Petstore server.  You can find out more about     Swagger at [http://swagger.io](http://swagger.io) or on [irc.freenode.net, #swagger](http://swagger.io/irc/).      For this sample, you can use the api key &#x60;special-key&#x60; to test the authorization     filters.

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `swagger_petstore` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [{:swagger_petstore, "~> 0.1.0"}]
end
```

Documentation can be generated with [ExDoc](https://github.com/elixir-lang/ex_doc)
and published on [HexDocs](https://hexdocs.pm). Once published, the docs can
be found at [https://hexdocs.pm/swagger_petstore](https://hexdocs.pm/swagger_petstore).


# How to generate Elixir code

``` bash
# pull required docker images
docker pull trinitronx/python-simplehttpserver
docker pull swaggerapi/swagger-codegen-cli


docker network create foo

docker run -h server --name=server --network=foo --rm -v $(pwd):/var/www:ro -p 8080:8080 trinitronx/python-simplehttpserver

docker run --network=foo --rm -v  ${PWD}:/local swaggerapi/swagger-codegen-cli generate -i petstore.yml -l elixir -o /local/elixir
```

# How to run

``` elixir
alias SwaggerPetstore.Connection
alias SwaggerPetstore.Api.Store                 

token = "special-key" 

iex(8)> conn = Connection.new(token)
%Tesla.Client{
  adapter: nil,
  fun: nil,
  post: [],
  pre: [
    {Tesla.Middleware.Headers, :call,
     [[{"authorization", "Bearer special-key"}]]}
  ]
}

iex(12)> {ok, inventory} = Store.get_inventory(conn)
{:ok,
 %{
   "1234567891234" => 1,
   "767778" => 1,
   "AVAILABLE" => 14,
   "Nonavailable" => 1,
   "Not Found" => 1,
   "OFF" => 1,
   "ON" => 4,
   "PENDING" => 18,
   "Pending" => 2,
   "Ready" => 1,
   "Reserved" => 1,
   "SOLD" => 20,
   "amet" => 1,
   "available" => 1062,
   "available;pending;sold" => 4,
   "avaliable" => 1,
   "c" => 1,
   "def" => 1,
   "ksks" => 1,
   "pending" => 355,
   "snatched" => 2,
   "sold" => 358,
   "string" => 30,
   "swimming" => 1,
   "unavailable" => 2,
   "{{petStatus}}" => 1
 }}

```
