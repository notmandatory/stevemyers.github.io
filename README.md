**Jekyll installation**

  1. Install Ruby with Ruby Gems, it is already pre-installed on Mac OSX
 
  ```
  $ gem update --system          # may need to be administrator or root
  $ gem install rubygems-update  # again, might need to be admin/root
  $ update_rubygems              # ... here too
  ```
 
  2. Install jekyll gem
 
  ```
  $ gem install jekyll
  ```

**Simple build and test instructions**

  1. Build and run in local server
 
  ```
  $ jekyll serve
  # => A development server will run at http://localhost:4000/
  # Auto-regeneration: enabled. Use `--no-watch` to disable.
  ```
 
 See [jekyll](http://jekyllrb.com/docs/usage/) site for more usage instructions.