# Docker image for build and upload Jekyll websites

I needed a tool to build Jekyll website from repo and publish it to S3.
So I ended with Butbucket Pipelines with the following configuration in `bitbucket-pipelines.yml`:

```yaml
 image: summerisgone/jekyll_s3_website
 
 pipelines:
   default:
     - step:
         script:
           - jekyll build -s `pwd` -d `pwd`/_site
           - aws s3 sync --delete `pwd`/_site s3://chellysoftware.com
```

Here ``pwd`` is important because jekyll/jekyll image sets its own WORKDIR.

## Usage

Run Jekyll in live update mode

    docker run -v `pwd`:/srv/jekyll -p 4000:4000 summerisgone/jekyll_s3_website jekyll build && open http://localhost:4000


Generate website

    docker run -v `pwd`:/srv/jekyll summerisgone/jekyll_s3_website jekyll build

Upload to existing bucket

    docker run -v `pwd`:/srv/jekyll summerisgone/jekyll_s3_website aws s3 sync /srv/jekyll/_site/ s3://example.com
