Artifacts in GitHub Actions..
Artifacts are used to store and share files generated during a workflow, such as logs, reports, or build outputs.

1️. Upload an Artifact
Artifacts are uploaded using the actions/upload-artifact action.

# Example: Save a Build File
name: Save Build Artifact

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Create a File
        run: echo "Hello, this is a build file!" > output.txt
      - name: Upload Artifact
        uses: actions/upload-artifact@v4
        with:
          name: my-artifact
          path: output.txt
  Uploads output.txt as an artifact named "my-artifact"

2️. Download an Artifact
Artifacts can be downloaded in another job using actions/download-artifact.

# Example: Retrieve the Artifact
jobs:
  deploy:
    runs-on: ubuntu-latest
    needs: build  # Wait for the build job
    steps:
      - name: Download Artifact
        uses: actions/download-artifact@v4
        with:
          name: my-artifact
      - name: Show Artifact Content
        run: cat output.txt
 Downloads my-artifact and prints output.txt

3. Upload Multiple Files
      - name: Upload Logs
        uses: actions/upload-artifact@v4
        with:
          name: logs
          path: logs/*.log  # Upload all .log files in logs/
👉 Uploads all .log files in the logs/ directory

4️. Delete Artifacts (Optional)
GitHub keeps artifacts for 90 days by default, but you can set an expiry time.
     - name: Upload with Expiry
        uses: actions/upload-artifact@v4
        with:
          name: temporary-artifact
          path: output.txt
          retention-days: 7  # Delete after 7 days
