===================
NewsBlog extension
===================

Extends tx_news with blog-like features.


Features
========

Backend users as article authors
--------------------------------
The *author* and *author_email* fields are hidden, but a new field for selecting a backend user as author for the article is displayed instead. The old fields are still accessible through e.g. ``{news.author}`` though. To access the backend user record, utilize ``{news.authorRecord}``.

Profile page for backend users
------------------------------
Backend users now contain a *profilePid* field which allows linking to a static page for displaying the author's profile. The page id to link to it is accessible through e.g. ``{news.authorRecord.profilePid}``.

Abstract for backend users
--------------------------
This extension allows to add a short abstract about the author to each backend user record which is accessible through e.g. ``{news.authorRecord.abstract}``.

Automatic assignmend of current backend user
--------------------------------------------
If you create or edit a record, the backend user you're currently logged in as will be assigned to the news record as author automatically.

Filter articles by author
-------------------------
Although only available through TypoScript, you can utilize ``plugin.tx_news.settings.authors`` to filter records by author(s). It takes a comma-separated list of backend user id's to filter records.

RTE transformation service to support code formatting
-----------------------------------------------------
As the default RTE transformations drop almost anything required to properly display multi-lined code with proper indentation, it adapts the news' *bodytext* field (where you type your content into) and applies the following transformations **to content wrapped inside pre-tags only**:

- Before storing content into the database:

  - Consecutive space characters are converted to non-breaking spaces (``&nbsp;``). This allows proper indentation, as they would be dropped otherwise.
  - Newlines are converted to ``<br />`` in order to keep line breaks where intended.

- Before displaying content inside the RTE:

  - ``<br />`` tags are converted back to newlines for easier editing in RTE.