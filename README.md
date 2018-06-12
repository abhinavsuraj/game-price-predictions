# game-price-predictions
Neural networks for game price predictions

#Execute the export_model_for_cloud final.py to generate the model in the local system.

To upload this model into the google cloud, follow the below steps.
1)Setup the google cloud account the following way
2)Create a google cloud account with with an existing gmail account or a new one.
3)Create a new project in the google cloud account.
-Project will also get assigned a unique key.
4)Enable the google cloud machine learning API for the project.
--Click on the main menu on the left, go to APIs and Services,
5)Provide billing details for your account before you can use some of the features of Google Cloud
6)The next step is to install the Google Cloud SDK.
7)Once you have the Google Cloud SDK installed, activate it by logging in from the command line.
8)Open the command line window in your computer and in that window type gcloud init and hit enter.
9)Google Cloud SDK will attempt to open a web browser window to the Google login page when we hit enter. 
10)Choose the correct account and then click Allow.
Once you see the message "You are now authenticated with the Google Cloud SDK", Your instance is ready.

The buckets and the model can be loaded in the google cloud machine learning using the following steps.
->gsutil mb -l us-central1 gs://tensorflow-class-sonu
->gsutil cp -R exported_model/* gs://tensorflow-class-sonu/earnings_v1/
->gcloud ml-engine models create earnings --regions us-central1
->gcloud ml-engine versions create v8 --model=earnings --origin=gs://tensorflow-class-sonu/earnings_v1/ --runtime-version=1.8
->gcloud ml-engine predict --model=earnings --json-instances=sample_input_prescaled.json

The above command throws the following error:-
{
  "error": "Prediction failed: Error during model execution: AbortionError(code=StatusCode.FAILED_PRECONDITION, details=\"Attempting to use uninitialized value output/biases4\n\t [[Node: output/biases4/read = Identity[T=DT_FLOAT, _output_shapes=[[1]], _device=\"/job:localhost/replica:0/task:0/device:CPU:0\"](output/biases4)]]\")"
}
