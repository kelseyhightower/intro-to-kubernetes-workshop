# Install GCE client tools

## Install the Google 'gcloud' SDK

Follow the instructions [here](https://cloud.google.com/sdk/) to install gcloud.
Then, set the Google Cloud project that you want to use for this lab as the default, by running:

```
gcloud config set project <your-project-id>
gcloud config set compute/zone us-central1-f
gcloud config set compute/region us-central1
```

Note: if you don't yet have a Google Cloud project created, then follow the signup
instructions [here](https://cloud.google.com/compute/docs/signup).

Grab the service account docs from here:

[Google Service Account Docs](https://developers.google.com/console/help/new/#serviceaccounts)
