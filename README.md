# Graphene OS building (Ubuntu 22.04, Pixel 7)

### Get sources
```shell
repo init -u https://github.com/GrapheneOS/platform_manifest.git --depth=1
repo sync -j8
```

### Install vendor files

#### Setup `nodejs 18`

Install and switch:

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
nvm install 18
nvm use 18
```

Setup environment:

```shell
export NODE_PATH=/usr/lib/nodejs:/usr/share/nodejs
```

#### Extracting vendor files for Pixel 7

```shell
yarnpkg install --cwd vendor/adevtool/
```

```shell
source build/envsetup.sh
```

```shell
lunch sdk_phone64_x86_64-cur-user
```

```shell
m aapt2
```

```shell
adevtool generate-all -d panther
```

### Setup OS build environment

```shell
source build/envsetup.sh
```

```shell
lunch panther-cur-userdebug
```

```shell
export OFFICIAL_BUILD=false
```

### Building

Clean `out/` directory:

```shell
rm -r out
```

#### For development purposes only:

```shell
m
```

#### For production:

```shell
m vendorbootimage vendorkernelbootimage target-files-package
```

### Flash

#### Development build:

```shell
fastboot flashall -w
```
