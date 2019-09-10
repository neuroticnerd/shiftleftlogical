
Git
===============

There are a number of options for version control, even a good number that are
free to use or open source. My choice is always |link_git|, but to each their
own. The learning curve may be slightly steeper, but it serves its purpose
well.


Learning Git
--------------------

|link_git| is a distributed version control system and though it can take a
bit of getting used to, it is extremely powerful for any size project;
|link_git| is a commandline tool by itself, but there are third party
GUI clients for it, and hosting providers for repositories.

*   The |link_progit| free book if you want a deep dive
*   Some good quality Atlassian |link_git_atlassian|
*   A StackOverflow compendium of |link_git_begin|
*   A |link_git_tut| that takes a deeper look at how Git works
*   A list of some additional |link_git_tuts|


Git Hosting
--------------------

|link_github|
    GitHub is a web-based front-end and hosting platform for
    Git repositories, and while a free account will not let you create private
    repositories, its still an amazing tool to know how to use, and I would
    even go so far as saying its worth a paid account once you start doing
    more serious programming projects (plus its a good cheap way to host all
    your code in the cloud so you can always access it).

|link_gitlab|
    This is an alternative hosting to the ever-popular GitHub, with the option
    to download the source-code for free and self-host your git repositories;
    I’ve not spent too much time with it yet, and still prefer GitHub for the
    time-being, but it has a lot going for it and continues to grow.

|link_bitbucket|
    With the exception of SourceTree, I am not a big fan of Atlassian products.
    However, having used the Atlassian stack professionally for some years now,
    I can say that Bitbucket offers much the same features as other Git hosting
    and usually integrates well with the rest of the Atlassian products
    (though Jenkins and Slack hooks can be temperamental). Access
    control settings can be clunky, but arguably that could be said of the
    Atlassian stack in general.


GUI Clients
---------------------

While I would always encourage someone to learn how to execute at least the
basics in Git from the command line, I find that GUI clients can both speed
up routine operations, as well as offer useful information at a glance.



|link_sourcetree|
    Possibly the best git GUI for Mac and Windows; they do
    want you to ‘register’ your copy but its free to do so (just give them a
    spam email address or something). Unfortunately there is no Linux version
    of this software, nor do they currently have any plans to make one.

|link_gitkraken|
    The newcomer, this one has been gaining quite a bit of popularity, and
    for good reason. While the software itself has seemed solid so far, there
    are limitations with the free version (though it does support Linux).

|link_smartgit|
    I have not personally tested it yet, but have heard some
    very promising anecdotes and like GitKraken does have support for Linux.
    It was previously free for non-commercial use, but may now be paid-only.

|link_gitextensions|
    If you happen to be struck with the misfortune of using Windows for
    development, or you want integration with Windows Explorer or
    Visual Studio, then you should consider looking into this one.

|link_gitgui_nix|
    Here is one of the available lists of GUIs for Git;
    while most things I write are designed to run on Unix machines, I usually
    develop on Mac or Windows (when under duress)


Best Practices
----------------------

`Git Workflow <https://nvie.com/posts/a-successful-git-branching-model/>`_
    I would argue that the this article is one of the most articulate and
    well-formed explanations of a useful git workflow that I have found to
    date, and I would highly recommend reading through it.

    Not every project will need the complexity of having hotfix, release, and
    stage branches, but the approach described in the article can be easily
    trimmed down or adapted for almost any scale or type of project.

`Commit Messages <http://chris.beams.io/posts/git-commit/>`_
    Consistent formatting is important for commit messages. It helps to keep
    the history clean, and have a consistent log of changes to the source code.
    This article provides some fantastic guidelines for commit messages to
    keep your git history tidy and consistent.

`Contributing to a Project <https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project>`_
    From a workflow standpoint, incorporating your changes when working on a
    team is generally done via Pull Requests. PR's are supported in the UI of
    all major git hosting providers, but are based on the
    `git request-pull <https://git-scm.com/docs/git-request-pull>`_
    mechanism.



.. |link_git| raw:: html

    <a href="https://git-scm.com/" rel="external noopener noreferrer">Git</a>

.. |link_git_tuts| raw:: html

    <a href="https://sixrevisions.com/resources/git-tutorials-beginners/" rel="external noopener noreferrer">Git guides</a>

.. |link_git_begin| raw:: html

    <a href="https://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide" rel="external noopener noreferrer">Git for beginners</a>

.. |link_git_atlassian| raw:: html

    <a href="https://www.atlassian.com/git/tutorials" rel="external noopener noreferrer">Git Tutorials</a>

.. |link_git_tut| raw:: html

    <a href="http://www.vogella.com/tutorials/Git/article.html" rel="external noopener noreferrer">Git tutorial</a>

.. |link_github| raw:: html

    <a href="https://github.com/" rel="external noopener noreferrer">GitHub</a>

.. |link_gitextensions| raw:: html

    <a href="https://gitextensions.github.io/" rel="external noopener noreferrer">GitExtensions</a>

.. |link_sourcetree| raw:: html

    <a href="https://www.atlassian.com/software/sourcetree/overview" rel="external noopener noreferrer">SourceTree</a>

.. |link_gitgui_nix| raw:: html

    <a href="https://git.wiki.kernel.org/index.php/InterfacesFrontendsAndTools#Graphical_Interfaces" rel="external noopener noreferrer">Linux Git GUIs</a>

.. |link_smartgit| raw:: html

    <a href="https://www.syntevo.com/smartgit/" rel="external noopener noreferrer">SmartGit</a>

.. |link_gitlab| raw:: html

    <a href="https://about.gitlab.com/" rel="external noopener noreferrer">GitLab</a>

.. |link_gitkraken| raw:: html

    <a href="https://www.gitkraken.com/" rel="external noopener noreferrer">GitKraken</a>

.. |link_bitbucket| raw:: html

    <a href="https://bitbucket.org/product/features" rel="external noopener noreferrer">Bitbucket</a>

.. |link_progit| raw:: html

    <a href="https://git-scm.com/book/en/v2" rel="external noopener noreferrer">Pro Git</a>
