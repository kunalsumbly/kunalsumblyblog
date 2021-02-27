# Justin Zimmerman's Personal Blog

Dear future Justin,

If you've found yourself here, you're probably being ambitious and updating your blog again.

Please find the steps to build and deploy that you've probably forgotten about by now:

  * `brew update && brew upgrade` to get the latest version of Hugo
  * Run `hugo` to build
  * Test things out locally with `hugo server`
  * Switch to public folder `cd public`
  * S3 Upload with Cache Control `aws s3 sync . s3://justinzimmerman.net --force --delete --cache-control max-age=172800 --acl public-read --profile justinzimmerman`
  * (optional) create a cache invalidation on Cloudfront

aws cli `sync` will only modify items that need changed, therefore, if cache-control is not working property, empty the bucket, and run the sync command above, do not upload on the s3 dashboard
