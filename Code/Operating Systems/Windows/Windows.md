# Windows
## SSH
1:
> ssh-keygen -t rsa -C "your email address"

2:
> eval $(ssh-agent)

3:
> ssh-add ~/.ssh/<private_key_file>

4:
> ssh -T git@bitbucket.org