How to install puppet
=====================
# 1. environment：
1. 操作系统：CentOS Linux release 7.2.1511 (Core)
2. 虚拟机：VirtualBox
3. Puppet：4.7

# 2. 安装ruby
<pre><code>yum install ruby</code></pre>

# 3. 安装puppet-server
## 3.1 前置：新安装的centos系统的源列表中可能没有puppet，因此需要首先更新centos的源
<pre><code>
1. 更新方法，备份：
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
2. 下载163的源
cd /etc/yum.repos.d/ && wget http://mirrors.163.com/.help/CentOS6-Base-163.repo
3. 更新：yum clean && yum makecache
4. 将puppet加入源：
sudo rpm -Uvh https://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm
</code></pre>
## 3.2 安装
1. yum install puppetserver
2. 这里可能yum下载速度太慢，我是直接下载下来puppet-agent和puppet server的rpm包自己装，具体的下载链接可以在执行yum安装的时候看到
3. puppet有agent机器和server机器，两个上边都可以同时安装puppet-agent和puppetserver

## 3.3 配置：
1. 机器名修改，我这里使用的是centos7，其中具体的机器和ip如下：
<pre><code>
	-server机器：
            - IP: 192.168.1.103
            - 机器名：along-server
            - 修改方法：hostnamectl --static set-hostname ‘along-server'
        - agent机器：
            - IP: 192.168.1.104
            - 机器名：along-client
            - 修改方法：hostnamectl --static set-hostname ‘along-client'
</code></pre>
2. 配置修改
<pre><code>
        - 修改server机器的:/etc/puppetlabs/puppet/puppet.conf
            - 在master字段下增加一项配置：certname = along-server  #指明本机的cert名字为along-server
        - 修改client机器的：/etc/puppetlabs/puppet/puppet.conf
            - 增加如下配置：
                - [agent]
                - server = along-server      #指明server机器名,未来client机器将会和这个机器建立连接
                - certname = along-client   #指明本机的cert名字为along-client
</code></pre>

# 4. 启动puppet服务，在server和client机器上分别执行：service puppet start
<pre><code>启动之后，可以用puppet status 来查看服务运行状态</code></pre>

# 5. 在puppetserver的就上执行puppet cert sign <NAME>，授权client机器的链接
# 6. 可以执行 puppet cert list 来查看已经注册上的agent
