# haproxy

## http://www.haproxy.org/

###Installation

#### Install Lua
* wget http://www.lua.org/ftp/lua-5.3.1.tar.gz
* tar xf lua-5.3.1.tar.gz
* cd lua-5.3.1
* make generic
* mkdir ../lua-5.3.1_install
*  make install INSTALL_TOP=/path/to/lua/lua-5.3.1_install
    
#### Install haproxy
* git clone http://git.haproxy.org/git/haproxy-1.6.git/
* cd haproxy-1.6
* On macosx change --export-dynamic to -export_dynamic in Makefile
* make TARGET=generic USE_DL=1 USE_LUA=1 USE_OPENSSL=1 SSL_LIB=/path/to/openssl/lib SSL_INC=/path/to/openssl/include LUA_LIB=/path/to/lua/lua-5.3.1_install/lib LUA_INC=/path/to/lua/lua-5.3.1_install/include
* mkdir ../haproxy-1.6_install
* make PREFIX=/path/to/haproxy/haproxy-1.6_install install


#### Running haproxy
* cd ../haproxy-1.6_install/
* create a file called hello_world.lua
```lua
core.register_service("hello-world", "http", function(applet)
        local response = "Hello World !"
        applet:set_status(200)
        applet:add_header("content-length", string.len(response))
        applet:add_header("content-type", "text/plain")
        applet:start_response()
        applet:send(response)
    end)
```
* create the config file hello_world.cfg
```lua
global
       lua-load hello_world.lua

        defaults
            mode http
            timeout connect 5000ms
            timeout client 50000ms
            timeout server 50000ms

        frontend example
            bind 127.0.0.1:10001
            http-request use-service lua.hello-world


        listen stats
            # Uncomment "disabeled" below to disable the stats page :
            # disabled
            bind       :8888
            stats uri /
```
* Check if config is valid
```bash
sbin/haproxy -f hello_world.cfg -c
```
* sbin/haproxy -f hello_world_content.cfg
* curl -v 127.0.0.1:10001
      
    

