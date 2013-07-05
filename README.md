Getting Git
===========

These are the slides for a talk I gave on Git to my coworkers at Six3 Systems.

## Acknowledgements

My talk is based on Scott Chacon's [talk with the same title](http://vimeo.com/14629850), which remains the
best talk on Git I have ever seen. About half of my slides from from various
[talks by Chacon](https://github.com/schacon/git-presentations), and I owe him
tremendously for all of his work.

Thanks also go to Six3 Systems for giving me time to prepare the presentation
and for allowing me to post it publicly.

## Further Useful Information

### When you've committed something you shouldn't have.
The most common problem I've seen after I gave the presentation was the accidental committing of large files.
Here are some things you can do about that.

#### Drop everything and make a good global .gitignore file now.
You can set a global .gitignore file that applies to all your repositories by editing .gitconfig in your home directory, adding the excludesfile line as follows. 
```
...
[core]
        excludesfile = /Users/daniel.cox/.gitignore
```

Then make that ~/.gitignore file, and put everything in there you're terrified you'll commit one day by accident. (Note that this file is just a backup. You should still make an appropriate .gitignore file in each of your repositories so that people without such a good global .gitignore file won't cause trouble.)

Here's what's in mine:

```
.DS_Store
*.svn
*~
.*.swp
.powenv
.classpath
.project
.settings
target
*.class
pom.properties
*.gem
vendor/bundle
vendor/cache
```

#### Always start a new repo by creating a .gitignore file in its root
Add things you don't want in the repo, such as passwords, log files, large files, IDE config files, etc.
Don't just rely on your global .gitignore file, because other people working with you might not have one, and you wouldn't want them to commit bad files either.
GitHub has [a repository full of good default .gitignore files for various types of projects](https://github.com/github/gitignore).

#### How to find big files in your history
I've attached a simple Ruby script called "big_files" that searches back from a starting point looking for files over some megabyte count you specify. Make it executable and put it somewhere in your path.

Credit goes to [mislav](http://stackoverflow.com/users/11687/mislav).

```
Usage:
    big_files [rev] [size in MB]
    $ big_files master 0.3
    3.8M  example/blah.psd  (aad2981: 4 months ago)
    1.1M  another/big.file  (6e73ca2: 2 weeks ago)
```

#### How to purge big files from your history
GitHub has [an excellent page on how to purge sensitive (or big) files from your history](https://help.github.com/articles/remove-sensitive-data) once you've found them. Please read the whole page and heed their warnings about rewriting commits that you've already pushed to the remote repo.
