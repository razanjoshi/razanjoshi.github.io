---
layout: post
title: 'How I imported my git contributions'
date: '2019-09-02'
categories: Git
---
How I Restored My Git Contributions
Source: GoogleI was a software engineer for my previous company for 4 years. We were a Ruby on Rails-based platform where we had been working for throughout the years. So every commit you push to your GitHub repo, be it private or public creates a mark in your profile's contribution chart. The darker the shade, the higher the number of commits you pushed.
We know we may or may not have roasted each other looking at each other's contribution chart on our GitHub profile, making statements about who has coded more in the past months or years. As a software engineer's life cycle continues, he/she moves on from his/her current job to a new one, which means we change organizations throughout our journey. The different organization has their own private repositories(repos) and access controls, which means you can only access their repos through these private work (email) accounts associated with it. After you leave the company, it seems all your commits are scrapped off as they archive those stale email addresses of their ex-employees.
So here are few tips to help you import those contributions to your profile:
1. Add the work email address to the account
Add your work email as secondary emails in your GitHub profile's email settings.
2. Show private contributions
Thanks to GitHub, make sure you have chosen the private contributions option in order to show all the contributions you have made to a private repo on GitHub. This will only show the index on the chart and one can not trace the contributions made to a private repo.
3. Importing contributions from GitHub Enterprise, GitLab, BitBucket to GitHub.
This is a bit tricky as if you work in different version control from the GitHub. For this, we can use a Python script which will import all the commits you(and only you) have pushed to those accounts. Go through the given link below so you can have a better understanding.
miromannino/Contributions-Importer-For-Github
This tool helps users to import contributions to GitHub from private git repositories, or from public repositories that…github.com
Importing contributions to your accountHow it works:
Clone the repo.

git clone git@github.com:miromannino/Contributions-Importer-For-Github.git
Make sure you create a blank repo or use an existing blank repo which is authored by your profile in which you want to import your contributions. This will be your Mock Repo
Make sure those two repos are inside a common directory/folder. i.e. Mock repo & the repo given above.
Go to the cloned repo and create a file at the root directory

{% highlight ruby %}
run_script.py [name of the file]
----------------------------------------------------------
import git
from git_contributions_importer import *
# Your private repo or Bitbucket repo
repo = git.Repo("path/to/your/private/repo")
# Your mock repo
mock_repo = git.Repo("path/to/your/mock/repo")
importer = Importer([repo], mock_repo)
# I use both my personal email and work email here,
# Since the private repo uses work email, and Github profiles uses
# my work email
importer.set_author(['rajan.joshi@personalemail.com', 'rajan.joshi@workemail.co.uk'])
importer.import_repository()
{% endhighlight %}

Install gitpython and pathlib with pip3
{% highlight ruby %}
pip3 install gitpython
pip3 install pathlib
{% endhighlight %}
Run this script in terminal

python3 run_script.py
If you see some logs which say "Analysing commit", you're good to go.
Go to your Mock Repo in your terminal and push the changes. [If you don't do this, you will not see changes in your chart]

git push
Voilà and you're done!!!
The best part of using this is that it actually imports your actual work from those private repositories and not bluffing the GitHub itself. There are few tools to alter the GitHub's contribution chart like Rockstar and Vanity Text for GitHub but it's not your actual work, to be honest.
So, I hope this was helpful. Happy Coding !!!