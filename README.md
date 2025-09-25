# vitorlinhalis.github.io
my portfolio 2025

## Jekyll Local Development (macOS)

### Prerequisites
- rbenv for Ruby version management
- Ruby (version 2.7 or higher)

### Setup
1. Install rbenv (if not already installed):
   ```bash
   brew install rbenv ruby-build
   ```

2. Add rbenv to your shell profile:
   ```bash
   echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
   echo 'eval "$(rbenv init -)"' >> ~/.zshrc
   source ~/.zshrc
   ```

3. Install and set Ruby version:
   ```bash
   rbenv install 3.1.0
   rbenv local 3.1.0
   ```

4. Install Bundler:
   ```bash
   gem install bundler
   ```

5. Install Jekyll dependencies:
   ```bash
   bundle install
   ```

### Running the Server
Start the local Jekyll server:
```bash
bundle exec jekyll serve
```

The site will be available at: http://localhost:4000

#### Development Options
- **Live reload**: `bundle exec jekyll serve --livereload`
- **Draft posts**: `bundle exec jekyll serve --drafts`
- **Incremental builds**: `bundle exec jekyll serve --incremental`
- **Custom port**: `bundle exec jekyll serve --port 4001`

### Common Issues
- **Ruby version mismatch**: Run `rbenv versions` to check available versions
- **Port already in use**: Use `--port` flag with different port number
- **Gem conflicts**: Run `bundle update` to update dependencies
- **rbenv not found**: Restart terminal or source your shell profile

### Troubleshooting Jekyll Installation Issues

If you encounter native extension compilation errors (eventmachine, http_parser.rb):

1. **Ensure Xcode Command Line Tools are installed**:
   ```bash
   xcode-select --install
   ```

2. **Verify you're using rbenv Ruby (not system Ruby)**:
   ```bash
   ruby --version  # Should show 3.1.0, not 2.6.x
   ```
   If still showing system Ruby, initialize rbenv:
   ```bash
   eval "$(rbenv init -)"
   ```

3. **Update Gemfile to remove problematic dependencies**:
   - Remove `jekyll-admin` (requires native extensions)
   - Uncomment `gem "jekyll", "~> 4.0"` and `gem "jekyll-remote-theme"`

4. **Install gems locally**:
   ```bash
   bundle config set --local path 'vendor/bundle'
   bundle install
   ```

5. **If compilation still fails, install Jekyll globally**:
   ```bash
   gem install jekyll
   jekyll serve
   ```

6. **For permission errors with system Ruby**:
   - Use rbenv to install a newer Ruby version (3.1.0+)
   - Update RubyGems: `gem update --system 3.2.3`

7. **Alternative: Use Docker**:
   ```bash
   docker run --rm -it -p 4000:4000 -v "$PWD":/srv/jekyll jekyll/jekyll jekyll serve --host 0.0.0.0
   ```

### Production Build
To build the site for production:
```bash
bundle exec jekyll build
```

Output will be in the `_site/` directory.
