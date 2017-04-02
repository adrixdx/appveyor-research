## AppVeyor

![](https://github.com/adrixdx/appveyor-research/blob/master/research/appveyor.jpg)


Appveyor is a specific tool made to facilitate the automatization of continuous integration, continuous delivery and continuous deployment.

And those pillars means:

-Continuous integration: It's a practice wich integrates all the changes produced in a repository with the server of compilation and ensures every single change in the application is being validated in the recopilation of the questions and the unit tests. 
The main objectives of continuous integration are: find and correct errors faster and optimize software quality.In addition, it also reduces the time it takes to validate and release new versions of an application.


-Continuous delivery:Step that is made after continuous integration. It is about having the necessary elements of the application for its distribution.


-Continuous deployment:Very similar to continuous delivery. However, in this mode, after the build server performs the validation of the build and code, the package is also prepared. However, the distribution / deployment is done automatically in the desired environment.


By the fact of using the continuous integration, thanks to AppVeyor we have a series of benefits like:

-Productivity increase

-Bug identification

-Simple and quick distribution


###How to use AppVeyor

First of all, we need to create and account in AppVeyor

![](https://github.com/adrixdx/appveyor-research/blob/master/research/sign%20up.jpg)

You can create an account of AppVeyor or sign in with an account of Github, VisualStudio Online,or BitBucket.


You have different packages:


-Basic: Wich costs 29$/month and allows you to have 1 private project, 1 concurrent job, 1 GB build cache and forum support.


-Pro: Wich costs 59$/month or 590$/year and allows you to have unlimited private project, 1 concurrent job, 5 GB build cache and priority technical support.


-Premium:Wich costs 99$/month or 990$/year and allows you to have unlimited private project, 2 concurrent job, 20 GB build cache and priority technical support.


Also you have a free trial of 14 days.

![](https://github.com/adrixdx/appveyor-research/blob/master/research/precios.jpg)

After you create an account, now you can select a repository of different programming tools:

![](https://github.com/adrixdx/appveyor-research/blob/master/research/research%20repositorio.jpg)

Select one and you can start using AppVeyor. In that case, it's using a Github repository.


Now you have your project and the first you have to do to see the utility of AppVeyor is create a new build:

![](https://github.com/adrixdx/appveyor-research/blob/master/research/new%20build.jpg)
 
This will integrate all the changes mades until the last commit:

![](https://github.com/adrixdx/appveyor-research/blob/master/research/research%20building%20console.jpg)

You have the message option to see the advices that AppVeyor makes of your code; it will help to find bugs, avoid memory leaks,...

![](https://github.com/adrixdx/appveyor-research/blob/master/research/research%20message%20build.jpg)

Now you have yor repository functionally in AppVeyor, but you need to create an environment to automatize the releases: 

![](https://github.com/adrixdx/appveyor-research/blob/master/research/enviroment.jpg)

When you're creating an environment, first of all you need to decide a provider. In that case, it's using a Github releases.

![](https://github.com/adrixdx/appveyor-research/blob/master/research/enviroment%20creation.jpg)


You will need a GitHub authentication token, and you can find it there:

https://github.com/settings/tokens

You have a lot of provider settings, there's a list:

Tag name (tag) - Optional. If not specified build tag or version is used. You can use environment variables in tag name, for example myproduct-v$(appveyor_build_version).

Release name (release) - Optional. The name of release. If not specified tag name is used as release name. You can use environment variables in release name, for example product release of v$(appveyor_build_version).

Release description (description) - mandatory release description. If not specified, GitHub returns 422: Unprocessable entity error.

GitHub authentication token (auth_token) - OAuth token used for authentication against GitHub API. Minimal token scope is repo or public_repo to release on private or public repositories respectively. Be sure to encrypt your token using the Account → Encrypt data tool.
Artifact to deploy (artifact) - Optional. Allows specifying one or more build artifacts to be uploaded as release assets. The value could be comma-delimited list of artifact’s file name, deployment name or regular expression matching one of these. For example bin\release\MyLib.zip or /.*\.nupkg/. Don’t forget to package your artifact first, as the deployment will fail if this value does not match artifacts.name or artifacts.path (even if the file exists.)

Draft release (draft) - true if draft release should be created; default is false.

Pre-release (prerelease) - true to mark release as “pre-release”; default is false.

Force update (force_update) - true to overwrite files in an existing release; default is false which will fail deployment if the release already exists on GitHub.

You also need a doc in your repository named appveyor.yml where you have to write the next:

deploy:

  release: myproduct-v$(appveyor_build_version)
  
  description: 'Release description'
  
  provider: GitHub
  
  auth_token:
    secure: <your encrypted token>  # your encrypted token from GitHub
    
  artifact: /.*\.nupkg/             # upload all NuGet packages to release assets
  
  draft: false
  
  prerelease: false
  
  on:
  
    branch: master                 # release from master branch only
    
    appveyor_repo_tag: true        # deploy on tag push only

To make the release:

-Add new tag in local repo.

-Push tag to GitHub repo and start a new AppVeyor build.

-Build produces artifacts.


