php 默认 php-fpm 数量

PHP的默认php-fpm进程数量是由系统决定的，通常是比较保守的。在安装PHP和php-fpm时，这些设置可以在配置文件中进行更改。例如，可以修改php-fpm.conf文件中的以下选项来更改进程数量：
```
pm.max_children = 5  # 设置php-fpm进程最多可以同时启动5个 
 
pm.start_servers = 2 # 设置启动时默认有2个进程 
 
pm.min_spare_servers = 1 # 设置最少保持1个进程不被停用 
 
pm.max_spare_servers = 3 # 设置最多保持3个进程不被停用 
```
以上是示例配置，您可以根据需要自行更改。需要注意的是，更改这些配置可能会对系统性能产生影响，应该慎重考虑。
