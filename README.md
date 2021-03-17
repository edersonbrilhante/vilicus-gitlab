# Vilicus Gitlab

## How to use
```yaml
include:
  - project: 'https://github.com/edersonbrilhante/vilicus-gitlab'
    ref: 'main'
    file: 'Vilicus.gitlab-ci.yml'

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