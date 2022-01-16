# Cloning a Pull Request
Test a pull request without merging it over your master repo.

1. Clone a fresh copy
```bash
git clone https://REPO_URL_HERE.git
```

2. Change into the directory
```bash
cd REPO_DIRECTORY_HERE
```

3. Clone the pull-request number (replace **5** with the # of the PR from the particular repo)
```bash
git pull origin pull/5/head
```

4. Test the pull request!

# Git Commands
I use git almost daily so I don't really need my cheat-sheet anymore, but there are always instances that call for uncommon scenarios.

Taking note of these, so I don't have to dig for them the next time they're needed.

## See unpublished commits
Stuff that got added after `git add filename`
```bash
git cherry -v
```

## Undo an unpublished commit (without losing the code changes)
```bash
git reset --soft HEAD~;
```

## Delete a Commit from the History (Plus it's contents)
If you committed a mistake to the repo that shouldn't stay in the history; a hard reset can clean it up - providing it's executed rapidly.  If other systems/users have already received this commit, this will cause a mess.

For use in situations where you know nobody pulled, yet:
1. Run `git log` and get the commit hash of the commit you want to return to (delete everything else after)
2. Reset it:
```bash
git reset --hard [commit hash]
```

3. Force push it to the repo:
```bash
git push -f
```

All should be well

***

## Specify an SSH Key During `git push`
This error:
> Pushing to git@bitbucket.org:username/repo.git
>
> Forbidden
>
> fatal: Could not read from remote repository.

typically occurs when Bitbucket doesn't find the key it expects to see. (id_rsa, usually)

- Host = alias for bitbucket.org
- HostName = actual destination for the alias
- IdentityFile = path to your preferred SSH key
- IdentitiesOnly = override sending the wrong key for multiple users/identities (identities are tried in sequence)

In your local `~/.ssh/config`:
```bash
Host bblocal
HostName bitbucket.org
IdentityFile ~/.ssh/keyname
IdentitiesOnly yes
```

In the repo's `.git/config`:
- All spots where you have entries like `git@bitbucket.org:username/repo.git` change `bitbucket.org` to your alias: `bblocal`

### Example
From:
```bash
url = git@bitbucket.org:username/repo.git
pushurl = git@bitbucket.org:username/repo.git
```

To:
```bash
url = git@bblocal:username/repo.git
pushurl = git@bblocal:username/repo.git
```


# Sign_and_Send_Pubkey Error when Running Git Push
Error:
```text
Jarelan@debian$ /repo[master *]: git push
sign_and_send_pubkey: signing failed: agent refused operation
Forbidden
fatal: Could not read from remote repository.
```

This occured after an in-place OS update from stretch to buster.  Check the permissions of the SSH key you're using:
```bash
ls -l ~/.ssh
```
Permissions of the affected key:
```text
-rw-r--r-- 1 angela angela  1766 Aug 14  2018 id_rsa
-rw-r--r-- 1 angela angela   395 Aug 14  2018 id_rsa.pub
```

Assign proper permissions to the affected key(s):
```bash
chmod 600 id_rsa && chmod 644 id_rsa.pub
```

Correct permissions:
```text
-rw------- 1 Jarelan Jarelan  1766 Aug 14  2018 id_rsa
-rw-r--r-- 1 Jarelan Jarelan   395 Aug 14  2018 id_rsa.pub
```

Run `git push` again and it should work!
