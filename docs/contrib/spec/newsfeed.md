# Newsfeed

!!! info
This page is a _design specification_ for a feature that was implemented and
tested before release.

The [MP website](//materialsproject.org) exposes a lot of data and tools.
Sometimes, people are surprised to learn about data and tools that have been
available on the site for months, especially if they have logged in and used the
site recently. One way to keep returning users informed, seen on many websites,
is a news feed. Such a feed consists of short entries, each with a date and
summary of the news.

Often, there is a subtle and unobtrusive visual cue for
returning users to review recent news before continuing to use the site. In
other cases, the recent news is presented in focus for the user to review and
dismiss. Apart from viewing a feed while visiting its website, the feed may
also be formatted as per e.g. the
[RSS](https://validator.w3.org/feed/docs/rss2.html) or
[Atom](https://validator.w3.org/feed/docs/atom.html) specifications to allow
users to aggregate such news feeds from many websites of interest.

## Data entry

To enter news feed items, one creates a Markdown file in the `newsfeed/data`
directory with a name of the format `YYYY-MM-DD-entry-title.md`, where
`YYYY-MM-DD` is a [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted
date. The file itself will look something like

```markdown
---
title: My feed item title
---

This is a great piece of news.
More info [here](https://materialsproject.org/newstuff).
```

This format is based on that used by the [Jekyll](https://jekyllrb.com/) static
site framework -- a simple organization of news items into separate files. The
first section of the file (delimited by `---` lines) is meta-data, aka "front
matter", and will be pre-processed for relevant key-value pairs. The remainder
of the file will be converted to HTML. This may be implemented in one pass, for
example using the Python `markdown` package with it's built-in `"meta-data"`
extension.

The `title` is the only required piece of metadata. If the feed entry requires a
significant change, then an `updated` metadata field and value (in `YYYY-MM-DD`
format) should be added -- do not change the filename. If a change to the entry
is insignificant, like fixing a typo, then you don't need to create or update an
`updated` field.

## Data display

The news feed is displayed in two places: on the static (not-signed-in) home
page, and on the signed-in default app view. Both views are in centered,
responsive two-column layouts near the top of their respective pages. For a
signed-in user, there is up to three months of unseen news. For the static home
page, the news fills the two columns -- this depends on the summary-lengths of
the news items, but does not exceed ten items (five per column). Finally, the
signed-in user view is dismissible with a click.

Each feed item on display shows a date, a title, and a summary. The date is
gathered from the item's filename or from its `updated` metadata field if
given. The summary is the rendered HTML of the item file's Markdown body. Feed
items are presented in reverse chronological order.

## Data management

The last time a user has seen the news feed is stored in the `app_db`'s
`newsfeed_views` collection, one document per user. The query

```python
return_document = app_db.newsfeed_views.find_one_and_update(
    {"user": request.user.username},
    {"$set": {"last_seen": datetime.utcnow()},
    upsert=True)
```

will update a user's document (inserting a document if one doesn't exist) with
the current time as the last-seen time, and return the old user document (or
`None` if no document existed). The application can then determine which
feed items to render to the user based on the last `"last_seen"` value. This
example uses the Django `request` object to get a user's immutable `username`.
The expression `request.user.is_authenticated` may be evaluated first in this
case to determine which view is to be rendered.
