# Docker Images Downloader

English | [简体中文](README_CN.md)

A GitHub Action to cache Docker image files.

## Usage

### Option 1: Manual trigger (recommended)

1. Go to the **Actions** tab, select the **Download** workflow.
2. Click **Run workflow**, enter the image name (with tag) in **image**, e.g. `testcontainers/ryuk:0.5.1`.
3. For `linux/arm64`, add `-arm64` to the image name (e.g. `testcontainers/ryuk:0.5.1-arm64`) or choose **arm64** in the dropdown.
4. Click **Run workflow** to start. When done, download `image.zip` from the run’s Artifacts.

No tag creation or push is required.

### Option 2: Trigger by creating a tag

Fork and clone this repository, create a tag from the Docker image name, then the Docker image file `image.tar` will be stored in the `image.zip` artifact.

Note: 
- There must not be `:` in git tag, so you should use `--` to represent `:` in the tag name.
- The workflow will use `linux/amd64` platform by default, if you want `linux/arm64` image, you can add suffix `-arm64` in tag name.
- Workflows are not being run on forked repository by default, so you should enable it manually. See [docs](https://docs.github.com/en/actions/using-workflows/disabling-and-enabling-a-workflow?tool=webui#enabling-a-workflow).

For example, to download the Docker image `testcontainers/ryuk:0.5.1`:

```shell
# 'testcontainers/ryuk--0.5.1' represents image 'testcontainers/ryuk:0.5.1'
git tag testcontainers/ryuk--0.5.1
git push origin --tags
```

A GitHub Action will be automatically triggered after the tag is pushed. You can check the run on the [actions](https://github.com/whhe/docker-images-downloader/actions) page. 

After the GitHub Action workflow is complete, you can download the image file from the 'Artifacts' section, then you can load the Docker image by the following commands:

```shell
unzip image.zip
docker load -i image.tar
```

## License


See [LICENSE](LICENSE).