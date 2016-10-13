# 1. 更新某个目录下的文件
<pre><code>
class update_file {
        file { "/var/www/html/test_along":
                source => "puppet:///modules/update_file/test_along.txt"
        }
        Exec { path => ["/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/opt/puppetlabs/bin:"],
                user => "root",
                cwd => "/var/www/html",
        }
        exec {"deploy_it":
                command => "echo \"nothing to do it\"",
                require => File["/var/www/html/test_along"]
        }
}
</code></pre>

# 2.修改crontab
<pre><code>
class update_cron {
        file { "/root/cron/":
                ensure => "directory",
                source => "puppet:///modules/update_cron/cron",
                recurse => true,
        }
        Exec {
                path => ["/usr/lib64/qt-3.3/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/opt/puppetlabs/bin:/home/mengalong/.local/bin:/home/mengalong/bin"],
                user => "root",
                cwd => "/root/cron",
        }
        exec { "exec_cron":
                command => "crontab aa",
                require => File["/root/cron"],
        }
}
</code></pre>

# 3. 执行指定的脚本
<pre><code>
class exec_shell {
    file { "/root/do_it.sh":
        source => "puppet:///modules/exec_shell/do_it.sh",
    }
    Exec {
        path => ["/usr/lib64/qt-3.3/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/opt/puppetlabs/bin:/home/mengalong/.local/bin:/home/mengalong/bin"],
        user => "root",
        cwd => "/root",
    }
    exec { "exec_command":
        command => "bash do_it.sh",
        require => File["/root/do_it.sh"],
    }
}
</code></pre>
