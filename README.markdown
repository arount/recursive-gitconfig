recursive-gitconfig
===================

`recursive-gitconfig` is a Bash tool to support several `.gitconfig` within the same Linux session.

It can also be use to handle several dynamic Git identities.


Install
-------

Copy the file `recursive-gitconfig` in your home folder and source it in your `.bashrc`.


    cp recursive-gitconfig.sh ~/.recursive-gitconfig.sh
	sed -i '1asource ~/.recursive-gitconfig.sh\n' ~/.bashrc


How it works
------------

`recursive-gitconfig.sh` alias `git` command to look for the closest `.gitconfig` file in parents folders and use this one instead of the default `~/.gitconfig`.

### An example

Let's say your home directory is something like:

	├── .gitconfig
	├── personal
	│   ├── .gitconfig
	│   ├── project-one
	│   ├── project-three
	│   └── project-two
	└── work
	    ├── client-project-one
	    ├── client-project-two
	    └── .gitconfig

You basicaly have two main folders, `personal` and `work` and subfolders for each project.

Your main config file is `~/.gitconfig` but you added two specifics files `~/work/.gitconfig` and `~/personal/.gitconfig`.


`~/.gitconfig`:


	[user]
		email = pierre@arount.info
		name = Arnout Pierre

	[color]
		lol = log --graph --decorate --pretty=oneline --abbrev-commit
		lola = log --graph --decorate --pretty=oneline --abbrev-commit --all



`~/work/.gitconfig`:


	[user]
		email = pierre.arnout@company.com
		name = Arnout Pierre (Company)
	[include]
		path = /home/arount/.gitconfig



`~/personal/.gitconfig`:


    [user]
		name = Arount
	[include]
		path = /home/arount/.gitconfig


From here there are three specific identities possible to have on the same session,


 + `Arnout Pierre` / `pierre@arount.info` is my default identity, the fallback and will be used everywhere except `~/work` and `~/personal`.
 + `Arnout Pierre (Company)` / `pierre.arnout@company.com` is my professional identity, only used under `~/work/`.
 + `Arount` / `pierre@arount.info` is my personal identity, for my personal projects, only used under `~/personal/`.


Because both of my specific `.gitconfig` files include the default `~/.gitconfig` I still access my alias from any identity.


Bugs
----

If you experience a bug, please check `recursive-gitconfig.sh` is sourced at the top of your `.bashrc`.

Otherwise feel free to submit an issue or PR.

