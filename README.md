# SSH Private key buildpack for Buildpacks v3

builds upon work done [here](https://github.com/debitoor/ssh-private-key-buildpack)

Used as part of a chain of buildpacks, allows the use of ssh keys inside a builder

## Usage

inside another buildpack
```bash
#!/usr/bin/env bash
set -eo pipefail

layersdir=$1
env_dir=$2/env

export SSH_DIRECTORY="$(cat $env_dir/SSH_DIRECTORY)"

echo "---> Java Buildpack" 
if [[ $SSH_DIRECTORY ]] ; then
  bash $SSH_DIRECTORY/setup-ssh
fi

# git clone git@github.com:username/private-repo.git
...
```

then build your app using

`pack build --env="SSH_PRIVATE_KEY=$(cat ~/.ssh/id_rsa)" --path=/path/to/app --buildpacks=path/to/private-ssh-pack,path/to/language-pack`
