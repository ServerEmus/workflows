# Workflows
Github worklow collection

To get the latest files to add into the project:
- Go to Template
- Copy all
- Paste into .github/workflows/
- Open the yml files and rename the RENAME_ME to the csproj file name you want to publish
- Commit changes

# Purpose of individual files
### Auto Update
This workflow is automaticly updates all dependencies to latest.\
It will break the project fully if major changes happened.\
!! This should run once a week or once a month.

### Build
This workflow is simply building and testing the file (if has tests).\
The result will be uploaded to artifacts so can be downloaded.

### Build DLL
This workflow is building a dll/so/dylib while also doing the same as the Build.\
Note: \
IF the csproj is using x32 instead of x86 you have to set a `platform32: x32` too.\
Also make sure you have different name for the 32 and 64 bit dll.

### Package
This workflow is building a package and pushing into github packages.\
Use this if you working with something that is a github packages related.

### Pre Release
This workflow is building a pre-relase version of the targeted project.\
It also publishes into github and the file everything in the output zipped.

# Arguments
### Auto update
runner: This is the OS the auto update runs on.\
TOKEN: Github token to push changes into repository.
```yml
with:
    runner: ubuntu-latest
secrets:
    TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Build
ProjName: Name of the csproj file it being used. It is also for path "MyTestProject/MyTestProject.csproj"\
uploadName: Uploading the artifact with this name if set.\
runner: This is the OS the auto update runs on.\
TOKEN: Github token to push changes into repository.
```yml
with:
    ProjName: MyTestProject
    uploadName: MyTestProject
    runner: ubuntu-latest
secrets:
    TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Build DLL
ProjName: Name of the csproj file it being used. It is also for path "MyTestProject/MyTestProject.csproj"\
uploadName: Uploading the artifact with this name if set.\
platform32: Name of the 32 bit platform.\
platform64: Name of the 64 bit platform.\
TOKEN: Github token to push changes into repository.
```yml
with:
    ProjName: MyTestProject
    uploadName: MyTestProject
    platform32: x32
    platform64: x64
secrets:
    TOKEN: ${{ secrets.GITHUB_TOKEN }}
    Sign: ${{ secrets.Sign_PFX }}
```

### Package
ProjName: Name of the csproj file it being used. It is also for path "MyTestProject/MyTestProject.csproj"\
PackagePrefix: The prefix of the package to upload into github packages.
runner: This is the OS the auto update runs on.
TOKEN: Github token to push changes into repository.
```yml
with:
    ProjName: MyTestProject
    PackagePrefix: ServerEmus.
    runner: ubuntu-latest
secrets:
    TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Pre Release
ProjName: Name of the csproj file it being used. It is also for path "MyTestProject/MyTestProject.csproj"\
uploadName: Uploading the artifact with this name if set.\
runner: This is the OS the auto update runs on.
TOKEN: Github token to push changes into repository.
```yml
with:
    ProjName: MyTestProject
    uploadName: MyTestProject-L
    runner: ubuntu-latest
secrets:
    TOKEN: ${{ secrets.GITHUB_TOKEN }}
```