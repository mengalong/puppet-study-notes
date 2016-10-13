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

## 3.2 安装
