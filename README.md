# Authenticating Git(Hub) via SSH

Since existing solutions and guides are inconsistent with newer versions of the GitHub 
workflow and interface, I would like this repository to serve as a solution to SSH 
authentication until it follows the same fate.

# Background

Since forever ago (November 2021), GitHub removed HTTPS authentication for contribution
signatures and required developers switch to the secure shell protocol (SSH) (or GPG) for 
user verification (I won't concern you nor myself with why).

An issue with the way GitHub handles SSH authentication -- which, admittedly, myself and 
a few others have dealt with countless times -- is that it's super easy to forget the
steps necessary to properly set up SSH authentication, since it's something that's done 
once and is forgotten before the brain can intuit how to do any of it (it doesn't help that 
it's somewhat GitHub-specific). I personally cannot be asked to re-read
the guide every time I just want to quickly push something before going to do something else
(maybe this is a me problem).

Anyways, I'll try to keep this repo updated. Contributions are welcome.

# Linux/BSD
If anyone wants to add Mac/Windows sections, feel free to PR.

## tl;dr - Per-Repository Authentication 
1. Generate local SSH key via `ssh-keygen -t ed25519 -a 100 -C github_linked_email@whatever.com`

[comment]: <> (`-a 100` courtesy of https://github.com/CapnRyna : "makes key significantly harder to brute-force crack")
> SHA-2 signed RSA keys are valid as well 

2. Add key to ssh-agent via `eval "$(ssh-agent -s)" && ssh-add <private SSH key path>`

> The official GitHub guide specifies running `ssh-agent -s` via `eval`, though I'm not sure why.

3. Create SSH key on GitHub `Profile icon in top-right > Settings > SSH and GPG keys`, add 
key and follow steps

> NOTE: You only have to do the first 3 steps ONCE per system.

4. Set git-url to SSH endpoint (in local repo) `git remote add origin git@github.com:OWNER/REPOSITORY.git`

5. Verify connection validity with `ssh -T git@github.com`

6. To avoid invalid attribution (commits not counting as your own), make sure to set your identity in the config:

```sh
cd "<path to local repository>"
git config user.name "<your username>"
git config user.email "<your github email>" 
```

> If you want these settings to apply globally, then call `git config --global ...` instead.

## tl;dr - System-Wide Authentication (WIP)
Nothing, yet.

## Not Long Enough, Read (WIP)
### References
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account

https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories#switching-remote-urls-from-https-to-ssh

TODOs:
- [ ] Finish long section(s) 
