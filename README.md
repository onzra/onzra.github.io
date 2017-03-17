# ONZRA Website

## Setup

Before you install dependencies, make sure [ruby is up to date](#Ruby).

    sudo gem install jekyll bundler
    bundle install

## Blogging

### Writing a Post

Create a new markdown file in `_posts` in the format `YYYY-MM-DD-post-title.md`. For example, "2017-03-16-blog-coming-soon.md`. Then add some YAML metadata at the top like:

    ---
    layout: post
    title:  "Coming Soon"
    date:   2017-03-16 16:14:06 -0700
    ---

The rest of the file is your blog post, written in markdown.

- Templating and syntax highlighting: https://jekyllrb.com/docs/templates/
- Posts with a `date:` value in the future will not show up until the site is rebuilt after that date.

### Preview

To preview your posts before publishing them to the website:

    bundle exec jekyll serve
    http://127.0.0.1:4000/

Jekyll will automatically detect changes to files and re-build. You can refresh to see changes to your blog post.

## Publishing

Simply pushing changes to master will trigger a new build of the production website, effectively "publishing" your new posts to https://onzra.github.io/.

## Ruby

You'll want the latest version of ruby, the easiest way to get that is to use rvm:

    curl -L https://get.rvm.io | bash -s stable --auto-dotfiles --autolibs=enable --ruby

Now if you open a new shell you should have `rvm` available and an updated `ruby --version`.

You should also update gem:

    gem install rubygems-update
    update_rubygems
    gem update --system

## TODO

- Different theme.
 - Trying minimal-mistakes-jekyll, but need to fix some gem build problems first (let's use rvm to install latest version of ruby)
- Test out the setup and publishing on a fresh machine to make sure we didn't miss any steps.
- Add some instructions on handling images.
- Write some initial blog posts to start things off.
- Fill out some basic content pages like about, team, location, etc. Look at what we have on the current site.
- Move to install gems in local .vendor folder instead of globally.
