# ssh_yes

Tired of answering 'yes' every time when you connect to a new server via ssh?<br>
This smal expect script will help you!) If connecting first time it'll send 'yes' on ssh's request.<br>
But first expect have to be installed:<br>

<pre>
    sudo apt-get install -y expect
</pre>

It's already wraped in bash function <b>ssh_yes</b> so you can insert it in your existing shell scrips.<br>

<pre>
ssh_yes() {
assword='
    "assword:" { exit }
    "$ "       { send "exit\n" }
'
expect <<  EOF
spawn  ssh $1
expect {
    "yes/no" {
        send "yes\n"
        expect { $assword }
    }
    $assword
}
EOF
}
</pre>

Function accepts ssh address via 1st option, usage example:<br>

<pre>
    ssh_yes "-p22 user@localhost"
</pre>

