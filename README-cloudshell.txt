================================================================================
Google Cloud Skills Arcade Build-a-thon: Deploy Your AI Agent
================================================================================

Welcome to the Cloud Shell environment for your Arcade Build-a-thon deployment!
Follow the steps below to configure, build, and deploy your containerized AI agent 
to Google Cloud Run and verify your project for Arcade Points.

--------------------------------------------------------------------------------
VERIFIED PROJECT LINKS & SUBMISSION DETAILS
--------------------------------------------------------------------------------
- Live Deployed Agent URL: https://arcade-agent-pc6zhbm6hq-uc.a.run.app/
- YouTube Video Demo:     https://youtu.be/NPT3CX7drNg?si=oXlEzkfsDzhTCZKt
- Google Drive Video:     https://drive.google.com/file/d/1TAmtakUw1Hr7k6Rm_dwIAIw7N4UvWnlA/view?usp=sharing
- Google Developer:       https://g.dev/swapnil03

--------------------------------------------------------------------------------
STEP 1: Navigate to the Project Directory
--------------------------------------------------------------------------------
In your Cloud Shell terminal, run:

  cd ~/arcade-buildathon-7b4m

--------------------------------------------------------------------------------
STEP 2: Set Environment Variables & Google Cloud Project
--------------------------------------------------------------------------------
Run the following commands to configure your project ID and region:

  export PROJECT_ID=$(gcloud config get-value project)
  export REGION="us-central1"
  gcloud config set compute/region $REGION

--------------------------------------------------------------------------------
STEP 3: Enable Required Google Cloud Services & Permissions
--------------------------------------------------------------------------------
Run the permission grant script (from Grant-permission.txt) or enable manually:

  gcloud services enable \
    compute.googleapis.com \
    aiplatform.googleapis.com \
    cloudbilling.googleapis.com \
    run.googleapis.com \
    cloudbuild.googleapis.com \
    artifactregistry.googleapis.com

--------------------------------------------------------------------------------
STEP 4: Deploy Your AI Agent to Cloud Run
--------------------------------------------------------------------------------
Deploy directly using source-based deployment:

  [ -f ~/.arcade-agent-verify-token ] || openssl rand -hex 16 > ~/.arcade-agent-verify-token
  VERIFY_TOKEN=$(cat ~/.arcade-agent-verify-token)

  gcloud run deploy arcade-agent \
    --source . \
    --region us-central1 \
    --no-invoker-iam-check \
    --max-instances=1 \
    --set-env-vars VERIFY_TOKEN=$VERIFY_TOKEN \
    --quiet

--------------------------------------------------------------------------------
STEP 5: Test & Verify Your Deployed AI Agent
--------------------------------------------------------------------------------
1. After deployment finishes, Cloud Run will print the Service URL:
   Live Service URL: https://arcade-agent-pc6zhbm6hq-uc.a.run.app/

2. Test the health check endpoint:
   curl https://arcade-agent-pc6zhbm6hq-uc.a.run.app/healthz

3. Test sending a message via the REST API:
   curl -X POST https://arcade-agent-pc6zhbm6hq-uc.a.run.app/chat \
     -H "Content-Type: application/json" \
     -d '{"message": "Hello Arcade AI Agent!"}'

4. Open the Service URL in your browser to interact with the DevOps Config Reviewer:
   https://arcade-agent-pc6zhbm6hq-uc.a.run.app/

--------------------------------------------------------------------------------
STEP 6: Submit for Arcade Points & Bonus
--------------------------------------------------------------------------------
- Live Service URL: https://arcade-agent-pc6zhbm6hq-uc.a.run.app/
- Video Demonstration: https://youtu.be/NPT3CX7drNg?si=oXlEzkfsDzhTCZKt
- Backup Video Demo: https://drive.google.com/file/d/1TAmtakUw1Hr7k6Rm_dwIAIw7N4UvWnlA/view?usp=sharing
- Developer Profile: https://g.dev/swapnil03
- Share with hashtags: #GoogleCloud #GEAR #ArcadeBuildathon
================================================================================
