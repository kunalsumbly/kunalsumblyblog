# Kunal Sumbly's Personal Blog

Please find the steps to build and deploy that you've probably forgotten about by now:

  * Run `hugo` to build
  * Test things out locally with `hugo server`
  * Switch to public folder `cd public`
  * S3 Upload  `aws s3 sync . s3://kunalsumbly.com --force --delete`
  * (optional) create a cache invalidation on Cloudfront

