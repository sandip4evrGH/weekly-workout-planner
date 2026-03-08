# 🔥 Weekly Workout Planner

A fully interactive, client-side Weekly Workout Planner that runs entirely in your browser. This application allows users to build, edit, and export their weekly fitness routines directly to their mobile calendar (Google Calendar, Apple Calendar, Outlook) using a drag-and-drop interface.

## ✨ Features
- **True Weekly Calendar View:** A visually responsive 5 AM to 9 PM (17-hour) drag-and-drop grid.
- **Smart Workouts Dashboard:** Add cardio, strength, and flexibility exercises from the pre-built side panel.
- **Save & Load Functionality:** Because taking care of your data matters, you can download a `.json` backup of your fully customized schedule and reload it at any time.
- **Mobile Calendar SYNC:** Clicking *"Sync to Mobile (ICS)"* iterates over your created calendar and algorithmically plots every single workout onto a standard `.ics` file that easily imports right into Apple or Google Calendar.
- **Print Specific CSS:** Need to put it on your fridge? Clicking *"Print"* uses custom `@media print` styling to hide all the UI buttons and menus, rendering a gorgeous, crisp black-and-white table of your week.

## 🚀 How to Run Locally

You don't need Node.js, Python, or a database!
1. Clone this repository to your computer.
2. Double-click the `index.html` file to open it in Chrome, Safari, or Firefox.
3. Start dragging and dropping workouts onto your grid!

---

## ☁️ AWS S3 Hosting & Deployment Architecture

This application functions with 100% vanilla JavaScript on the frontend. This means there is **no backend requirement** (no EC2 or Lambda necessary). 

To give this application to the world as efficiently and cheaply as possible, the project is deployed using **Amazon S3 Static Website Hosting**, lowering hosting costs to roughly **$0.01 / month**.

### Deployment Commands

If you wish to host your own version of this project on an AWS account, you can use the following AWS CLI commands:

**1. Create the bucket (replace the name with your own unique one):**
```bash
aws s3api create-bucket --bucket YOUR-UNIQUE-BUCKET-NAME
```

**2. Open Public Access:**
```bash
aws s3api put-public-access-block --bucket YOUR-UNIQUE-BUCKET-NAME --public-access-block-configuration BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=false,RestrictPublicBuckets=false
```

**3. Set the Read Policy (save the below json to `policy.json` first and replace the bucket name):**
_policy.json_:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": [
        "arn:aws:s3:::YOUR-UNIQUE-BUCKET-NAME/*"
      ]
    }
  ]
}
```
Apply the policy:
```bash
aws s3api put-bucket-policy --bucket YOUR-UNIQUE-BUCKET-NAME --policy file://policy.json
```

**4. Enable Web Hosting & Upload Code:**
```bash
aws s3 website s3://YOUR-UNIQUE-BUCKET-NAME/ --index-document index.html
aws s3 sync . s3://YOUR-UNIQUE-BUCKET-NAME/
```

### Accessing Your Site
Your new website will be publicly available at: 
`http://YOUR-UNIQUE-BUCKET-NAME.s3-website-[region].amazonaws.com`
