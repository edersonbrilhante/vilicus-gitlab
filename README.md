# Vilicus Gitlab

## How to use
```yaml
include:
  - remote: https://raw.githubusercontent.com/edersonbrilhante/vilicus-gitlab/feature/add-template/Vilicus.gitlab-ci.yml  

# scanning a remote image
remote_image:
  extends: .vilicus
  variables:
    IMAGE: python
  tags:
    - <gitlab-runner>

# build a local image and scanning it
local_image:
  extends: .vilicus
  variables:
    IMAGE: localhost:5000/local-image:${CI_COMMIT_SHORT_SHA}
  script:
    - docker build -t localhost:5000/local-image:${CI_COMMIT_SHORT_SHA} .
    - ./run-job.sh
  tags:
    - <gitlab-runner>
```