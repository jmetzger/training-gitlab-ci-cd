# Merge Request and branch pipeline (Template) 

```
merge_request_event 
https://docs.gitlab.com/ee/ci/pipelines/merge_request_pipelines.html

merge_request_pipeline 
Alternatively, you can configure your pipeline to run every time you make changes to the source branch for a merge request. This type of pipeline is called a merge request pipeline.

https://gitlab.com/gitlab-org/gitlab/-/blob/master/lib/gitlab/ci/templates/Workflows/MergeRequest-Pipelines.gitlab-ci.yml
(not default)

branch_pipeline 
You can configure your pipeline to run every time you commit changes to a branch. This type of pipeline is called a branch pipeline.
(default)

https://gitlab.com/gitlab-org/gitlab/-/blob/master/lib/gitlab/ci/templates/Workflows/Branch-Pipelines.gitlab-ci.yml

```
