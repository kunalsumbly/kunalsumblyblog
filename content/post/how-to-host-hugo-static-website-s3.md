+++
title= "Personal Blog on AWS S3 using Hugo"
keywords = ["Hugo", "AWS S3", "Static website", "CloudFront"]
date= 2021-02-28T22:29:18+11:00
description = "Static web site hosting is very common on S3 buckets. This tutorial walks through how to setup a simple blog on AWS S3 and using CloudFront for content caching"
topics = ["Hugo", "AWS S3", "CloudFront", "Route53"]
tags = ["Hugo", "AWS S3", "CloudFront", "Route53"]
type = "post"
+++


# Problem statement

In this tutorial we will be hosting a static website on AWS S3 bucket. The website domain will be registered on AWS Route53 which in AWS world acts both as a Domain registrar and a DNS provider. Also we would be using another AWS service called CloudFront that is similar to Akamai. CloudFront acts as a CDN (Content Delivery Network) which in layman's terms means a blazing fast cache to store static content closer to the user's geographical location. 

# High Level Architecture

The diagram below has been copied from the AWS website itself. Also this reference architecture is advocated by AWS to protect the web application against DDoS Attacks.

![architecture](/img/Architecture_R53_CDN.png)

In our specific use case, the Step 5 redirect does not happen via S3 and it actually handled by CloudFront.

# Tools inventory

* **AWS S3 bucket**  
    Use S3 to host your static website. Incurs usual cost for using standard storage class 

* **AWS Route 53**  
    As Domain Registrar (**kunalsumbly.com**) and DNS service (using Alias records to point to my CloudFront distribution). A new domain costs you around 12 USD per year.   

* **CloudFront**  
    Caching static content close to users thereby enhancing user experience. Charges for caching static content. So need to carefully select the pricing tier. 
* **AWS CLI**   
    Because using CLI is fun and lets agree, AWS console can get boring. 
* **Hugo static website generator**  
    Saves you a lot of hassle if all you need is a simple static website to host your blog. Hugo setup instructions are available here https://gohugo.io/getting-started/installing/
* **Hugo theme**  
    hyde-y is the theme that we have used in this example, it provides standard left menu style navigation and easy integration with **Disqus** for user comment management. The theme can be downloaded from here https://github.com/enten/hyde-y
* **Disqus**  
   Disqus is a cool platform to engage with the audience, user comment moderation and to understand your audience and optimize the content strategy. They do offer different pricing tier depending on your specific usecase. For this exercise we are using free plan.  
   
    After creating a Disqus account and entering the website details in Disqus, it will generate a JS code snippet that we would need to embed in our website, to complete the integration with Disqus. More details on Disqus here https://disqus.com/features/engage/


# S3 bucket setup

Create S3 bucket with the same name as domain (**kunalsumbly.com**) and enable static website hosting and public access for now. This is quite useful to initial testing and can be turned off later. We don't want anonymous access allowed on the S3 bucket. The bucket and its content are not open to public and only CloudFront has access to the bucket using **Origin Access Identity (OAI)** user. This is configured during setting up CloudFront distribution and setting up S3 bucket as origin and configuring OAI, which is a secure way of accessing bucket contents from CloudFront. More on this in the CloudFront Section.


# Route 53 setup

First you need to buy a domain in Route 53 which should automatically create a Hosted Zone in Route 53. A hosted zone in AWS is critical for proper DNS resolution.

A hosted zone will have multiple records (record type A, AAAA , CNAME or Alias). In this case , we would be using Alias records for our root domain [**.kunalsumbly.com**] and for sub-domain [**www.kunalsumbly.com**] to point to our cloudfront distribution. 

A good tip is to first host the website on S3 and create alias records to point to S3 so that we can test Route53 DNS resolution and if everything works fine, flip the Alias records to point to cloudfront distribution.

# CloudFront setup



# Curious case of Lambda Edge

A specific usecase of Lambda Edge in which Node.js code gets deployed on Regional Cache locations closer to users to append index.html for every request URI that user requests, to help redirect user to the index.html of a sub-directory. More on this later, this is actually to circumvent an issue which comes when pointing to cloudFront distribution. CloudFront by default only points to the index.html located at the base of the s3 bucket. It is not able to redirect the request to the index.html of the subfolders within a S3 bucket. 

Why is this a problem? Well our static website consists of multiple sub-directories and each sub-directory has its own index.html that contains the content for the respective sub-directory. So when the user request /kunalsumbly.com/posts/ the CloudFront should actually serve  /kunalsumbly.com/posts/index.html and which is not possible without actually appending /index.html so every user request. This is where Lambda edge comes into picture that actually intercepts each user-request and appends /index.html at the end. 

