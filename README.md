# Kunal Sumbly's Personal Blog

If you've found yourself here, you're probably being ambitious and updating your blog again.

Please find the steps to build and deploy that you've probably forgotten about by now:

  * Run `hugo` to build
  * Test things out locally with `hugo server`
  * Switch to public folder `cd public`
  * S3 Upload  `aws s3 sync . s3://kunalsumbly.com --force --delete`
  * (optional) create a cache invalidation on Cloudfront

Inspired from https://github.com/jrzimmerman/justinzimmerman.net
