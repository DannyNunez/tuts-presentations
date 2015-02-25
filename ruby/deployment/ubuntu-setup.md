sudo apt-get update 
sudo apt-get install build-essential git-core python-software-properties nodejs

sudo curl https://raw.githubusercontent.com/fesplugas/rbenv-installer/master/bin/rbenv-installer | bash 

vim ~/.bash_profile 

```
export RBENV_ROOT="${HOME}/.rbenv"

if [ -d "${RBENV_ROOT}" ]; then
  export PATH="${RBENV_ROOT}/bin:${PATH}"
  eval "$(rbenv init -)"
fi
```

source ~/.bash_profile 

rbenv install 2.0.0-p0

rbenv global 2.0.0-p0

gem install bundler