# npm-install-strapi-provider-upload-aws-s3-plus-cdn-public-access

npm install strapi-provider-upload-aws-s3-plus-cdn-public-access

## Background

I needed to use **Digital Ocean CDN Origin URL** on my **strapi version 3.6.5** to make uploads to the CDN and needed that URL returned the media link with .*cdn* URL.

So I found in this page https://snyk.io/advisor/npm-package/strapi-provider-upload-aws-s3-plus-cdn-public-access#package-footer the parcial solution.

After testing for a while, it work.

Down below I bring to you the solution that worked for me.

**Remember:** I used this solution to connect **Digital Ocean CDN Origin**  with **Strapi Version 3.6.5**  through **aws-s3-plus-cdn-public-access**.

## Configuration

The  **allowPublicAccess**  variable needs to be set to true if your Cloudfront S3 bucket access is set to "Don't use OAI (bucket must allow public access)". Otherwise, make sure the allowPublicAccess variable is set to false.

**./config/plugins.js**

    module.exports = ({ env }) => {
	    return {
		    upload: {
			    provider:  'aws-s3-plus-cdn-public-access',
			    providerOptions: {
				    accessKeyId:  env('AWS_ACCESS_KEY_ID'),
				    secretAccessKey:  env('AWS_ACCESS_SECRET'),
				    endpoint:  env('AWS_ENDPOINT'),
				    region:  env('AWS_REGION'),
				    params: {
					    Bucket:  env('AWS_BUCKET'),
				    },
				    cdnUrl:  env('CDN_URL'),
				    allowPublicAccess:  env('AWS_CDN_ALLOW_PUBLIC_ACCESS'),
			    },
		    },
	    };
    };

**.env**

    AWS_ACCESS_KEY_ID=xxxxxxxxxxxxx
    AWS_ACCESS_SECRET=xxxxxxxxxxxxx
    AWS_ENDPOINT=nyc3.digitaloceanspaces.com
    AWS_CDN_ENDPOINT=nyc3.cdn.digitaloceanspaces.com
    AWS_REGION=us-east-1
    AWS_BUCKET=bucket-name-you-created
    CDN_URL=https://bucket-name-you-created.nyc3.cdn.digitaloceanspaces.com/
    AWS_CDN_ALLOW_PUBLIC_ACCESS=true


## Credits
https://snyk.io/advisor/npm-package/strapi-provider-upload-aws-s3-plus-cdn-public-access#package-footer
https://www.npmjs.com/package/strapi-provider-upload-aws-s3-plus-cdn
