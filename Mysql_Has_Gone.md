# Fixing "MySQL server has gone away" error
https://serverfault.com/questions/106323/fixing-mysql-server-has-gone-away-error?rq=1
1. PHP taking long time:

If you are using PHP, the execution time may be longer than MySQL's timeouts. You may want to check net_read_timeout and net_write_timeout against PHP's max_execution_time. If PHP's execution time is longer than 60, then MySQL might disconnect.

2. overloaded server

Since your wait_timeout variable is 8 hours (28800 seconds) You may be bothered by idle MySQL connections. Use the show processlist query to see how much idle threads are running. If you have a lot of idle threads then you might want to lower the wait_timeout directive. I am currently using a value of 60 on production web servers (and nobody has complained yet).

Anyway MySQL obviously needs some settings adjustments. There are a lot of articles around the web talking about MySQL tuning.




# Keep getting "MySQL server has gone away" errors during command line import
https://serverfault.com/questions/167574/keep-getting-mysql-server-has-gone-away-errors-during-command-line-import?rq=1

It is possible one column is a blob, perhaps an image or PDF that is larger than 16M. Why not set the max_allowed_packet to 160MB (as no one packet can be bigger than the entire file size) and test it again, you can always switch it back later.

You can get a more accurate value if you get the data imported use the SHOW TABLE STATUS command to get the data sizes and you will then see how large it should be.
