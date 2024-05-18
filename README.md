# Ansible Collection - lanefu.armlab

Documentation for the collection.

## my own notes

### subtrees

I like subtrees of other roles.  sometimes i'll fork role and then push changes back up

#### slurping role to subtree

example for zfs role

`git subtree -P roles/zfs add https://github.com/mrlesmithjr/ansible-zfs.git master`

```bash
ROLE_NAME=rolename
REPO=git subtree -P roles/zfs add https://github.com/mrlesmithjr/ansible-zfs.git master
REPO_BRANCH=master

git subtree -P roles/${ROLE_NAME} add ${REPO} ${REPO_BRANCH}
```
