# Walk Through Notes

## What is Bundler?

Bundler allows Ruby projects to use exact gems and versions.  If you are working on a few different Ruby projects, each depending on different versions of gems, then maintaining gem dependencies becomes error prone.  Bundler installs the gems with the right versions and forces your project to only use those versions.

## Bundler with a non-rails project

### start with a Gemfile

create a new directory and get in there, let's say:
```
> md my_simple_project
> cd my_simple_project
```
When starting a project from scratch, and want to use bundler for gem management: use `bundle init` to create a basic Gemfile.
```
> bundle init
```
Now with a `Gemfile` at hand, we can start adding gems that we need.  This is what the `Gemfile` looks like:
```ruby
source "https://rubygems.org"

gem 'prawn'
```
From then on, the most often used command is: `bundle install` whenever you modify any gems or versions of gems you need for the project.

Note, Bundler looks for a `Gemfile` in the current directory.  If such file is not available, Bundler gives an error `Could not locate Gemfile`.

## Bundler with a rails project

Within a Rails project directory, we can find both `Gemfile`, and `Gemfile.lock`.  So we know Rails uses Bundler to manage gem dependencies.

### How does Rails use Bundler?

But wait, `rails` is also a gem, does bundler manage rails' dependencies?  Yes.  A typical `Gemfile` in a Rails project looks like:
```ruby
source 'https://rubygems.org'
gem 'rails', '4.1.9'
gem 'sqlite3'
...
```
But this raises the question:
### Which one comes first when setting up a new project? Rails or Bundler?
If we haven't installed Rails or Bundler, then we can start by
```
> gem install rails
```
This will install the latest version of rails.  Then we can create a vanilla rails project.
```
> rails new my_project
...
run  bundle install
Fetching gem metadata from https://rubygems.org/..........
Fetching version metadata from https://rubygems.org/..
Resolving dependencies...
Using rake 10.4.2
...
Using uglifier 2.7.0
Bundle complete! 10 Gemfile dependencies, 42 gems now installed.
Use `bundle show [gemname]` to see where a bundled gem is installed.
         run  bundle exec spring binstub --all
```
As the new project is being created, the output shows bundle is in fact run for resolving dependencies.
Within this new project directory, a new `Gemfile` is present.
Rails by default uses Bundler, but it is also possible to do without.  The rails command line manuals shows this
```
> rails new -h
...
-m, [--template=TEMPLATE]                              # Path to some application template (can be a filesystem path or URL)
    [--skip-gemfile], [--no-skip-gemfile]              # Don't create a Gemfile
-B, [--skip-bundle], [--no-skip-bundle]                # Don't run bundle install
...
```
### How come requiring gems is not needed when you use Rails with Bundler?

See [How does Rails use Bundler?](http://www.justinweiss.com/blog/2014/10/13/how-does-rails-handle-gems/) (about halfway down the article).  The short answer is: Rails has some machinary to take care of it so you don't have to.

### Where are the installed gems?

Use `bundle list` to show all gems in the current bundle.
Then we can use `bundle show <gem>` to show the source location of a particular gem in the bundle.
For example:
```
> bundle show prawn
/home/eric/.rbenv/versions/2.1.5/lib/ruby/gems/2.1.0/gems/prawn-1.3.0
```
Seeing this raises another area to explore.  Notice the above path shows the version of ruby I use.  Also it gives hint that I use rbenv to manage ruby version. As time goes on, it is likely on a developer's machine, one would want to have different versions of working ruby (say 2.1.5, and 1.9.x) for new and older projects.  This functionality is outside of bundler primarily.

## Related: managing multiple versions of ruby

There are several solutions to install and use multiple versions of ruby:
   * chruby + ruby-install
   * rbenv + ruby-build
   * rvm

See [solutions in detail](http://kgrz.io/2014/02/13/Programmers-guide-to-choosing-ruby-version-manager.html)
