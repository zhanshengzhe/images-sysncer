# images-sysncer
name: Sync Image to Aliyun  Example

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Git pull
      uses: actions/checkout@v3

    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2.9.1

    - name: Login to Docker Hub
      uses: docker/login-action@v2.2.0
      with:
        registry: registry.cn-hangzhou.aliyuncs.com
        username: aliyun1983734399
        password: zsz100715!
        logout: false

    - name: Use Skopeo Tools Sync Image to Docker Hub
      run: |
         skopeo copy docker://docker.io/hslr/sun-panel:1.4.0 docker://registry.cn-hangzhou.aliyuncs.com/weiyigeek/sun-panel:1.4.0
