# notes-elixir

### Mix
```sh
# List all archive
mix archive
# Remove an archive
mix archive.uninstall phoenix_new-1.0.3.ez
# Install archive
mix archive.install https://github.com/phoenixframework/phoenix/releases/download/v1.0.4/phoenix_new-1.0.4.ez

# Get dependecies
mix deps.get
```

### Phoenix
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
mix archive.install https://github.com/phoenixframework/phoenix/releases/download/v1.0.4/phoenix_new-1.0.4.ez

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

--
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/80x15.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">notes-elixir</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://jimmy-beaudoin.com" property="cc:attributionName" rel="cc:attributionURL">Jimmy Beaudoin</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
