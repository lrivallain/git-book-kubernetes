---
title: Introduction
---

# My Kubernetes book

The following book is a personal note-book to keep some relevant informations
about Kubernetes and k8s related products, for my personal and/or professional
use.


{{% notice info %}}
This is not a substitution to official projects documentation,
just a quick way for me to get the information I need.
{{% /notice %}}



{{%expand "How to contribute ?" %}}

This website is built on [Hugo](https://gohugo.io/) static website engine with the
[learn theme](https://learn.netlify.app/en/).

You can contribute by suggesting [issues](https://github.com/lrivallain/git-book-kubernetes/issues/new/choose) or 
[pull-requests](https://github.com/lrivallain/git-book-kubernetes/pulls) on the <i class='fab fa-fw fa-github'></i> 
GitHub project.

1. As a pre-requesite to local build, you will need Hugo engine installed: [Quick Start](https://gohugo.io/getting-started/quick-start/)
2. Clone the repository with submodules:

```bash
git clone --recursive https://github.com/lrivallain/git-book-kubernetes.git
```

3. Push changes to a new branch:

```bash
# new branch:
git checkout -b "my-changes"
# <do changes here !>
# test your changes with:
hugo server
# <git add / git commit / git push>
```

4. Create a pull request on the project.
5. Once accepted and merged to master, the static will be run through this
[Publish GitHub Action](https://github.com/lrivallain/git-book-kubernetes/actions?query=workflow%3A%22Publish+Site%22)


{{% /expand%}}