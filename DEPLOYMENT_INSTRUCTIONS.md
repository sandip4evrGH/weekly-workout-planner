# Weekly Workout Planner - S3 Deployment

This project hosts the static Weekly Workout Planner as a serverless static website using Amazon S3.

## Live Website
Your app is currently live and publicly accessible at this URL:
👉 **[http://workout-plan-app-723626972697.s3-website-us-east-1.amazonaws.com/](http://workout-plan-app-723626972697.s3-website-us-east-1.amazonaws.com/)**

---

## How it was Deployed (Architecture)

Since this app operates entirely inside the browser using JavaScript and does not require a backend server (e.g. Node.js or Python) or a database, we used **Amazon S3 Static Website Hosting**. 

This is incredibly lightweight, secure, and costs virtually $0.00 per month compared to a traditional EC2 server.

### Steps Executed

1. **Created a dedicated S3 Bucket** named `workout-plan-app-723626972697` in the `us-east-1` region.
2. **Disabled "Block All Public Access"** on the bucket so that anyone on the internet can load the HTML file.
3. **Attached a Bucket Policy** allowing the action `s3:GetObject` for any internet visitor to silently read the bucket's content.
4. **Enabled "Static Website Hosting"** configuration on the bucket, setting the index document to `index.html`.
5. **Uploaded `index.html`** (The Workout Planner app) and set its content type to `text/html`.

### How to Update It Later

If you want to edit your code locally and push an update to the live site, simply open your terminal and run this sync command:

```powershell
aws s3 sync d:\workspace\workout-planner s3://workout-plan-app-723626972697/
```

### Next Level Security & Custom Domain (Optional)
If you eventually want to put this app on your own domain (like `www.myworkout.com`) and secure it with a green padlock lock icon (`https`), you would deploy **Amazon CloudFront** in front of this S3 bucket. CloudFront acts as a global caching firewall and will issue you a completely free SSL certificate via AWS Certificate Manager.
