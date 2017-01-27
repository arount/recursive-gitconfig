#!/bin/bash
#
# recursive-gitconfig: Alias git to use closest .gitconfig file found in parents directories.
#
# Quick example:
#
#     # Make dirs & .gitconfig files
#     mkdir -p /tmp/gitenvs/john && mkdir /tmp/gitenvs/jack
#     touch /tmp/gitenvs/john/.gitconfig && touch /tmp/gitenvs/jack/.gitconfig
#
#     # Set values to config files
#     git config -f /tmp/gitenvs/john/.gitconfig --add user.name 'John'
#     git config -f /tmp/gitenvs/john/.gitconfig --add user.email 'john@local'
#
#     git config -f /tmp/gitenvs/jack/.gitconfig --add user.name 'Jack'
#     git config -f /tmp/gitenvs/jack/.gitconfig --add user.email 'jack@local'
#
#     # Create git repositories under config files
#     mkdir /tmp/gitenvs/john/repo/ && git --git-dir /tmp/gitenvs/john/repo/.git init
#     mkdir /tmp/gitenvs/jack/repo/ && git --git-dir /tmp/gitenvs/jack/repo/.git init
#
#     # Commit & test behaviour
#     cd /tmp/gitenvs/john/repo && git commit --allow-empty --message "John's" && git log
#     cd /tmp/gitenvs/jack/repo && git commit --allow-empty --message "Jacks's" && git log
#
# Docs:
#     Please refere to project git repository for more infos. (https://github.com/arount/recursive-gitconfig)
#

# Look for closest .gitconfig file in parent directories
# This file will be used as main .gitconfig file.
function __recursive_gitconfig_git {
    gitconfig_file=$(__recursive_gitconfig_closest)
    if [ "$gitconfig_file" != '' ]; then
        home="$(dirname $gitconfig_file)/"
        HOME=$home /usr/bin/git "$@"
    else
        /usr/bin/git "$@"
    fi
}

# Look for closest .gitconfig file in parents directories
function __recursive_gitconfig_closest {
    slashes=${PWD//[^\/]/}
    directory="$PWD"
    for (( n=${#slashes}; n>0; --n ))
    do
        test -e "$directory/.gitconfig" && echo "$directory/.gitconfig" && return 
        directory="$directory/.."
    done
}


alias git='__recursive_gitconfig_git'
