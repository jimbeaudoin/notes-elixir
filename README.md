# notes-elixir

### Mix
```sh
# List all archive
mix archive
# Remove an archive
mix archive.uninstall phoenix_new-1.0.3.ez
# Install archive
mix archive.install https://github.com/phoenixframework/phoenix/releases/download/v1.1.0/phoenix_new-1.1.0.ez

# Get dependecies
mix deps.get
```

### Phoenix
**Installation**
```sh
# Ubuntu 15.10 (wily)
sudo apt-get install inotify-tools
wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && sudo dpkg -i erlang-solutions_1.0_all.deb
wget http://packages.erlang-solutions.com/ubuntu/erlang_solutions.asc
sudo apt-key add erlang_solutions.asc
sudo apt-get update
sudo apt-get install esl-erlang
sudo apt-get install elixir
mix local.hex
mix archive.install https://github.com/phoenixframework/phoenix/releases/download/v1.1.0/phoenix_new-1.1.0.ez

# Dev Database Setup
sudo su - postgres
psql
ALTER ROLE postgres WITH PASSWORD 'postgres';

# Changeset
def changeset(model, params \\ nil) do
  model
  |> cast(params, @required_fields, @optional_fields)
  |> validate_unique(:username, on: Phitter.Repo, downcase: true)
  |> validate_length(:password, min: 1)
  |> validate_length(:password_confirmation, min: 1)
  |> validate_confirmation(:password)
end
```
**Update dependencies**
```sh
# Update all
mix deps.update --all
# Update phoenix
mix deps.update phoenix
```
**Cheat Sheet**
```sh
# Generate a new application
mix phoenix.new <app_name> 
# Generate a new application with binary ID
mix phoenix.new <app_name> --binary-id
```

**JSON API**
```
# config/config.exs
config :plug, :mimes, %{
  "application/vnd.api+json" => ["json-api"]
}

# web/router.ex
pipeline :api do
  plug :accepts, ["json-api"]
end

touch deps/plug/mix.exs
mix deps.compile plug
```

### Debugger
```
require IEx;
IEx.pry
```

### Logger
```
require Logger
Logger.info "TEST"
```

### Presence
```
defmodule RoomChannel do
  use Phoenix.Channel
  
  def join() do
    send self(), :after_join
    {:ok, socket}
  end
  
  def handle_info(:after_join, socket) do
    id = socket.assigns.user_id
    push socket, "presence_state", Presence.list(socket)
    Presence.track(socket, id, %{status: "available"})
    {:noreply, socket}
  end
end

Presence.track("services", "email", %{
  pid: self(),
  max_jobs: 100,
  work_load: 0
})

Presence.list("services")
=> %{"email" => [...]}
```

### Notes
```
# This is not recommended, this code is going to spawn a OS process
{status, _} = System.cmd("s3cmd", ["-P", "put", filename, s3_name])

# Tuples
data = {:ok, response}
elem(data, 0) => :ok
elem(data, 1) => response
```

--
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/80x15.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">notes-elixir</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://jimmy-beaudoin.com" property="cc:attributionName" rel="cc:attributionURL">Jimmy Beaudoin</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
