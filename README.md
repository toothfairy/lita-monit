# lita-monit

Lita-monit is a simple handler to catch monit notifications and forward them directly into your chat.

## Installation

Add lita-monit to your Lita instance's Gemfile:

``` ruby
gem "lita-monit"
```

## Configuration

There are two configuration options provided:

**token** - is a token string to confirm that it's real monit alert. By default token string is null. So no validation happens and anyone can send notification to your handler. Adding that configuration option is recommended.

**rooms** - JIDs of rooms to send notification. Default value is :all.

## Usage

To send **monit** notifications you need to make a simple shell script:

``` shell
#!/bin/sh
/usr/bin/curl -s \
  -F "message=$HOST" \
  -F "service=$SERVICE" \
  -F "description=$DESCRIPTION" \
  -F "token=**token**"\
  http://0.0.0.0:8080/monit
```

By default lita listens 8080 port. Don't forget to add token to configuration options.
After that you can add following to your monitrc config
``` shell
check program check-mysql with path "/opt/monit/check_mysql.sh"
     if status != 0 then exec /home/user/monit.sh
```
to call notification for certain events

## License

[MIT](http://opensource.org/licenses/MIT)
