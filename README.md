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



      
    

