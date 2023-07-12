# Architecture 

## Overview 

![image](https://github.com/jmetzger/training-gitlab-ci-cd/assets/1933318/cbd998b1-cb5e-4978-889c-6213eaac2515)

## Components 

```
GitLab Workhorse
================
-> smart reverse proxy 
GitLab Workhorse is a smart reverse proxy for GitLab. It handles “large” HTTP requests such as file downloads, file uploads, Git push/pull and Git archive downloads.

GitLab Shell
============
GitLab Shell handles Git SSH sessions for GitLab and modifies the list of authorized keys. GitLab Shell is not a Unix shell nor a replacement for Bash or Zsh.
GitLab supports Git LFS authentication through SSH.
--> Alternative notwendig statt openssh 

When you access the GitLab server over SSH, GitLab Shell then:

1. Limits you to predefined Git commands (git push, git pull, git fetch).
2. Calls the GitLab Rails API to check if you are authorized, and what Gitaly server your repository is on.
3. Copies data back and forth between the SSH client and the Gitaly server.
 
Sidekiq (GitLab Rails -> gitlab rails console) 
======================

Simple, efficient background processing for Ruby.

Sidekiq uses threads to handle many jobs at the same time in the same process. It does not require Rails but will integrate tightly with Rails to make background processing dead simple.

Puma (Gitlab Rails -> gitlab rails console) 
===================
Puma is a fast, multi-threaded, and highly concurrent HTTP 1.1 server for Ruby applications. It runs the core Rails application that provides the user-facing features of GitLab.

Gitaly 
======
Dein Repo liegt auf einem bestimmten gitaly - Server 
Gitaly provides high-level RPC access to Git repositories. It is used by GitLab to read and write Git data.

Gitaly is present in every GitLab installation and coordinates Git repository storage and retrieval. Gitaly can be:

A background service operating on a single instance Linux package installation (all of GitLab on one machine).
Separated onto its own instance and configured in a full cluster configuration, depending on scaling and availability requirements.

```

