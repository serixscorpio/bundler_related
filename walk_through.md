# Walk Through Notes

## What is Bundler?

Bundler allows Ruby projects to use exact gems and versions.  If you are working on a few different Ruby projects, each depending on different versions of gems, then maintaining gem dependencies becomes error prone.  Bundler installs the gems with the right versions and forces your project to only use those versions.

## Bundler with a non-rails project

### start with a Gemfile

When starting a project from scratch, and want to use bundler for gem management: use `bundle init` to create a basic Gemfile.

The most often used command is: `bundle install`. Bundler looks for a `Gemfile` in the current directory.  If such file is not available, Bundler gives an error `Could not locate Gemfile`.

## Bundler with a rails project

Within a Rails project directory, we can find both `Gemfile`, and `Gemfile.lock`.  So we know Rails uses Bundler to manage gem dependencies.

### How does Rails use Bundler?

But wait, `rails` is also a gem, does bundle manage rails' own dependencies?

### How come requiring gems is not needed when you use Rails with Bundler?

Is it better practice to install the `rails` gem first or the `bundler` gem?

### Where are the installed gems?

Use `bundle list` to show all gems in the current bundle.
Then we can use `bundle show <gem>` to show the source location of a particular gem in the bundle.
For example: `/home/eric/.rbenv/versions/2.1.5/lib/ruby/gems/2.1.0/gems/prawn-1.3.0`

Seeing this raises another area to explore.  Does bundler also manage which version of ruby to use in addition to resolving gem dependencies?

?? search `bundler check ruby version`, answer is probably no.

## Related: managing multiple versions of ruby

There are several solutions to install and use multiple versions of ruby:
   * chruby + ruby-install
   * rbenv + ruby-build
   * rvm

See [solutions in detail](http://kgrz.io/2014/02/13/Programmers-guide-to-choosing-ruby-version-manager.html)
