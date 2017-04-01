## Fix Python 3.6 venv on Ubuntu

On Ubuntu, after installing Python 3.6, the command 'python3.6 -m venv testing' produces the error:
'Error: Command '['/home/ubuntu/obeythetestinggoat/bin/python3.6', '-Im', 'ensurepip', '--upgrade', '--default-pip']' returned non-zero exit status 1.'

To fix it, update the python3.6-venv package:

```shell
sudo apt-get install python3.6-venv
```