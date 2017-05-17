# Docker image for build and upload Jekyll websites

## Usage

Run Jekyll in live update mode

    docker run -v `pwd`:/srv/jekyll -p 4000:4000 summerisgone/jekyll_s3_website jekyll build && open http://localhost:4000


Generate website

    docker run -v `pwd`:/srv/jekyll summerisgone/jekyll_s3_website jekyll build

Upload to existing bucket

    docker run -v `pwd`:/srv/jekyll summerisgone/jekyll_s3_website aws s3 sync /srv/jekyll/_site/ s3://example.com