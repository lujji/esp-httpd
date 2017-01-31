# esp-httpd
This is a basic HTTP server with WebSockets for ESP8266 based on httpd from LwIP.

This server was intended to be used with [esp-open-rtos](https://github.com/SuperHouse/esp-open-rtos), although it should work with non-RTOS version of SDK, since httpd is based on callbacks.

WebSockets implementation supports binary and text modes. Multiple sockets are supported.
Continuation frames are not implemented.

## Building
Run `make html` before building the project in order to generate `fsdata.c` with web contents.

## Configuration
By default, a WebSocket is closed after 20 seconds of inactivity to conserve memory. This behavior can be changed by overriding `WS_TIMEOUT` option.

To enable debugging extra flags `-DLWIP_DEBUG=1 -DHTTPD_DEBUG=LWIP_DBG_ON` should be passed at compile-time.

## Code Structure
Example code is located inside `http_server`. It demonstrates streaming ADC reading and server status parameters ([screenshot](https://lujji.github.io/blog/esp-httpd/websocket_demo.png)). Web-page contents are located inside `fsdata/fs` subdirectory. Httpd expects a `fsdata.c` file, which contains C structures generated from the contents of `fs` folder. This file is created with `makefsdata` Perl utility.