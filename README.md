# ssh_yes

Tired of answering 'yes' every time when you connect to a new server via ssh?
This smal expect script will help you!) If connecting first time it'll send 'yes' on ssh's request.
But firs expect have to be installed:

    sudo apt-get install -y expect

It's already wraped in bash function ssh_yes so you can insert it in your existing shell scrips.
Function accepts ssh address via 1st option:
    $1 - ssh address with parameters(if needed)

Usage example:
    ssh_yes "-p22 user@localhost"

<pre>
function ssh_yes () {
expect << EOF
spawn ssh $1 $2
expect {
    "(yes/no)?" {
        send "yes\n"
        expect {
            "assword:" { exit }
            "$ "       { send "exit\n" }
        }
    }
    "assword:" { exit }
    "$ "       { send "exit\n" }
}
exit
EOF
}
</pre>

