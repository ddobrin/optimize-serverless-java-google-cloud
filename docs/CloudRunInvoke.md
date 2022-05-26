gcloud run deploy quotes --image gcr.io/dan-workshop-project-332213/quotes-jvm \
  --add-cloudsql-instances quote-cr-db-instance \
  --set-env-vars INSTANCE_CONNECTION_NAME="quote-cr-db-instance" \
  --set-env-vars DB_NAME="quote_db" \
  --set-env-vars DB_USER="quote_user" \
  --set-env-vars DB_PASS="quote-cr-db-pwd" \
  --set-env-vars INSTANCE_HOST="172.24.0.10" \
  --set-env-vars DB_HOST="172.24.0.10" \
  --set-env-vars DB_PORT="5432" \
  --set-env-vars SERVER.PORT="8080" \
  --set-env-vars SPRING_PROFILES_ACTIVE="cloud-dev" \
  --vpc-connector="quote-connector" \
  --region us-central1 \
  --memory 2Gi \
  --allow-unauthenticated

  curl -H "Authorization: Bearer $(gcloud auth print-identity-token)" https://quotes-ieuwkt6jkq-uc.a.run.app

  =======================

  gcloud run deploy quotes-native --image gcr.io/dan-workshop-project-332213/quotes-native \
  --add-cloudsql-instances quote-cr-db-instance \
  --set-env-vars INSTANCE_CONNECTION_NAME="quote-cr-db-instance" \
  --set-env-vars DB_NAME="quote_db" \
  --set-env-vars DB_USER="quote_user" \
  --set-env-vars DB_PASS="quote-cr-db-pwd" \
  --set-env-vars INSTANCE_HOST="172.24.0.10" \
  --set-env-vars DB_HOST="172.24.0.10" \
  --set-env-vars DB_PORT="5432" \
  --set-env-vars SERVER.PORT="8080" \
  --set-env-vars SPRING_PROFILES_ACTIVE="cloud-dev" \
  --vpc-connector="quote-connector" \
  --region us-central1 \
  --memory 2Gi \
  --allow-unauthenticated



  gcloud run deploy quotes --image gcr.io/dan-workshop-project-332213/quotes-jvm \
  --add-cloudsql-instances quote-cr-db-instance \
  --set-env-vars INSTANCE_CONNECTION_NAME="quote-cr-db-instance" \
  --set-env-vars DB_NAME="quote_db" \
  --set-env-vars DB_USER="quote_user" \
  --set-env-vars DB_PASS="quote-cr-db-pwd" \
  --set-env-vars INSTANCE_HOST="172.24.0.10" \
  --set-env-vars DB_HOST="172.24.0.10" \
  --set-env-vars DB_PORT="5432" \
  --set-env-vars SERVER.PORT="8080" \
  --set-env-vars SPRING_PROFILES_ACTIVE="cloud-dev" \
  --vpc-connector="quote-connector" \
  --region us-central1 \
  --memory 2Gi \
  --service-account cr-quote-service-account \
  --no-allow-unauthenticated

  curl -H "Authorization: Bearer $(gcloud auth print-identity-token)" https://quotes-ieuwkt6jkq-uc.a.run.app

  ---
  curl -v -H 'Content-Type: application/json' -d '{"id":"6","author":"Henry David Thoreau","quote":"Go confidently in the direction of your dreams! Live the life you’ve imagined"}' -X POST 127.0.0.1:8080/quotes

  http POST :8080/quotes author="Henry David Thoreau" quote="Go confidently in the direction of your dreams! Live the life you’ve imagined" id="6"

  http PUT :8080/quotes/6 author="Henry David Thoreau" quote="Go confidently in the direction of your dreams! Live the life you’ve imagined" id="6"

  curl -v -X DELETE 127.0.0.1:8080/quotes/6
  http DELETE :8080/quotes/6

  curl -v -X DELETE 127.0.0.1:8080/quotes/6
  http DELETE :8080/quotes/6  
  ---

  ================================
  gcloud run deploy bff --image gcr.io/dan-workshop-project-332213/bff-jvm \
  --set-env-vars SERVER.PORT="8080" \
  --set-env-vars QUOTES_URL="https://quotes-ieuwkt6jkq-uc.a.run.app" \
  --region us-central1 \
  --memory 2Gi \
  --allow-unauthenticated

  gcloud run deploy bff-native --image gcr.io/dan-workshop-project-332213/bff-native \
  --set-env-vars SERVER.PORT="8080" \
  --set-env-vars QUOTES_URL="https://quotes-native-ieuwkt6jkq-uc.a.run.app" \
  --region us-central1 \
  --memory 2Gi \
  --allow-unauthenticated

  curl -H "Authorization: Bearer $(gcloud auth print-identity-token)" https://bff-ieuwkt6jkq-uc.a.run.app/quotes
  curl -H "Authorization: Bearer $(gcloud auth print-identity-token)" https://bff-native-ieuwkt6jkq-uc.a.run.app/quotes