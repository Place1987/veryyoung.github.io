---
layout: post
title: Ubuntu下安装Redis
date: 2014-12-17 14:49
author: VERYYOUNG
comments: true
categories: [Database]
---
<h1>1.下载源码</h1>

<pre><code>wget http://download.redis.io/releases/redis-2.8.19.tar.gz
</code></pre>

<h1>2.解压</h1>

<pre><code>tar -zxf redis-2.8.19.tar.gz 
</code></pre>

<h1>3.make</h1>

<pre><code>make
</code></pre>

<h1>4.install</h1>

<pre><code>sudo make install
</code></pre>

<h1>5.服务配置</h1>

<pre><code>wget https://github.com/ijonas/dotfiles/raw/master/etc/init.d/redis-server
wget https://github.com/ijonas/dotfiles/raw/master/etc/redis.conf 
sudo mv redis-server /etc/init.d/redis-server 
sudo chmod +x /etc/init.d/redis-server 
sudo mv redis.conf /etc/redis.conf
</code></pre>

<h1>6.配置log位置</h1>

<pre><code>sudo useradd redis 
sudo mkdir -p /var/lib/redis 
sudo mkdir -p /var/log/redis 
sudo chown redis.redis /var/lib/redis 
sudo chown redis.redis /var/log/redis
</code></pre>

<h1>7.启动Redis</h1>

<pre><code>sudo /etc/init.d/redis-server start
</code></pre>

<h1>8.客户端测试</h1>

<pre><code>redis-cli
</code></pre>

<h1>9.代码测试</h1>

<p>在pom里添加Jredis的依赖项</p>

<pre><code>import java.util.HashMap;
import java.util.List;
import java.util.Map;

import redis.clients.jedis.Jedis;

/**
* Created by veryyoung on 2014/12/17.
*/
public class RedisTest {


    public static void main(String[] args) {

    //连接redis服务 :第一个参数是redis的IP，第二个参数是redis访问端口
    Jedis jedis = new Jedis("", 6379);

    //密码验证-如果你没有设置redis密码可不验证即可使用相关命令
    //jedis.auth("");

    //简单的key-value 存储
    jedis.set("redis", "myredis");
    System.out.println(jedis.get("redis"));

    //在原有值得基础上添加,如若之前没有该key，则导入该key
    //之前已经设定了redis对应"myredis",此句执行便会使redis对应"myredisyourredis"
    jedis.append("redis", "yourredis");
    jedis.append("content", "rabbit");

    //mset 是设置多个key-value值 参数（key1,value1,key2,value2,…,keyn,valuen）
    //mget 是获取多个key所对应的value值 参数（key1,key2,key3,…,keyn） 返回的是个list
    jedis.mset("name1", "yangw", "name2", "demon", "name3", "elena");
    System.out.println(jedis.mget("name1", "name2", "name3"));

    //map
    Map&lt;String, String&gt; user = new HashMap&lt;String, String&gt;();
    user.put("name", "cd");
    user.put("password", "123456");
    //map存入redis
    jedis.hmset("user", user);
    //mapkey个数
    System.out.println(String.format("len:%d", jedis.hlen("user")));
    //map中的所有键值
    System.out.println(String.format("keys: %s", jedis.hkeys("user")));
    //map中的所有value
    System.out.println(String.format("values: %s", jedis.hvals("user")));
    //取出map中的name字段值
    List&lt;String&gt; rsmap = jedis.hmget("user", "name", "password");
    System.out.println(rsmap);
    //删除map中的某一个键值 password
    jedis.hdel("user", "password");
    System.out.println(jedis.hmget("user", "name", "password"));

    //list
    jedis.del("listDemo");
    System.out.println(jedis.lrange("listDemo", 0, -1));
    jedis.lpush("listDemo", "A");
    jedis.lpush("listDemo", "B");
    jedis.lpush("listDemo", "C");
    System.out.println(jedis.lrange("listDemo", 0, -1));
    System.out.println(jedis.lrange("listDemo", 0, 1));

    //set
    jedis.sadd("sname", "wobby");
    jedis.sadd("sname", "kings");
    jedis.sadd("sname", "demon");
    System.out.println(String.format("set num: %d", jedis.scard("sname")));
    System.out.println(String.format("all members: %s", jedis.smembers("sname")));
    System.out.println(String.format("is member: %B", jedis.sismember("sname", "wobby")));
    System.out.println(String.format("rand member: %s", jedis.srandmember("sname")));
    //删除一个对象
    jedis.srem("sname", "demon");
    System.out.println(String.format("all members: %s", jedis.smembers("sname")));
    }
}
</code></pre>

<p>输入</p>

<pre><code>myredis
[yangw, demon, elena]
len:2
keys: [password, name]
values: [123456, cd]
[cd, 123456]
[cd, null]
[]
[C, B, A]
[C, B]
set num: 3
all members: [wobby, demon, kings]
is member: TRUE
rand member: demon
all members: [wobby, kings]

Process finished with exit code 0
</code></pre>

