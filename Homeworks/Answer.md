# Framgia Tranning Workshop - Linux Essential 1
## Homework answer (Group 4)

### Homework 1
- Alternative `rpm` command for `dpkg` command.
  - `dpkg -l` -> `rpm -qa`
  - `dpkg -l {package_name}`: `rpm -qap {package_name}`
  - `dpkg -L {package_name}` -> `rpm -ql {package_name}`
  - `dpkg -i package.deb` -> `rpm -i package.rpm`
  - `dpkg -r {package_name}`: Not found
  - `dpkg -P {package_name}` -> `rpm -e {package_name}`
  - `dpkg -c {package.deb}` -> `rpm -qpl {package.rpm}`
  - `dpkg -p {package_name}`: Not found
  - `dpkg -s {package_name}` -> `rpm -qi {package_name}`
  - `dpkg -S {/path/to/file}` -> `rpm -qf {/path/to/file}`
  - `dpkg --get-selections`: Not found
- Alternative `yum` command for `apt` command.
  - `apt install {package_name}` -> `yum install {package_name}`
  - `apt search {package_name}` -> `yum search {package_name}`
  - `apt remove {package_name}`: Not found
  - `apt purge {package_name}` -> `yum remove {package_name}`
  - `apt policy`: Not found
  - `apt list` -> `yum list`
    - Option: installed (`yum`), --installed (`apt`)
    - Option: available (`yum`), --all-versions (`apt`)
    - Option: --upgradeable (`apt`)
  - `apt update`: Nothing alternative but yum refresh each time it's use
  - `apt upgrade` -> `yum update`
  - `apt autoremove`: Not found
  - `add-apt repository {repository_name}`: Not found


### Homework 2
1. Convert to `deb` package and install: `alien --to-deb --install bless.rpm`
2. First run `alien --to-deb bless.rpm` to convert then `sudo dpkg -i bless.deb` to install

### Homework 3
```bash
alias l5lm='ls -lt | sed -ne 2,6p' 
```

### Homework 4
```bash
function get_ubuntu_code_name() {
  cat /etc/lsb-release | grep "CODENAME" | awk -F "=" '{print $2}'
}

PS1='{$(get_ubuntu_code_name)} \u@\h:\w\$ '
```

### Homework 5
Ease way:
```bash
alias kill_all='killall -e'
```
or use `ps` and `kill` command
```bash
function kill_all {
  if [ ! $1  ]; then
    echo "Need a command or program name"
  else
    pids=$(ps -aux | grep $1 | grep -v grep | awk '{print $2}')
    if [ $pids  ]; then
      kill -9 $pids
    fi
  fi

}
```

### Homework 6
```bash
alias gplo='git pull origin $(git branch | sed -e "/^[^*]/d" -e "s/* \(.*\)/\1/")'
```
