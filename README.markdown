InSTEDD Platform Common Rails
=============================

This gem makes it easy to apply the look and feel found in InSTEDD applications.

Installation
------------

    gem install instedd-rails

Gemfile
-------

    gem 'instedd-rails'

Layout
------

Your application layout in app/views/layouts/application.html.erb should
look something like this:

    <% content_for :navigation do %>
      <%= section "Home", root_path, :home %>
      <%= section "Tour", tour_path, :tour %>
      <%= section "Community", community_path, :community %>
      <%= section "Help", help_path, :help %>
    <% end %>
    <% content_for :right_menu do %>
      <ul class="RightMenu">
        <%- if user_signed_in? %>
          <li>
          <div id="User">
            <%=current_user.email%><br><br>
            <div class="container">
              <ul>
                <li><%= link_to 'Settings', edit_user_registration_path %></li>
              </ul>
              <hr/>
              <ul>
                <li><a href="mailto:support@instedd.org?subject=[<%= application_name.underscore %>-bug]">Report a bug</a></li>
                <li><%= link_to "Sign Out", destroy_user_session_path, :method => :delete %></li>
              </ul>
            </div>
          </div>
          </li>
          <li>
            <%= link_to '', edit_user_registration_path, :class => 'fsettings' %>
          </li>
          <% else %>
          <li>
            <%= link_to "Create account", new_user_registration_path, :class => 'fedit' %>
          </li>
          <li>
            <%= link_to "Log in", new_user_session_path, :class => 'fuser' %>
          </li>
        <% end %>
      </ul>
    <% end %>
    <% content_for :footer_links do %>
      <a href="<%= root_path %>">Home</a>
    <% end %>
    <%= render :file => 'layouts/instedd_application' %>

Breadcrumbs
-----------

To specify the breadcrumbs, in your controller:

    class YourController < ApplicationController
      def index
        @show_breadcrumb = true
        add_breadcrumb 'Home', home_path
      end
    end

Read more about the [breadcrumbs\_on\_rails gem](https://github.com/weppos/breadcrumbs_on_rails).

Tabs
----

To render tabs in the view:

    <ul class="tabs top">
      <%= tab "Overview", overview_path %>
      <%= tab "Settings", settings_path %>
    </ul>

Using a different URL for the theme
-----------------------------------

You can use the INSTEDD\_THEME environment variable to use a different
url for the theme. For example:

    INSTEDD_THEME=http://localhost rails s

If you have the [platform-common](https://bitbucket.org/instedd/platform-common) project checkout out locally you
can serve it with this command line:

    sudo python -m SimpleHTTPServer 80

(be sure to run `rake` in that project before serving it)

How to develop
--------------

To make a change to the project without having to commit to check the results,
you must tell your application to get the gem from your local hard drive.
This can be done modifying your app's `Gemfile` to point to where you have this gem:

	gem 'instedd-rails', :path => /path/to/this/gem

and then running `bundle install`.
