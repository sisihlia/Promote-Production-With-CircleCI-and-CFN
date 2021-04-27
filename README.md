# Promote-Production-With-CircleCI-and-CFN

Deploy cloudfront.yaml

aws cloudformation deploy \
--template-file cloudfront.yaml \
--stack-name production-distro \
--parameter-overrides PipelineID="${S3_BUCKET_NAME}" \ # Name of the S3 bucket you created manually.
--tags project=udapeople &


Deploy bucket.yaml

aws cloudformation deploy \
--template-file bucket.yml \
--stack-name "${CIRCLE_WORKFLOW_ID:0:7}" \ # ${CIRCLE_WORKFLOW_ID:0:7} takes the first 7 chars of the variable CIRCLE_CI_WORKFLOW_ID
--parameter-overrides PipelineID="${CIRCLE_WORKFLOW_ID:0:7}"
