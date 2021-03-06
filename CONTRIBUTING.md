# Contributing to Recog

The users and maintainers of Recog would greatly appreciate any contributions
you can make to the project.  These contributions typically come in the form of
filed bugs/issues or pull requests (PRs).  These contributions routinely result
in new versions of the [recog gem](https://rubygems.org/gems/recog) and the
[recog release](https://github.com/rapid7/recog/releases) to be released.  The
process for everything is described below.

## Contributing Issues / Bug Reports

If you encounter any bugs or problems with Recog, please file them
[here](https://github.com/rapid7/recog/issues/new), providing as much detail as
possible.  If the bug is straight-forward enough and you understand the fix for
the bug well enough, you may take the simpler, less-paperwork route and simply
fill a PR with the fix and the necessary details.

## Contributing Code

Recog uses a model nearly identical to that of
[Metasploit](https://github.com/rapid7/metasploit-framework) as outlined
[here](https://github.com/rapid7/metasploit-framework/wiki/Setting-Up-a-Metasploit-Development-Environment),
at least from a ```git``` perspective.  If you've been through that process
(or, even better, you've been through it many times with many people), you can
do exactly what you did for Metasploit but with Recog and ignore the rest of
this document.

On the other hand, if you haven't, read on!

### Fork and Clone

Generally, this should only need to be done once, or if you need to start over.

1. Fork Recog: Visit https://github.com/rapid7/recog and click Fork,
   selecting your github account if prompted
2.  Clone ```git@github.com:<your-github-username>/recog.git```, replacing
```<your-github-username>``` with, you guessed it, your Github username.
3.  Add the master Recog repository as your upstream:
```
git remote add upstream git://github.com/rapid7/recog.git
git fetch --all
```

### Branch and Improve

If you have a contribution to make, first create a branch to contain your
work.  The name is yours to choose, however generally it should roughly
describe what you are doing.  In this example, and from here on out, the
branch will be FOO, but you should obviously change this

```
git fetch --all
git checkout master
git rebase upstream/master
git checkout -b FOO
```

Now, make your changes, committing as necessary, using useful commit messages:

```
vim CONTRIBUTING.md
git add CONTRIBUTING.md
git commit -m "Add a document on how to contribute to recog" -a
```

Please note that changes to [lib/recog/version.rb](https://github.com/rapid7/recog/blob/master/lib/recog/version.rb) in PRs are almost never necessary.

Now push your changes to your fork:

```
git push origin FOO
```

Finally, submit the PR.  Navigate to ```https://github.com/<your-github-username>/recog/compare/FOO```, fill in the details and submit.

## Landing PRs

(Note: this portion is a work-in-progress.  Please update it as things change)

Much like with the process of submitting PRs, Recog's process for landing PRs
is very similar to [Metasploit's process for landing
PRs](https://github.com/rapid7/metasploit-framework/wiki/Landing-Pull-Requests).
In short:

1. Follow the "Fork and Clone" steps from above
2. Fetch the latest revisions:

    ```
    git fetch --all
    ```
    
3. Checkout and branch the PR for testing.  Replace ```PR``` below with the actual PR # in question:

    ```
    git checkout -b landing-PR upstream/pr/PR
    ```
    
4. Test the PR, which typically involves running ```rspec```.
5. Merge with master, re-test, validate and push:

    ```
    git checkout -b upstream-master --track upstream/master
    git merge -S --no-ff --edit landing-PR
    git push upstream upstream-master:master --dry-run # confirm you are pushing what you expect
    git push upstream upstream-master:master
    ```

## Releasing New Versions

When Recog's critical parts are modified, for example its fingerprints or
underlying supporting code, a new version should eventually be released.  These
new releases can then be optionally included in projects such as Metasploit or
products such as Rapid7's in a controlled manner.

For now, in general any time Recog is modified you should release a version of
the Gem and the Github release, described below.  Eventually this process may
change.

### Release New Gem

1. Get an account on [Rubygems](https://rubygems.org)
2. Contact one of the Recog project contributors (listed [here under OWNERS](https://rubygems.org/gems/recog) and have them add you to the Recog gem.  They'll need to run:
  ```
  gem owner recog -a EMAIL
  ```
3. Edit [lib/recog/version.rb](https://github.com/rapid7/recog/blob/master/lib/recog/version.rb) and increment ```VERSION```.  Commit and push to rapid7/recog master.
4. Run ```rake release```

### Github Release

Some users may prefer to consume recog in a manner other than using git itself.  For that reason, Github offers [Releases](https://github.com/blog/1547-release-your-software).  Whenever a new version of the software is to be released, be kind and also create a new [Release](https://github.com/rapid7/recog/releases), using a versioning scheme identical to that used for the gem


