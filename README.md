# ssh_yes

Tired of answering 'yes' every time when you connect to a new server via ssh?<br>
This small script will help you!)

It's already wraped in bash function <b>ssh_yes</b> so you can insert it in your existing shell scrips.<br>

<pre>
ssh_yes() {
    local target=$1
    local knwhosts=${2:-~/.ssh/known_hosts}
    local fprint=($(ssh-keyscan -H "$target" 2>/dev/null)) || return 1
    grep -q "${fprint[2]}" "$knwhosts" 2>/dev/null || echo "${fprint[@]}" >> "$knwhosts"
}
</pre>

Function accepts server's IP address via 1st option, and path to known_hosts as second if
it's different from default, usage example:<br>

<pre>
    ssh_yes 192.168.0.1 [/my/path/to/known_hosts|default is ~/.ssh/known_hosts]
</pre>

