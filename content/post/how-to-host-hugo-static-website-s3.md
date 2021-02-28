+++
title= "Host Personal Website/Blog on AWS S3 using Hugo"
keywords = ["Hugo", "AWS S3", "Static website", "CloudFront"]
date= 2021-02-28T22:29:18+11:00
description = "Static web site hosting is very common on S3 buckets. This tutorial walks through how to setup a simple blog on AWS S3 and using CloudFront for content caching"
topics = ["Hugo", "AWS S3", "CloudFront", "Route53"]
tags = ["Hugo", "AWS S3", "CloudFront", "Route53"]
type = "post"
+++


# Problem statement

In this tutorial we will be hosting a static website on AWS S3 bucket. The website domain will be registered on AWS Route53 which in AWS world acts both the Domain registrar and DNS provider. Also we would be using another AWS service called CloudFront that is similar to Akamai and acts as a CDN (Content Delivery Network) which in layman's terms means a blazing fast cache to store static content closer to the user's geographical location. 

A specific usecase of Lambda Edge which gets deployed on Regional Cache locations to append index.html for every request URI that user requests, to help redirect user to the index.html of a sub-directory.



# Different Tools involved

* AWS S3 buckets  
-->Use S3 to host your static website
* AWS Route 53  
--> As Domain Registrar (**kunalsumbly.com**) and DNS service (using Alias records to point to my CloudFront distribution)
* CloudFront  
--> Caching static content close to users thereby enhancing user experience
* AWS CLI  
--> Because using CLI is fun and lets agree, AWS console can get boring. 
* Hugo static website generator  
--> Saves you a lot of hastle if all you need is a simple static website to host your blog
* Hugo theme  
--> hyde-y is the theme that we have used in this example, it provides standard left menu style navigation and easy integration with **Disqus** for comments management. 

# S3 bucket setup

Create S3 bucket with the same name as domain (kunalsumbly.com) 


# Route 53 setup

First you need to buy a domain in Route 53 which should automatically create a Hosted Zone in Route 53. A hosted zone in AWS is critical for proper DNS resolution.

A hosted zone will have multiple records (record type A, AAAA , CNAME or Alias). In this case , we would be using Alias records for our root domain [**.kunalsumbly.com**] and for sub-domain [**www.kunalsumbly.com**] to point to our cloudfront distribution. 

A good tip is to first host the website on S3 and create alias records to point to S3 so that we can test Route53 DNS resolution and if everything works fine, flip the Alias records to point to cloudfront distribution



