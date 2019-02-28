# Python获取外网IP地址

最简洁的方法就是直接获取网络服务商提供的获取本机IP地址的查询网站。
我们可以使用 <http://ip.42.pl/raw> 这个网站来实现。
代码如下：

    from urllib.request import urlopen

    def get_wan_ip():
        '''
        get the wan ip of current pc.
        '''
        my_ip = urlopen("http://ip.42.pl/raw")
        return my_ip.read()

这种方式依赖于所访问的网站是否有效，但是胜在简单。