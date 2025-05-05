🚀 Flask CI/CD Pipeline using GitHub, Jenkins, and Webhooks
This project demonstrates a basic DevOps CI/CD pipeline that automatically deploys a simple Flask "Hello World" app using GitHub, Jenkins, and Webhooks.

📌 Objective
Automate the deployment process such that:

Code is pushed to GitHub

A webhook triggers a Jenkins job

Jenkins pulls the latest code, installs dependencies, and restarts the Flask app

🗂️ Project Structure
bash
Copy
Edit
flask-cicd-demo/
├── app.py               # Simple Flask app
├── requirements.txt     # Python dependencies
└── README.md            # Project documentation
🧱 Tech Stack
Python 3.11

Flask

Jenkins (running on Windows)

GitHub Webhooks

Ngrok (for exposing localhost to the internet)

(Optional) GitHub Actions

🔧 Setup Instructions
1. Clone the Repository
bash
Copy
Edit
git clone https://github.com/Pranav-Saraswat/flask-cicd-demo.git
cd flask-cicd-demo
2. Install Flask Locally (Optional)
bash
Copy
Edit
pip install -r requirements.txt
python app.py
Visit: http://localhost:5000
Output: Hello World from Flask CI/CD!

3. Install Jenkins on Windows
Download Jenkins: https://www.jenkins.io/download/

Follow the installation steps

Access Jenkins at: http://localhost:8080

To unlock Jenkins:

bash
Copy
Edit
type "C:\Program Files (x86)\Jenkins\secrets\initialAdminPassword"
4. Expose Jenkins to GitHub using Ngrok
Download Ngrok: https://ngrok.com

Run the following command in Command Prompt or PowerShell:

bash
Copy
Edit
ngrok http 8080
You’ll get a public URL like: https://abcd1234.ngrok.io

5. Configure Jenkins Freestyle Job
Open Jenkins → New Item → Name: flask-cicd-job → Select Freestyle project

Source Code Management:

Select Git

Paste your GitHub HTTPS repo URL

Build Triggers:

✅ Check: GitHub hook trigger for GITScm polling

Build → Execute Windows batch command:

bat
Copy
Edit
cd %WORKSPACE%
python -m venv venv
call venv\Scripts\activate
pip install -r requirements.txt
taskkill /F /IM python.exe >nul 2>&1
start /B python app.py
6. Set Up GitHub Webhook
Go to your repo on GitHub → Settings → Webhooks → Add Webhook

Fill in:

Payload URL: https://<your-ngrok-subdomain>.ngrok.io/github-webhook/

Content type: application/json

Events: Just the push event

Click Add Webhook

✅ 7. Trigger a Test Deployment
bash
Copy
Edit
echo "# trigger" >> README.md
git add .
git commit -m "Trigger Jenkins"
git push
Go to Jenkins → Build should start automatically

Visit http://localhost:5000 to see your app running

🔁 CI/CD Pipeline Flow
Developer pushes code to GitHub

GitHub Webhook triggers Jenkins via Ngrok

Jenkins job executes:

Pulls latest code

Installs dependencies

Restarts Flask app

📷 Optional Screenshots
Description	Screenshot Placeholder
Jenkins Job Configuration	(Add screenshot here)
GitHub Webhook Setup	(Add screenshot here)
Flask App in Browser	(Add screenshot here)
Jenkins Console Output	(Add screenshot here)

📝 Assumptions & Limitations
Jenkins and Flask app run on the same Windows machine

Ngrok must remain active for GitHub webhooks to function

No production-grade process managers like supervisor or systemd

No rollback or advanced error handling

Designed for educational/demo purposes, not production use

📬 Feedback
Have questions or ideas?
Feel free to open an issue or submit a pull request.


