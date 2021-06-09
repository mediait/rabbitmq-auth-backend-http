### Prerequisites
* GNU make
* mercurial version control system to clone the required dependencies
* Erlang compiler (the recommended way is to use [official upstream packages](erlang-solutions.com/downloads/download-erlang-otp))

### Dependencies fetching

RabbitMQ plugins are built inside a specifically set up environment.

```bash
hg clone http://hg.rabbitmq.com/rabbitmq-public-umbrella # Clone the official repo for plugin development
cd rabbitmq-public-umbrella
make co # Fetch the submodules and dependencies
git clone https://github.com/mediait/rabbitmq-auth-backend-http.git # Fetch our plugin source

mkdir ets-cache # Folder will contain the only external dependency
cd ets-cache
wget https://gist.githubusercontent.com/kirushik/a2888fbabe29cdbd6c6c/raw/fd7d5cf23c45d2dcd7c910bdf20ae836db8c1ed4/package.mk
# You've just fetched the library definition. The rest will be handled by the plugin build system
```

### Plugin build process

```bash
cd ../rabbitmq-auth-backend-http/ # Navigate to our plugin folder
make dist # Run the build and packaging process, will take some time
```
All the required packages will be placed in the `dist` subfolder.

The resulting `dist` folder should be archived and committed into https://github.com/mediait/mtv-cookbooks/tree/master/cookbooks/mtv/resources/rabbitmq_auth_http as a `plugins-cache.tar.gz` file.