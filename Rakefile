task default: 'test'

# cf. GitHub - gjtorikian/html-proofer
# https://github.com/gjtorikian/html-proofer
require 'html-proofer'
task test: [:build] do
  options = {
    checks: ['Links', 'Images', 'Scripts', 'OpenGraph', 'Favicon'],
    allow_hash_href:  true,
    disable_external: ENV['TEST_EXTERNAL_LINKS'] != 'true',
    enforce_https:    true,

    # NOTE: Ignore file, URL, and response as follows
    ignore_files: [
      /google(.*)\.html/,
    ],
    ignore_urls: [
      # URL should be perfect-matching
      # e.g. 'http://example.com/foobar',

      # Use REGEX to ignore URLs by domains
      %r{^http://www.coderdojo-urasoe.com},
    ],
    #ignore_status_codes: [0, 500, 999],
  }

  HTMLProofer.check_directory('_site', options).run
end

# Enable 'build' to flush cache files via 'clean'
task build: [:clean] do
  system 'JEKYLL_ENV=test bundle exec jekyll build' unless ENV['SKIP_BUILD'] == 'true'
end

task :clean do
  system 'bundle exec jekyll clean' unless ENV['SKIP_BUILD'] == 'true'
end
