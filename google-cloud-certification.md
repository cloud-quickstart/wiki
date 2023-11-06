# Google Cloud Certification

## Areas to review
- [Binary Authorization](https://cloud.google.com/binary-authorization) - only trusted containers are deployed to GKE or Cloud Run
- non-GKE deployment frameworks like appspot
- [Firebase Test Lab](https://firebase.google.com/docs/test-lab) iOS and Android testing
- Pub/Sub - triage producer perf
- gke horizantal pod autoscaling
- GKE autopilot security - https://unit42.paloaltonetworks.com/gke-autopilot-vulnerabilities/
- Service Perimeter - https://cloud.google.com/vpc-service-controls/docs/service-perimeters


## Google Services

## SRE Principles
Google has defined Site Reliability Engineering tenets.

Emergency Response (MTTR, MTTF)

Capacity Planning

Change Management

Error Budget

Monitoring (Alerts, Tickets, Logging/Metrics)
Provisioning


## Google Professional Machine Learning Engineer
- https://cloud.google.com/learn/certification/machine-learning-engineer
- 1 time practice test per org - https://docs.google.com/forms/d/e/1FAIpQLSeYmkCANE81qSBqLW0g2X7RoskBX9yGYQu-m1TtsjMvHabGqg/viewform 
- 
### PMLE Training
- [https://www.cloudskillsboost.google/cou](https://www.cloudskillsboost.google/course_sessions/5978131/video/411368)

## PMLE Notes
- Machine Learning Crash Course https://developers.google.com/machine-learning/crash-course/representation/cleaning-data
- learn gradient ascent and expand the partial derivative section - "the negative of the gradient vector points into the valley" https://developers.google.com/machine-learning/crash-course/reducing-loss/gradient-descent
- deep field before deep learning https://esahubble.org/images/heic0611b/ https://simbad.u-strasbg.fr/simbad/sim-id?Ident=Hubble+Ultra+Deep+Field
- https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software
- tree classifier using area under the curve - https://dmip.webs.upv.es/papers/ICML2002presentation.pdf - the greater AUC means better positive/negative classification
- XGBoost - https://xgboost.readthedocs.io/en/stable/tutorials/model.html https://www.analyticsvidhya.com/blog/2018/09/an-end-to-end-guide-to-understand-the-math-behind-xgboost/#:~:text=XGBoost%20is%20a%20machine%20learning,won%20several%20machine%20learning%20competitions.
- https://medium.com/google-cloud/vertex-ai-pipelines-vs-cloud-composer-for-orchestration-4bba129759de#:~:text=Vertex%20AI%20Pipelines%20is%20serverless,Even%20with%20GPUs%20if%20needed.
- https://cloud.google.com/blog/products/ai-machine-learning/schedule-and-execute-notebooks-with-vertex-ai-workbench
- https://codelabs.developers.google.com/vertex_notebook_executor#0
- https://www.tensorflow.org/guide/tpu#distribution_strategies
- TPU nodes(gRPC)/VMs(ssh) and twisted topology https://cloud.google.com/tpu/docs/system-architecture-tpu-vm
- TPU V4 up to 2048 TPU cores - https://cloud.google.com/tpu/docs/supported-tpu-configurations
- JAX Autograd (automated gradient function) and XLA (Accelerated Linear Algebra - see cuBLAS) https://jax.readthedocs.io/en/latest/
- https://neptune.ai/blog/retraining-model-during-deployment-continuous-training-continuous-testing
- hashing or homomorphic encryption https://fastdatascience.com/sensitive-data-machine-learning-model/
- TensorFlow Data Validation and Pandas https://www.tensorflow.org/tfx/data_validation/get_started
- TensorFlow from Google Brain https://en.wikipedia.org/wiki/TensorFlow#TensorFlow
- Batch and Streaming data processing https://beam.apache.org/
- https://medium.com/mlpoint/pandas-for-machine-learning-53846bc9a98b
- training with mini-batch gradient descent https://towardsdatascience.com/batch-mini-batch-stochastic-gradient-descent-7a62ecba642a
- https://en.wikipedia.org/wiki/Regularization_%28mathematics%29
- training with L1 regularization (prevent overfitting) https://towardsdatascience.com/regularization-in-deep-learning-l1-l2-and-dropout-377e75acc036
- small normalized wide dataset (reduce feature scaling for training) https://developers.google.com/machine-learning/data-prep/transform/normalization
- PCA https://www.analyticsvidhya.com/blog/2022/07/principal-component-analysis-beginner-friendly/
- reduce ML latency https://cloud.google.com/architecture/minimizing-predictive-serving-latency-in-machine-learning#optimizing_models_for_serving
- https://en.wikipedia.org/wiki/Decision_tree_pruning
- https://en.wikipedia.org/wiki/Confusion_matrix
- https://www.tensorflow.org/guide/keras/serialization_and_saving
- https://www.tensorflow.org/guide/saved_model
- https://cloud.google.com/vertex-ai/docs/model-registry/introduction

- https://developers.google.com/machine-learning/crash-course/classification/roc-and-auc
- https://colab.research.google.com/github/Fraud-Detection-Handbook/fraud-detection-handbook/blob/main/Chapter_4_PerformanceMetrics/ThresholdBased.ipynb
- https://colab.research.google.com/github/Fraud-Detection-Handbook/fraud-detection-handbook/blob/main/Chapter_4_PerformanceMetrics/ThresholdFree.ipynb
- https://cloud.google.com/storage/docs/encryption
- https://cloud.google.com/vertex-ai/docs/workbench/managed/schedule-managed-notebooks-run-quickstart
- https://cloud.google.com/vertex-ai/docs/pipelines/run-pipeline
- https://cloud.google.com/architecture/setting-up-mlops-with-composer-and-mlflow
- https://cloud.google.com/tpu/docs/intro-to-tpu#when_to_use_tpus
- https://www.tensorflow.org/guide/distributed_training
- https://www.tensorflow.org/tutorials/distribute/multi_worker_with_ctl
- https://cloud.google.com/dlp/docs/transformations-reference#transformation_methods
- https://cloud.google.com/blog/products/identity-security/next-onair20-security-week-session-guide
- https://cloud.google.com/dlp/docs/creating-job-triggers
- https://www.tensorflow.org/tfx/guide/tfdv
- https://cloud.google.com/tensorflow-enterprise/docs/overview
- https://cloud.google.com/architecture/ml-modeling-monitoring-analyzing-training-server-skew-in-ai-platform-prediction-with-tfdv
- https://developers.google.com/machine-learning/crash-course/representation/cleaning-data
- https://developers.google.com/machine-learning/testing-debugging/metrics/interpretic
- https://developers.google.com/machine-learning/crash-course/regularization-for-sparsity/l1-regularization
- https://developers.google.com/machine-learning/crash-course/feature-crosses/video-lecture
- https://cloud.google.com/blog/products/ai-machine-learning/building-ml-models-with-eda-feature-selection
- https://developers.google.com/machine-learning/crash-course/regularization-for-sparsity/l1-regularization
- https://cloud.google.com/vertex-ai/docs/training/hyperparameter-tuning-overview
- https://cloud.google.com/vertex-ai/docs/vizier/overview
- https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-1.0.7/google_cloud_pipeline_components.v1.hyperparameter_tuning_job.html#google_cloud_pipeline_components.v1.hyperparameter_tuning_job.HyperparameterTuningJobRunOp
- https://developers.google.com/machine-learning/testing-debugging/common/model-errors#establish-a-baseline
- https://cloud.google.com/automl-tables/docs/evaluate#evaluation_metrics_for_regression_models
- https://developers.google.com/machine-learning/glossary#baseline
- https://cloud.google.com/ai-platform/training/docs/training-at-scale
- https://cloud.google.com/ai-platform/training/docs/machine-types#scale_tiers
- https://cloud.google.com/vertex-ai/docs/training/distributed-training
- https://cloud.google.com/ai-platform/training/docs/overview#distributed_training_structure
- https://github.com/tensorflow/mesh
- https://cloud.google.com/vertex-ai/docs/featurestore/overview#benefits
- https://cloud.google.com/architecture/ml-on-gcp-best-practices#model-deployment-and-serving
- https://cloud.google.com/memorystore/docs/redis/redis-overview
- https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview
- https://cloud.google.com/vertex-ai/docs/ml-metadata/introduction
- https://cloud.google.com/vertex-ai/docs/pipelines/visualize-pipeline
- https://cloud.google.com/architecture/ml-modeling-monitoring-automating-server-data-skew-detection-in-ai-platform-prediction
- https://cloud.google.com/vertex-ai/docs/model-monitoring/overview
- https://cloud.google.com/automl-tables/docs/problem-types
- https://cloud.google.com/blog/products/gcp/predicting-community-engagement-on-reddit-using-tensorflow-gdelt-and-cloud-dataflow-part-2
- https://www.tensorflow.org/tutorials/keras/regression
- https://www.tensorflow.org/tutorials/keras/classification
- https://cloud.google.com/architecture/best-practices-for-ml-performance-cost
- https://www.tensorflow.org/lite/performance/model_optimization
- https://www.tensorflow.org/tutorials/images/transfer_learning
- https://developers.google.com/machine-learning/data-prep/construct/sampling-splitting/imbalanced-data
- https://colab.research.google.com/github/tensorflow/docs/blob/master/site/en/tutorials/structured_data/imbalanced_data.ipynb
- https://colab.research.google.com/github/stellargraph/stellargraph/blob/master/demos/calibration/calibration-node-classification.ipynb
- https://developers.google.com/machine-learning/glossary#calibration-layer
- https://developers.google.com/machine-learning/testing-debugging/common/overview
- https://developers.google.com/machine-learning/crash-course/regularization-for-simplicity/l2-regularization
- https://developers.google.com/machine-learning/crash-course/regularization-for-sparsity/l1-regularization
- https://cloud.google.com/bigquery-ml/docs/preventing-overfitting
- https://www.tensorflow.org/tutorials/keras/overfit_and_underfit
- https://www.tensorflow.org/tensorboard/get_started
- https://cloud.google.com/architecture/guidelines-for-developing-high-quality-ml-solutions#guidelines_for_model_quality
- https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning#data_and_model_validation
- https://cloud.google.com/architecture/implementing-deployment-and-testing-strategies-on-gke
- https://cloud.google.com/architecture/application-deployment-and-testing-strategies#choosing_the_right_strategy
- https://cloud.google.com/vertex-ai/docs/general/deployment
- https://docs.seldon.io/projects/seldon-core/en/latest/analytics/routers.html
- https://cloud.google.com/blog/topics/developers-practitioners/add-preprocessing-functions-tensorflow-models-and-deploy-vertex-ai
- https://www.tensorflow.org/tutorials/customization/custom_layers
- https://www.tensorflow.org/api_docs/python/tf/keras/layers/Lambda
- https://developers.google.com/machine-learning/guides/rules-of-ml#rule_32_re-use_code_between_your_training_pipeline_and_your_serving_pipeline_whenever_possible
- https://cloud.google.com/vertex-ai/docs/pipelines/lineage
- https://cloud.google.com/vertex-ai/docs/ml-metadata/tracking
- https://cloud.google.com/vertex-ai/pricing
- https://cloud.google.com/architecture/ml-on-gcp-best-practices#operationalized-training
- https://cloud.google.com/architecture/ml-on-gcp-best-practices#organize-your-ml-model-artifacts

## Google Professional Cloud DevOps Engineer

https://cloud.google.com/certification/guides/cloud-devops-engineer

### Cloud DevOps Engineer - Certification Exam Guide 

> sections below are from https://cloud.google.com/certification/guides/cloud-devops-engineer as of 20211226

#### Section 1. Applying site reliability engineering principles to a service

1.1 Balance change, velocity, and reliability of the service:

Discover SLIs (e.g., availability, latency)
Define SLOs and understand SLAs
Agree to consequences of not meeting the error budget
Construct feedback loops to decide what to build next
Eliminate toil via automation
1.2 Manage service life cycle:

Manage a service (e.g., introduce a new service, deploy, maintain, and retire it)
Plan for capacity (e.g., quotas and limits management)
1.3 Ensure healthy communication and collaboration for operations:

Prevent burnout (e.g., set up automation processes to prevent burnout)
Foster a learning culture
Foster a culture of blamelessness

#### Section 2. Building and implementing CI/CD pipelines for a service

2.1 Design CI/CD pipelines:

Creating and storing immutable artifacts with Artifact Registry
Deployment strategies with Cloud Build and Spinnaker
Deployment to hybrid and multicloud environments with Anthos, Spinnaker, and Kubernetes
Artifact versioning strategy with Cloud Build and Artifact Registry
CI/CD pipeline triggers with Cloud Source Repositories, external SCM, and Pub/Sub
Testing a new version with Spinnaker
Configuring deployment processes (e.g., approval flows)
2.2 Implement CI/CD pipelines:

CI with Cloud Build
CD with Cloud Build
Open source tooling (e.g., Jenkins, Spinnaker, GitLab, Concourse)
Auditing and tracing of deployments (e.g., CSR, Artifact Registry, Cloud Build, Cloud Audit Logs)
2.3 Manage configuration and secrets:

Secure storage methods
Secret rotation and config changes
2.4 Manage infrastructure as code:

Terraform
Infrastructure code versioning
Make infrastructure changes safer
Immutable architecture
2.5 Deploy CI/CD tooling:

Centralized tools vs. multiple tools (single vs. multi-tenant)
Security of CI/CD tooling
2.6 Manage different development environments (e.g., staging, production):

Decide on the number of environments and their purpose
Create environments dynamically per feature branch with GKE
Local development environments with Docker, Cloud Code, Skaffold
2.7 Secure the deployment pipeline:

Vulnerability analysis with Artifact Registry
Binary Authorization
IAM policies per environment

#### Section 3. Implementing service monitoring strategies

3.1 Manage application logs:

Collecting logs from Compute Engine, GKE with Cloud Logging, Fluentd
Collecting third-party and structured logs with Cloud Logging, Fluentd
Sending application logs directly to the Cloud Logging API
3.2 Manage application metrics with Cloud Monitoring:

Collecting metrics from Compute Engine
Collecting GKE/Kubernetes metrics
Use Metrics Explorer for ad hoc metric analysis
3.3 Manage Cloud Monitoring platform:

Creating a monitoring dashboard
Filtering and sharing dashboards
Configure third-party alerting in Cloud Monitoring (e.g., PagerDuty, Slack)
Define alerting policies based on SLIs with Cloud Monitoring
Automate alerting policy definition with Terraform
Implementing SLO monitoring and alerting with Cloud Monitoring
Understand Cloud Monitoring integrations (e.g., Grafana, BigQuery)
Using SIEM tools to analyze audit/flow logs (e.g., Splunk, Datadog)
Design Cloud Monitoring metrics scopes
3.4 Manage Cloud Logging platform:

Enabling data access logs (e.g., Cloud Audit Logs)
Enabling VPC flow logs
Viewing logs in the Google Cloud Console
Using basic vs. advanced logging filters
Implementing logs-based metrics
Understanding the logging exclusion vs. logging export
Selecting the options for logging export
Implementing a project-level / org-level export
Viewing export logs in Cloud Storage and BigQuery
Sending logs to an external logging platform
3.5 Implement logging and monitoring access controls:

Set ACL to restrict access to audit logs with IAM, Cloud Logging
Set ACL to restrict export configuration with IAM, Cloud Logging
Set ACL to allow metric writing for custom metrics with IAM, Cloud Monitoring

#### Section 4. Optimizing service performance

4.1 Identify service performance issues:

Evaluate and understand user impact
Utilize Google Cloud’s operations suite to identify cloud resource utilization
Utilize Cloud Trace and Cloud Profiler to profile performance characteristics
Interpret service mesh telemetry
Troubleshoot issues with the image/OS
Troubleshoot network issues (e.g., VPC flow logs, firewall logs, latency, view network details)
4.2 Debug application code:

Application instrumentation
Cloud Debugger
Cloud Logging
Cloud Trace
Debugging distributed applications
App Engine local development server
Error Reporting
Cloud Profiler
4.3 Optimize resource utilization:

Identify resource costs
Identify resource utilization levels
Develop plan to optimize areas of greatest cost or lowest utilization
Manage preemptible VMs
Utilize committed use discounts where appropriate
TCO considerations (e.g., security, logging, networking)
Consider network pricing

#### Section 5. Managing service incidents

5.1 Coordinate roles and implement communication channels during a service incident:

Define roles (incident commander, communication lead, operations lead)
Handle requests for impact assessment
Provide regular status updates, internal and external
Record major changes in incident state (e.g., When mitigated? When is all clear?)
Establish communications channels (e.g., email, IRC, Hangouts, Slack, phone)
Scaling response team and delegation
Avoid exhaustion / burnout
Rotate / hand over roles
Manage stakeholder relationships
5.2 Investigate incident symptoms impacting users:

Identify probable causes of service failure
Evaluate symptoms against probable causes; rank probability of cause based on observed behavior
Perform investigation to isolate most likely actual cause
Identify alternatives to mitigate issue
5.3 Mitigate incident impact on users:

Roll back release
Drain / redirect traffic
Turn off experiment
Add capacity
5.4 Resolve issues with deployments (e.g., Cloud Build, Jenkins):

Code change / fix bug
Verify fix
Declare all-clear
5.5 Document issue in a postmortem:

Document root causes
Create and prioritize action items
Communicate postmortem to stakeholders



# Links
- [GCP Flowcharts](https://grumpygrace.dev/posts/gcp-flowcharts/#compute)
- [sathishvj - all exam prep](https://sathishvj.medium.com/on-passing-all-google-cloud-certifications-54b2cc1e428c)
- https://sites.google.com/robertsonmarketing.com/digitalassetdownloadportal/digital-toolkit?authuser=0
- https://docs.google.com/document/d/1geAYSKyh4i44LNYNHxbwggicfjRBkoleGWWfgx-LBI0/edit?resourcekey=0-U_Za7iSr-3Z7zVOtHe7gWQ
