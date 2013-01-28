[Permalink](http://susy.oddbird.net/guides/ "Permalink to Susy: Getting Started")

# Susy: 入門

## <a href="#start-install" id="start-install">安裝</a>

安裝有以下五種方法：

- 使用命令列安裝到 Compass 環境或現有專案
- 安裝到 Rails 專案
- 安裝到 Yeoman 專案
- 安裝 fire.app（設計師請看此方法）
- 手動安裝

### <a href="#start-compass" id="start-compass">使用命令列安裝到 Compass 環境</a>

從命令列安裝：

    :::bash
    # 命令列
    gem install susy

建立一個新的 [Compass][compass] 專案：

    :::bash
    # 命令列
    compass create <project name> -r susy -u susy

或安裝到現有的 [Compass][compass] 專案：

    :::ruby
    # config.rb
    require "susy"

[compass]: http://compass-style.org/

### <a href="#start-rails" id="start-rails">安裝到 Rails 3.x 專案</a>

    :::ruby
    # Gemfile
    gem "susy"

你可能還需要：

    :::ruby
    # Gemfile
    gem 'compass', '>= 0.12.2'
    gem 'compass-rails', '>= 1.0.3'


之後執行：

    :::bash
    # 命令列
    bundle install

### <a href="#start-yeoman" id="start-yeoman">安裝到 Yeoman 專案</a>

編輯你專案的根目錄裡的 **Gruntfile.js** 檔案，找到有關 compass 的規則那邊，照下面這個指示加入 option 的部份：

    :::javascript
    // Gruntfile.js
    compass: {
      dist: {
        options: {
          config: '.config.rb'
        }
      }
    }

然後在 **Gruntfile.js** 檔案同一個目錄下，建立一個檔案叫 **.config.rb** 並填入以下內容：

    :::ruby
    # .config.rb
    require "susy"

就可以開始用了！

### <a href="#start-fireapp" id="start-fireapp">安裝 fire.app</a> （設計師請看此方法）

- 前往 <http://fireapp.handlino.com> 購買 fire.app
- 用 fire.app 開啟一個 susy 專案 Create Project > susy > project

就可以開始用了！

### <a href="#start-manual" id="start-manual">手動安裝</a>

如果說你不想使用命令列安裝到 Compass 或 Rails 專案，就用這方法吧。
CodeKit 的愛用者也可以用這個方式安裝。

* 只要從 github <a href="https://github.com/ericam/susy/archive/master.zip">下載</a> 這個 zip 檔
* 拷貝 sass 資料夾裡面的所有東西，剩下的其他檔案你可以隨意刪除
* 貼到你專案裡面的 sass 資料夾（或是你自己改過名字，那個放 sass 的資料夾就對了）
* 最後 import Susy! ( 參考 <a href="#start-usage">使用方法</a> )

就可以開始用了！

## <a href="#start-usage" id="start-usage">使用方法</a>

    :::scss
    @import "susy";

### <a href="#start-settings" id="start-settings">設定</a>

Set up your default grid values: total columns, column width, and gutter width.

    :::scss
    $total-columns  : 12;             // a 12-column grid
    $column-width   : 4em;            // each column is 4em wide
    $gutter-width   : 1em;            // 1em gutters between columns
    $grid-padding   : $gutter-width;  // grid-padding equal to gutters

### <a href="#start-basic" id="start-basic">Basic Grids</a>

The basic Susy grid is composed using two simple mixins:

- Use the [container()][container] mixin to create your initial grid context.
- Use the [span-columns()][span-columns] mixin to declare
  the width of an element on the grid.

Here's a simple page layout:

    :::scss
    .page {
      // page acts as a container for our grid.
      @include container;

      // header and footer are full-width by default.
      header, footer { clear: both; }

      // nav spans 3 columns of total 12.
      nav { @include span-columns(3,12); }

      .content {
        // content spans the final (omega) 9 columns of 12.
        @include span-columns(9 omega,12);

        // main content spans 6 of those 9 columns.
        .main { @include span-columns(6,9); }

        // secondary content spans the final 3 (omega) of 9 columns.
        .secondary { @include span-columns(3 omega,9); }
      }
    }

### <a href="#start-responsive" id="start-responsive">Responsive Grids</a>
Responsive Susy grids allow you to change the number of columns in a layout
at different window sizes, using @media-queries with min and max widths.
This requires one more mixin:

- Use [at-breakpoint()][at-breakpoint] to set different layouts
  at min- and max-width breakpoints.

Here's a mobile-first example:

    :::scss
    $total-columns: 4;

    .page {
      // Establish our default 4-column grid container.
      @include container;

      // Create a media-query breakpoint at a min-width of 30em
      // And use a larger 8-column grid within that media-query.
      @include at-breakpoint(30em 8) {
        // Establish our new 8-column container.
        @include container;
      }
    }

### <a href="#start-advanced" id="start-advanced">Advanced</a>
Susy is built to handle your unique markup, and any number of edge cases.
It includes the standard [push()][push] and [pull()][pull] mixins,
along with other useful functions and shortcuts,
support for various grid styles,
and even bi-directional grids for multi-lingual sites.
Check the [reference documentation][reference] for details.

[reference]: ../reference/
[container]: ../reference/#ref-container
[span-columns]: ../reference/#ref-span-columns
[at-breakpoint]: ../reference/#ref-at-breakpoint
[push]: ../reference/#ref-push
[pull]: ../reference/#ref-pull

## <a href="#troubleshooting" id="troubleshooting">Troubleshooting</a>

### <a href="#troubleshooting-versions" id="troubleshooting-versions">Version Management</a>

When you are working with bundled gems and dependencies
across a number of different projects,
managing gem versions can become an issue.

If you are working in a **Ruby** environment,
we recommend using [RVM](http://rvm.io/rvm/install/).
See our [Rails troubleshooting](#troubleshooting-rails-install)
below for some basic instructions, or
[dig into RVM's installation instructions](http://rvm.io/rvm/install/).

In a **Python** environment,
we recommend [virtualenv](http://www.virtualenv.org/en/latest/index.html)
in conjunction with these
["postactivate" and "predeactivate" scripts](https://gist.github.com/1078601)
to add support for Ruby gems.

Once you have that in place,
[Bundler](http://gembundler.com/)
can be used in either environment
to manage the actual installation
and updating of the gems.

### <a href="#troubleshooting-compass-install" id="troubleshooting-compass-install">Compass Install</a>

The old gem and the new gem have different names,
but are required simply as ``susy``.
That can cause a conflict if both gems are present.

If you have installed Susy in the past,
make sure you've uninstalled older versions:

    :::bash
    # 命令列
    gem uninstall compass-susy-plugin
    # "compass-susy-plugin" was the gem name for 0.9.x and lower
    # Susy 1.0 switches to "susy" as the gem name

And then install 1.0:

    :::bash
    # 命令列
    gem install susy

Then use Compass as normal.

### <a href="#troubleshooting-rails-install" id="troubleshooting-rails-install">Rails 3.x Install</a>

We recommend you use [RVM](http://rvm.io)
for using Susy with Rails projects.
It has become the standard gem management system for Rails,
it's very easy to install and use,
and it helps create and manage Gemsets
among different developers working on different branches.

[Here are some RVM best practices](http://rvm.io/rvm/best-practices/):

If you have installed Susy in the past,
make sure you've uninstalled older versions.
See [Compass Install](#troubleshooting-compass-install) above.

[Install RVM](http://rvm.io/rvm/install/)
(These are basics,
if you do not have Ruby and Rails already installed in your environment,
we [recommend you use RVM's installation instructions](http://rvm.io/rvm/install/)):

    :::bash
    # 命令列
    # from your system's root:
    curl -L get.rvm.io | bash -s stable

Create a gemset for your site:

    :::bash
    # 命令列
    rvm gemset create fooBar

Create an ``.rvmrc`` file at your site's root:

    :::bash
    # .rvmrc
    rvm use 1.9.3@fooBar
    # Use whatever Ruby version number your app uses

Now whenever you ``cd`` into your site's root,
RVM will pick up and use that Gemset.

``cd`` to your site and install [Bundler](http://gembundler.com/):

    :::bash
    # 命令列
    gem install bundler

Add Susy to your ``Gemfile``
([more info on Gemfiles](http://gembundler.com/gemfile.html)):

    :::ruby
    gem "susy", "~> 1.0.5"

And finally run your bundle:

    :::bash
    # 命令列
    bundle
